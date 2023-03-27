
# Contents
- Architecture flow for Chingari's lite version on Aptos
	- Identifying Components
		- User Interface (UI)
		- Backend Server
		- Database:
		- Content Delivery Network (CDN)
		- Analytics Platform
	- System architecture design
	- How it Works

### Architecture flow for Chingari's lite version on Aptos:

The system architecture for Chingari's lite version on Aptos should be designed in a way that allows it to scale easily as more users join the platform. It should also be secure, reliable, and efficient to provide a good user experience. Here's an example of how this could be achieved:

#### 1. Identifying Components: 
The following elements will be present in the Chingari on Aptos lite version:


- **User Interface (UI)**: This is where most user interactions with the application will take place.It will have interactive aspects including a news feed, video streaming, and other functions.


- **Backend Server**: This one will deal with user queries and deliver data to the user interface.Moreover, it will manage authentication and store user data.


- **Database**: This will keep track of every user's information, including profiles, video metadata, and content metadata.


- **Content Delivery Network (CDN)**: This will be in charge of rapidly and effectively getting content to users.To make sure that frequently accessed content is available, caching will be used. 

- **Analytics Platform**: This would help Chingari improve its offerings by giving it insights into user behaviour and usage patterns. It will monitor user behaviour in real time and provide information on views, likes, comments, and shares. 


#### System architecture design:


Chingari's Aptos lite version's system architecture ought to be created in a way that makes it simple to grow as new users sign up for the service.
To offer a positive user experience, it should also be safe, dependable, and effective.
Here is an illustration of how this might be accomplished:


-  React Native will be used to create the UI, ensuring a responsive design that works on a variety of platforms and devices.

- Golang will be the backend server's main programming language, allowing it to process requests rapidly and effectively. To communicate with the Interface and database, it will use a RESTful API.

- User information and content metadata will be stored in the database using MongoDB. In order to ensure scalability and redundancy, a sharded cluster will be used. 

-  Analytics Platform: This would help Chingari improve its offerings by giving it insights into user activity and usage patterns. It will monitor user activity in real time and provide information on views, likes, comments, and shares. 


#### 3.  How it Works: 

After everything is set up, it can all work together without any issues to give users of Chingari's lite edition on Aptos the best possible experience.
This is how it goes:

- When a user starts the app, they will see a new feed populated with content from many sources, including user-generated content and curated content. The analytics platform tracks their interactions with this feed as they scroll through it, such as likes and dislikes, so that Chingari may learn more about their preferences over time.

- When users click on a video, it is instantly delivered over the CDN, allowing them to begin watching without any pauses or buffering problems. HLS or MPEG-DASH streaming will be used by the video player to ensure a fluid viewing experience on various devices. 

- The UI uses the RESTful API to make queries to the backend server whenever a user interacts with the app (such as by giving it a like or remark). The server will review the request, make the necessary changes to the database, and then provide the UI a reply.

- The backend server handles user authentication while storing all user data and content information safely in MongoDB. All data will be encrypted both in transit and at rest because protecting user privacy is a high priority.

- Chingari may leverage the analytics platform's real-time data on user activity to improve its offerings, such as personalised suggestions and targeted advertising.


Overall, Chingari's lite version on Aptos is built with a scalable, dependable, and effective architecture flow in mind. 

