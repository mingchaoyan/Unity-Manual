# Attributes
特性是一种放在类前，属性前或者函数前标记，用来指明特定的行为。比如HideInInspector特性加在一个属性上来避免这个熟悉在inspector view中显示出来（即使这个属性是public的）。在JavaScript中，特性使用@标记，而在C#中特性处于方括号内。

Unity在Script refernce中提供了很多特性。同时.NET也提供了一些在Unity代码中非常有用的特性。

注意：.NET库中的ThreadStatic特性，不要使用，因为这将引起Crash
