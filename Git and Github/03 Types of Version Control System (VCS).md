
### 1.  Local Version Control System (VCS)
- Contains the Version Database located on your computer
- Every file change is stored as a patch 
- Every patch set contains only the changes made to the file since its last version

![[local.png]]

#### Problems:-
- Since , stored locally collaboration with other developer or a team is not possible 
- If anything happens to local database , all the patches would be lost
- If anything happens to single version , alll the changess made after that version would be lost

### 2. Centralized Version Control System
- Contains a single server that contains all the file versions
- Allows multiple clients to simultaneously access files on the server
- Allows to pull files to their local computer or push onto server from their local computer
- Administrator have control over who can co what 
- Allows for easy collaboration with other developer or a team

![[centralized.png]]

#### Problems:-
- Single point of failure 
- As everything is stored on the centralized server. If something were to happen to that server, nobody can save their versioned changes, pull files or collaborate at all.
- If the central database became corrupted, and backups haven't been kept, you lose the entire history of the project except whatever single snapshots people happen to have on their local machines.

### 3. Distributed Version Control System
- Clients don’t just check out the latest snapshot of the files from the server, they fully mirror the repository, including its full history
- Everyone collaborating on a project owns a local copy of the whole project, i.e. owns their own local database with their own complete history
- If the server becomes unavailable or dies, any of the client repositories can send a copy of the project's version to any other client or back onto the server when it becomes available
- It is enough that one client contains a correct copy which can then easily be further distributed.
![[distributed.png]]

#### Example :-
Git is the most well-known example of distributed version control systems


