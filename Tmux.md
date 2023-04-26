`ctrl + b`  --->  to perform any task in the tmux can also be denoted as `^ b`

| command | fuctions|
|--|--|
|ctrl+b   c| create new window|
|ctrl+b l| toogle between the previous and new window|
|ctrl+b ,|change the name of the current window|
|ctrl+b 0 to 9| select windows 0 to 9|
|ctrl+b q| briefly shows pane indexes|
|ctrl+b q 0 to 9| to move to the indexed pannel|
|ctrl+b w| show windows tree|
|ctrl+b n/p| select the next/previous window|
|ctrl+b f| search window from prompt window|
|ctrl+b %| split pane into two, left and right|
|ctrl+b ""| split pane into two, top and bottom|
|ctrl+b spacebar[⎵]|arrange the panes|
|ctrl+b  ↑↓→←| to move pane up, down, left and right|
|ctrl+b o| to toggle between pane|
|ctrl+b ctrl+↑/ctrl+↓| to resize the pane up or down|
|ctrl+b ctrk+→/ctrl+←| to resize pane left or right|
|ctrl+b !| break pane into new window|
|ctrl+b z| toogle minimize/maximize the current pane|
|ctrl+b ctrl+z| suspend the current client|
|ctrl+b  x| kill the current pane|
|ctrk+b &| kill the current window|
|ctrl+b d| ditach the current clielt|
|ctrl+b s| check different session|

```
	tmux attach --> opens to last sessions
	tmux ls ---> shows the different sessions
	tmux a -t[name or index] ---> select the session with given index or namw
	tmux remane-session NEW_NAME ---> remane the curent session
```


