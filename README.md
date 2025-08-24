I am a flutter developer and when i write code i face many comments on my PR by reviewer....
So i am very worried about it...
So i wants you to write a detailed blog on how to get less comments on PR of flutter.

Here are some suggestion for developers to follow....
In Flutter (and Dart), instance variables (fields) are generally declared before the constructor in a class.
A typical and recommended order in class definitions is:
Declare all instance variables (fields) first.
Then define constructors (including `const`, factory, named constructors).
Then methods (including lifecycle methods like `initState` in `State` classes).
Then build method (for widgets).
Then private/helper methods.

In Dart (and Flutter), the best practice when defining variables in a constructor with named parameters is:
Place `super.key` first (if the class extends a widget like StatelessWidget or StatefulWidget).
Put all `required` parameters next.
Then optional parameters with default values.
Finally, optional parameters without default values.

Example : 

MyClass({
  super.key,                     // 1. Key parameter first for widgets
  required this.borderColor,     // 2. Required parameters next
  required this.day,
  required this.displayDate,
  required this.displayDateSelected,
  required this.monthType,
  this.backgroundColor = Colors.white,  // 3. Optional with default values
  this.events,                           // 4. Optional without default value
});


So, in same way list all the guidelines and standard that a senior flutter develoer must be follow while writing code so that his code must be of industry standards....
Please include everthing of flutter concept and give suporting example also.
I want end to end content of blog.
