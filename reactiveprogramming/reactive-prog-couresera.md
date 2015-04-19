### Reactive Programming
 
- Scalable
- Resilient
- Responsive
- Event Driven

### Event Driven

Traditional syatem are composed of multiple threads, which communicate with shared, sysnchronized state.These system are strongly coupled and hard to compose.

Now the system are composed from loosely coupled event handlers. These events can be handled asynchronously, without blocking.

### Scalable
The application is consider scalable if it expands according to its usage.

- scale up(vertical) : make usage of parallelism in multi-core system.
- scale out(horizontal) : make use of multiple server nodes.

Important for scalability is minimizing the shared mutable state.

### Resillent
Recovering from the failures quickly.Failures could be:

- software failure,
-  hardware failure
- network failure

For sytem to be resillent:

- loose coupling
- strong encapsulation of state
- pervasive supervisor hierarchies
  
### Responsive
 Should provide  rich, real-time interaction with its users even during the words and in the presence of failures.



