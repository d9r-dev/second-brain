* Records are always final
* you cannot explicitly add fields to Records
* unreachable code will not compile
* static void setDefault(Locale.Category category, Locale newLocale): Sets the default locale for the specified Category for this instance of the Java Virtual Machine.  
* Locale.Category is an enum for locale categories with two values - DISPLAY and FORMAT. These locale categories are used to get/set the default locale for the specific functionality represented by the category.
* But a floating point division with 0 (i.e. dividing a float or double value with 0 or 0.0) will result in Float.POSITIVE_INFINITY or Float.NEGATIVE_INFINITY (or Double.POSITIVE_INFINITY or Double.NEGATIVE_INFINITY, if the operands are double instead of float).
* Optional.of method throws NullPointerException if you try to create an Optional with a null value. If you expect the argument to be null, you should use Optional.ofNullable method, which returns an empty Optional if the argument is null.
* Once you have the service providers, you can iterate through them using an enhanced for loop (ServiceLoader implements Iterable and so, it can be used in an enhanced for loop directly) 

Remember the following 4 points about Path.getName() method :  
  
1. Indices for path names start from 0.  
2. Root (i.e. c:\) is not included in path names.  
3. \ is NOT a part of a path name.  
4. If you pass a negative index or a value greater than or equal to the number of elements, or this path has zero name elements, java.lang.IllegalArgumentException is thrown. It DOES NOT return null.

= can be chained
Comparator does have a reversed() method.

Always remember: Instance methods are overridden and variables (and static methods) are hidden. Which instance method is invoked depends on the class of the actual object, while which field (and static method) is accessed depends on the class of the variable.