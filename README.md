# MapReduce-Project-Description

The goal of this project was to make an implementation of the MapReduce framework using multithreaded programming, TCP sockets, and UDP sockets. My team and I were required to simulate a distributed system of computers running a MapReduce job by representing each "computer" as a different process. A manager process was used to discover new jobs to group and send them to workers. It was also responsible for keeping track of live workers. The workers jobs were to complete the task assigned to it by the manager

The sequence of the code was as follows:
- A job is sent to the manager's TCP server. It determines what kind of job it is (either data to group or initialization of a new worker)      and acts accordingly
-  If it is the initialization of a new worker, an acknowledgement will be sent over TCP back to the worker and that worker will marked as a    live and  ready worker by the manager
-  When the worker recieves the acknowledgment it will start sending heartbeat messages to the manager via a UDP client, which the manager      can use to keep track of a worker's status
-  If the manager recieves a new job request (will always start as map request) it will take the file that needs to be mapped and              partition the data within into tasks. Then it will send the tasks to any worker that is not completing a task at the moment
-  When a worker recieves a task it will run an executable on the data to map it. Once mapping is complete, it will send the completed task    back to the manager over TCP
-  Once all mapping jobs are complete, the manager will group like terms in the data together, and redo the same process for reducing.
-  If a worker that is working on a task ever stops sending heartbeats, the manager needs to notice this and assign that task to a              different, live worker

Below is an image from the spec that helps to explain the process:
<img width="773" alt="Screen Shot 2023-05-18 at 11 44 48 AM" src="https://github.com/omastey/MapReduce-Project-Description/assets/67980312/c4f516f8-cafc-40ce-9af7-993ca2c2829d">


This was an interesting project to work on as it required me to balance requirements over different threads and processes, rather than thinking of code as one thread.

Due to University of Michigan's academic integrity policies, I cannot attach my code, but the links to the spec is attached below!
- https://eecs485staff.github.io/p4-mapreduce/#mapreduce-server-specification
