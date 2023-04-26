

![[Screenshot from 2023-03-28 10-58-06.png]]

![[Screenshot from 2023-03-28 10-58-40.png]]![[Screenshot from 2023-03-28 10-59-10.png]]![[Screenshot from 2023-03-28 11-00-12.png]]![[Screenshot from 2023-03-28 11-00-31.png]]![[Screenshot from 2023-03-28 11-01-07.png]]


#### controlers

```
import logging

from flask import jsonify

from flask import render_template

from flask import request

from flask import Response

from droneapp.models.drone_manager import DroneManager

import config

logger = logging.getLogger(__name__)

app = config.app

def get_drone():

return DroneManager()

@app.route('/')

def index():

return render_template('controller.html')

@app.route('/api/command/', methods=['POST'])

def command():

cmd = request.form.get('command')

logger.info({'action': 'command', 'cmd': cmd})

drone = get_drone()

# Drone Takeoff

if cmd == 'takeoff':

drone.takeoff()

# Drone Land

if cmd == 'land':

drone.land()

# Drone Go Up

if cmd == 'up':

drone.up()

# Drone Go Down

if cmd == 'down':

drone.down()

# Drone Go Left

if cmd == 'left':

drone.left()

# Drone Go Right

if cmd == 'right':

drone.right()

#Drone Move Forward

if cmd == 'forward':

drone.forward()

# Drone Move Backward

if cmd == 'back':

drone.back()

# Drone Turn Right

if cmd == 'clockwise':

drone.clockwise()

# Drone Turn left

if cmd == 'counterClockwise':

drone.counter_clockwise()

# Drone Doing Flip

if cmd == 'flipFront':

drone.flip_front()

if cmd == 'flipBack':

drone.flip_back()

if cmd == 'flipLeft':

drone.flip_left()

if cmd == 'flipRight':

drone.flip_right()

# Drone Command For Face Detect and Tracking the Face

if cmd == 'faceDetectAndTrack':

drone.enable_face_detect()

if cmd == 'stopFaceDetectAndTrack':

drone.disable_face_detect()

# Command For taking Snapshot From Drone

if cmd == 'snapshot':

if drone.snapshot():

return jsonify(status='success'), 200

else:

return jsonify(status='fail'), 400

return jsonify(status='success'), 200

# Generate Video From Drone into Image

def video_generator():

drone = get_drone()

for jpeg in drone.video_jpeg_generator():

yield (b'--frame\r\n'

b'Content-Type: image/jpeg\r\n\r\n' +

jpeg +

b'\r\n\r\n')

@app.route('/video/streaming')

def video_feed():

return Response(video_generator(), mimetype='multipart/x-mixed-replace; boundary=frame')

def run():

app.run(host=config.WEB_ADDRESS,

port=config.WEB_PORT,

threaded=True)
```

### drone manager

```
import logging

import contextlib

import os

import socket

import subprocess

import threading

import time

import cv2 as cv

import numpy as np

import pickle

from droneapp.models.base import Singleton

# Get Face Recoqnition Trainer File

TRAINER_YML_FILE = './trainner.yml'

recoqnizer = cv.face.LBPHFaceRecognizer_create()

recoqnizer.read(TRAINER_YML_FILE)

labels = {"person_name": 1}

with open("labels.pickle", 'rb') as f:

og_labels = pickle.load(f)

labels = {v:k for k,v in og_labels.items()}

# Initialize Drone

logger = logging.getLogger(__name__)

DEFAULT_DISTANCE = 0.30

DEFAULT_SPEED = 10

DEFAULT_DEGREE = 10

FRAME_X = int(960/3) # 320

FRAME_Y = int(720/3) # 240

FRAME_AREA = FRAME_X * FRAME_Y

FRAME_SIZE = FRAME_AREA * 3

FRAME_CENTER_X = FRAME_X / 2

FRAME_CENTER_Y = FRAME_Y / 2

CMD_FFMPEG = (f'ffmpeg -hwaccel auto -hwaccel_device opencl -i pipe:0 '

f'-pix_fmt bgr24 -s {FRAME_X}x{FRAME_Y} -f rawvideo pipe:1')

# Get Face Detect XML File in Folder

FACE_DETECT_XML_FILE = './droneapp/models/haarcascade_frontalface_default.xml'

# Set Image Folder for Snapshot From Drone

SNAPSHOT_IMAGE_FOLDER = './droneapp/static/img/snapshots'

class ErrorNoFaceDetectXMLFile(Exception):

"""Error no face detect xml file"""

class ErrorNoImageDir(Exception):

"""Error no image dir"""

class DroneManager(metaclass=Singleton):

def __init__(self, host_ip='192.168.10.2', host_port=8889,

drone_ip='192.168.10.1', drone_port=8889,

is_imperial=False, speed=DEFAULT_SPEED):

self.host_ip = host_ip

self.host_port = host_port

self.drone_ip = drone_ip

self.drone_port = drone_port

self.drone_address = (drone_ip, drone_port)

self.is_imperial = is_imperial

self.speed = speed

self.socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

self.socket.bind((self.host_ip, self.host_port))

self.response = None

self.stop_event = threading.Event()

self._response_thread = threading.Thread(target=self.receive_response,

args=(self.stop_event, ))

self._response_thread.start()

self.patrol_event = None

self.is_patrol = False

self._patrol_semaphore = threading.Semaphore(1)

self._thread_patrol = None

self.proc = subprocess.Popen(CMD_FFMPEG.split(' '),

stdin=subprocess.PIPE,

stdout=subprocess.PIPE)

self.proc_stdin = self.proc.stdin

self.proc_stdout = self.proc.stdout

self.video_port = 11111

self._receive_video_thread = threading.Thread(

target=self.receive_video,

args=(self.stop_event, self.proc_stdin,

self.host_ip, self.video_port,))

self._receive_video_thread.start()

if not os.path.exists(FACE_DETECT_XML_FILE):

raise ErrorNoFaceDetectXMLFile(f'No {FACE_DETECT_XML_FILE}')

self.face_cascade = cv.CascadeClassifier(FACE_DETECT_XML_FILE)

self._is_enable_face_detect = False

if not os.path.exists(SNAPSHOT_IMAGE_FOLDER):

raise ErrorNoImageDir(f'{SNAPSHOT_IMAGE_FOLDER} does not exists')

self.is_snapshot = False

self._command_semaphore = threading.Semaphore(1)

self._command_thread = None

self.send_command('command')

self.send_command('streamon')

self.set_speed(self.speed)

def receive_response(self, stop_event):

while not stop_event.is_set():

try:

self.response, ip = self.socket.recvfrom(3000)

logger.info({'action': 'receive_response',

'response': self.response})

except socket.error as ex:

logger.error({'action': 'receive_response',

'ex': ex})

break

def __dell__(self):

self.stop()

def stop(self):

self.stop_event.set()

retry = 0

while self._response_thread.is_alive():

time.sleep(0.3)

if retry > 30:

break

retry += 1

self.socket.close()

import signal

os.kill(self.proc.pid, signal.CTRL_C_EVENT)

def send_command(self, command, blocking=True):

self._command_thread = threading.Thread(

target=self._send_command,

args=(command, blocking,))

self._command_thread.start()

def _send_command(self, command, blocking=True):

is_acquire = self._command_semaphore.acquire(blocking=blocking)

if is_acquire:

with contextlib.ExitStack() as stack:

stack.callback(self._command_semaphore.release)

logger.info({'action': 'send_command', 'command': command})

self.socket.sendto(command.encode('utf-8'), self.drone_address)

retry = 0

while self.response is None:

time.sleep(0.3)

if retry > 3:

break

retry += 1

if self.response is None:

response = None

else:

response = self.response.decode('utf-8')

self.response = None

return response

# Take Off Command

def takeoff(self):

self.send_command('takeoff')

# Landing Command

def land(self):

self.send_command('land')

# Move Command

def move(self, direction, distance):

distance = float(distance)

if self.is_imperial:

distance = int(round(distance * 30.48))

else:

distance = int(round(distance * 100))

return self.send_command(f'{direction} {distance}')

# Go Up Command

def up(self, distance=DEFAULT_DISTANCE):

return self.move('up', distance)

# Go down Command

def down(self, distance=DEFAULT_DISTANCE):

return self.move('down', distance)

# Go Left Command

def left(self, distance=DEFAULT_DISTANCE):

return self.move('left', distance)

# Go Right Command

def right(self, distance=DEFAULT_DISTANCE):

return self.move('right', distance)

# Go Forward Command

def forward(self, distance=DEFAULT_DISTANCE):

return self.move('forward', distance)

# Go Back Command

def back(self, distance=DEFAULT_DISTANCE):

return self.move('back', distance)

# Drone Turn Right Command

def clockwise(self, degree=DEFAULT_DEGREE):

return self.send_command(f'cw {degree}')

# Drone Turn Left Command

def counter_clockwise(self, degree=DEFAULT_DEGREE):

return self.send_command(f'ccw {degree}')

# Drone Flip Front Command
```

## speed based detection 2km , 5km 
