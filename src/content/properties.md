I cannot possibly express enough how annoying the typical Java boilerplate of setter and getter methods is. Why on Earth would I be fine with compusively wrapping fields that are effectively public in effectively decorative methods that add nothing of value to the actual functionality of the program. Of course, it is more rational when the mutator actually performs some action other than just assigning a new value to the field, or when the value should be read but not written to externally. Despite that, the fact that this has been the status quo for so long even in the trivial scenarios is honestly just laughable compared to the simplicity and cleanliness of C# properties.

```java
public class Example {
    private int data;

    public int getData() {
        return data;
    }

    public void setData(int data) {
        this.data = data;
    }
}
```

```c#
public class Example
{
    public int Data { get; set; }
}
```

This is an obviously substantial simplification in the class definition. In usage, the different is also notable:

```java
Example e1 = new Example();
e1.setData(50);

Example e2 = new Example();
e2.setData(e1.getData());
```

```c#
Example e1 = new Example();
e1.Data = 50;

Example e2 = new Example();
e2.Data = e1.Data;
```

This particular example has lesser benefit of course but in more complex usage it can become significant.

To unfamilar developers properties can seem unusual (especially to those that are complicit to the lack of operator overloading in Java), as though the code was lying about what it was doing. On first glance it may appear the code is simply reading/writing a location in memory directly without any side-effects, but it might not be. Though that in itself is the entire point of properties, they are supposed to appear as though they have semantics similar to fields. It could be argued that what seems like field access should always be field access (and should be side effect/exception free), but this is just an interpretation, and the fear of some unexpected side-effect generally subsides quickly as one acclimates to using properties. That, common sense, and proper documentation allows for trivial lookups of the validation properties perform by simply hovering over the name in any typical IDE.

That in itself provides many benefits, such as allowing computed properties to exist. Think an mathematical Angle class, with multiple properties in different units, but all stored using one field. This can also be changed freely by the implementor without causing a breaking change like direct field access would (which is a major reason they are usually not exposed directly in Java).

While in general properties are a potential vector for abuse of the language, this is consistent with literally every other language feature that involves identifiers (and also operator overloading), and is not an excuse to avoid properties all-together.
