This Tutorial introduces the Kafka software for queuing messages. This
will help us decouple our microservices.

This chapter covers
Using live reload at the application level for faster iterations
Sending direct messages between microservices with HTTP requests
Sending indirect messages between microservices with RabbitMQ
Choosing between using direct and indirect messages
A microservices application is composed of many microservices, each
looking after its own area of responsibility. Because each microservice by
itself is small, simple, and doesn’t do much, our microservices must
collaborate to create the complex behaviors needed to implement the feature
set for our product. To work together, our microservices need ways to
communicate. If they can’t talk to each other, then they won’t be able to
coordinate their activities, and they won’t achieve much.
In this chapter, we examine the different ways that microservices can
communicate so that they can collaborate and fulfill the higher-level
requirements of the application. In the process, we’ll also revisit Docker and
Docker Compose to set up live reload for our entire application. Moving
forward, that’s essential so that we aren’t constantly rebuilding and restarting
our application as we update our code.
We already saw in earlier chapters that HTTP requests are one way that
microservices can communicate. In this chapter, we’ll expand on using HTTP
requests for direct messaging, and we’ll also look at using RabbitMQ for
indirect messaging. Throughout the chapter, you’ll learn how to decide what
type of messaging to use for a given situation.


