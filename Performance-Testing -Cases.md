Performance Testing - cases
=====================
We will discuss about typical performance tests (for web applications) in this post.

### Load Testing: 
We typically test how a system behaves with a large number of users/user requests and measure response time under different scenarios. We typically generate concurrent requests from 1 or several machines using some Load testing tool (like JMeter). 

### Capacity Testing: 
Capacity testing is another variation, which will fix the maximum capacity of users the system can support. The main criteria will be the response time for all the requests falls below expected load time.

### Stress Testing: 
Stress testing is another variation, which will find how a system behaves in extreme conditions. You purposely try to break your system, using any set of extreme conditions – whether doubling the number of users, using a Server with much less memory/CPU, etc...Typically we will observe increase in response time, or the entire system get stuck or crash. We need to take mitigation per observations.

### Soak Testing: 
Soak testing is another variation, which will uncover performance problems that surface only during a long duration of time. This is important case, because at first some memory leak may not affect the system, but after a while the system may crash. Typically soak test would last hours, days and even weeks.
