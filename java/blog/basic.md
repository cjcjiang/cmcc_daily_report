# Basic Java Knowledge
1. Java是值传递还是引用传递？
java是值传递。C++里的引用是引用传递。
根本区别在于基本数据类型，如int。
java传int时，传的是原先int的副本。故方法内不管如何操作，都不会影响方法外的int。
C++传int的引用时，方法内操作这个引用，方法外的int也会改变。
