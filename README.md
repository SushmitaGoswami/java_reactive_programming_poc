# java_reactive_programming_poc

## What is the problem with the exiting thread per request model?
Here, the calling service creates a separate thread for each request, but the calling thread will have to wait for the caller service to return. So, this is a blocking IO.


## IO Models
There are 4 different types of IO models.

1. **Synchronous Blocking IO** : Here calling service waits until the caller returns.

2. **Asynchronous Blocking IO** : The calling service delegates the call to a third party agent which waits for the caller to return and during this time, the calling service wouldn't
wait for the caller service.

3. **Non Blocking w/o agent IO** : Here the calling service will make an async call to the caller service. It's the resposibility of the caller service to notify the result to the 
calling service. So, there are 2 issues with this approach. One is there is an involvement in low level programming as the OS call is involved. Another one is there can be many nesting 
callback in the source service code as there may be multiple calls to multiple services dependening on the logic.

4. Non Blocking with agent IO : Here the calling service will delegate the call to a third party agent and it's the job of that agent to establish a async call to the caller service.
So, no callback would have to set up at calling service and it will free up some resource consumption at the calling service end.



## So what is reactive programming?
It is basically an agent providing IO as a service. Agent will be receiving unbounded request to process an IO call from no of services. It is implementation of reactive streaming
specification. It follows observer pattern or publisher and subscriber or declarative style of programming. It is a subset of asynchronous or event driven programming where events happen when data flows through a predefined data
pipeline. It reduces the complexity of imperative style of programming where lots of interdependant nested call is involved. It breaks down a problem into a set of logical easily 
representable problem statement which makes the code much more readable along with the asynchronous processing capability.

## Reactive Specification Implementation

1. Akka.
2. rxJava2
3. Reactor

## What is the flow?
1. First subscriber will call the subscribe method on a publisher object.
2. Publisher will then call the onSubscribe method of the subscriber and will return a subscription object along with this to continue with the further process.
3. Subscriber will call the request for some objects to the publisher. Publisher will call the onNext method of the subscriber and return the Object.
4. Whenever, the subscriber is no longer interested to receive any item from the producer, it will call the onComplete method to close the connection.
5. Whenever, any error occurrs while producing the data at the producer end, producer will call the onError method of the subscriber and no more data will be pushed to 
the subscriber afterwards.

## Mono & Flux
Mono : Producer can generate 0 or 1 element.
Flux : Subscriber generate 0 or n elements.

Here building data pipeline is separated from the execution. 

## Terminologies
1. FluxSink : It is used to create and emit object programmtically.
