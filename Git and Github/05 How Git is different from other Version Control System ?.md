## 1. Snapshorts,  Not Differences
- ##### Others: 
	- Most other systems store information as a list of file-based changes. These other systems think of the information they store as a set of files and the changes made to each file over time.
	-  ![[deltas.png]]
- ##### Git:
	- Git thinks of its data more like a series of snapshots of a miniature filesystem
	- With Git, every time you commit, or save the state of your project, Git basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot
	- To be efficient, if files have not changed, Git doesn’t store the file again, just a link to the previous identical file it has already stored. Git thinks about its data more like a **stream of snapshots**.
	- ![[snapshots.png]]


## 2. Nearly Every Operation Is Local

- Most operations in Git need only local files and resources to operate — generally no information is needed from another computer on your network
- You have the entire history of the project right there on your local disk, most operations seem almost instantaneous

	####  Example:-
	 To browse the history of the project, Git doesn’t need to go out to the server to get the history and display it for you — it simply reads it directly from your local database. This means you see the project history almost instantly. If you want to see the changes introduced between the current version of a file and the file a month ago, Git can look up the file a month ago and do a local difference calculation, instead of having to either ask a remote server to do it or pull an older version of the file from the remote server to do it locally.
	 

## 3. Git Has Integrity
- Everything in Git is checksummed before it is stored and is then referred to by that checksum
- This means it’s impossible to change the contents of any file or directory without Git knowing about it
- The mechanism that Git uses for this checksumming is called a SHA-1 hash
- This is a 40-character string composed of hexadecimal characters (0–9 and a–f) and 
- Calculated based on the contents of a file or directory structure in Git.
- A SHA-1 hash looks something like this:

```
24b9da6552252987aa493b52f8696cd6d3b00373
```

### 4. Git Generally Only Adds Data

- When you do actions in Git, nearly all of them only _add_ data to the Git database
- It is hard to get the system to do anything that is not undoable or to make it erase data in any way
- After you commit a snapshot into Git, it is very difficult to lose, especially if you regularly push your database to another repository





