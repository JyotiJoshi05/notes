# Angular Notes
A framework for building client applications in HTML, CSS< Javascript/Typescript.
### Why do we need Angular?
- Provide structure to our project
- Easy to test
### Architecture of Angular Apps
- Front-end (HTML Templates and Presentation Logic)
- Back-end (Data + APIs and Business Logic)
> APIs are endpoints that are accessible via the HTTP protocol.
Angular uses some features of javascript that are not yet supported by some browsers so to fill this gap between the browser and angular framework we need polyfills file.
> Karma is a test runner for javascript code.
### Type Assertions
(message as string).charAt()
(<string> message).charAt()
> (message) => {};
### Inline Annotations
(point: {x: number}) => {}
> Components should only contain presentation logic.
### Dependency Injection
> Providing or injecting dependencies of a class to it's constructor which helps in loose coupling.
> Same instance is passed to every component when registered in Providers property - Singleton pattern
> Injectable added when we need some other service in a service. In componennts included automatically.


