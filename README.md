Session Controller Center
===========================

Environment
---
Java 1.8<br>
Maven 3.5<br>

Deploy
---
cd {source code root}<br>
mvn package<br>
java -jar ./target/SessionControllerCenter-0.0.1-SNAPSHOT.jar<br>


Statement
---
Control LTE-B sessions starting and stopping.<br>
Start with home page: http://localhost:8083/
<br>
server default port = 8083<br>

Core ideas
---
1. Have simple web Front-end pages to "Start/Stop"<br>
2. Back-end handle 3 kinds of requests from Front-end:<br>
    start n sessions.<br>
    stop single sessions.<br>
    stop all active sessions.<br>
   Then send related "Start/Stop" requests to "LTE-B virtual server"<br>
3. One thread handle one session, for example, we can "Start" 7 session at same time, then 7 threads will be created to start 7 sessions<br>
4. All "Start/Stop" history would be logged.<br>
5. Validate XML format before send POST requests to  "LTE-B virtual server"
6. Loaded 3 collections Map<Integer,LTESession> startedItems, List<LTESession> startingItems, List<LTESession> failedItems in servletContext to save sessions status<br>


v1.0
---
1. Start multiple sessions.<br>
2. Stop single sessions.<br>
3. Stop all sessions<br>


v1.1 
---
changes:<br>
 1. Replace required collection with thread-safe collection. <br>
 2. Fix factory not singleton issue. <br>
 3. Delegate all session related threads to a fixed thread pool(max allowed threads is 100).<br>