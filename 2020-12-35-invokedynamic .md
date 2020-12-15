invokedynamic is a bytecode operation used to call arbitrary method within JVM. The exact method to be called and executed is unknown at a compile-time. Instead it is computed by object implementing CallSite. Thus the dynamic in invokedynamic.

CallSite objects, as any other, have to be instantiated. Boostrap Method is a method which instantiates CallSite objects.

Each invokedynamic has a known bootstrap method given as its compile-time parameter. Whenever a invokedynamic is processed for a first time, appropriate bootstrap method is invoked. As result of boostrap method execution a CallSite object is created. This CallSite object is then cached and associated by JVM to a given invokedynamic operation. From now on, whenever particular invokedynamic call is to be executed, a cached CallSite instance is used to resolve called method.

Majority of boostrap methods are not written directly by end Java programmer. However that doesn't mean they are some rare obscure mechanism. They are created by javac compiler whenever particular java statements are used within source. String concatenation or lambda expression come to mind.

For example lambda expression could be implemented as inner classes. For matter of fact, lambdas are presented to programmers 'as shorthand' to using inner classes. However actual javac implementation, for performance reasons, avoids inner classes by generating lambda code under a static method and using invokedynamic to invoke this method.

For more direct, more impressive, usage of invokedynmaic I recommend Charles Nutter blog on how he optimizes JRubby calls sites with this mechanism. While writing RubyVM is not usual Java Programmer activity it is a really an eye opener on how to appropriately use ivokedynamic.
