
# cs1302-ce15 Genericize is stil a Real Word

> And yet to me, what is this quintessence of dust? 
> **--Hamlet, _Hamlet_ by William Shakespeare**

This class exercise continues coverage of generic methods, including some checkpoints related to
upper bounds. 
It also provides a small demonstration of branching and merging using Git.

## References and Prerequisites

* Basic knowledge of Java Generics.
* [Oracle: Generic Methods](https://docs.oracle.com/javase/tutorial/extra/generics/methods.html)
* [Oracle: Bounded Type Parameters](https://docs.oracle.com/javase/tutorial/java/generics/bounded.html)

## Questions

In your notes, clearly answer the following questions. These instructions assume that you are 
logged into the Nike server. 

**NOTE:** If a step requires you to enter in a command, please provide in your notes the full 
command that you typed to make the related action happen. If context is necessary (e.g., the 
command depends on your present working directory), then please note that context as well.

### Getting Started

1. Use Git to clone the repository for this exercise onto Nike into a subdirectory called `cs1302-ce15`:

   ```
   $ git clone --depth 1 https://github.com/cs1302uga/cs1302-ce15.git
   ```

1. Change into the `cs1302-ce15` directory that was just created and look around. There should be
   multiple Java files contained within the directory structure. To see a listing of all of the 
   files under the `src` subdirectory, use the `find` command as follows:
   
   ```
   $ find src
   ```

### Exercise Steps

1. Examine the generic static `checkNull` method in the `cs1302.Utility` 
   class. 

   1. What is the name of the generic type parameter?
   1. What is the minimum number of parameters that can be used 
      when invoking this method?
      Provide an example.
   1. What kind of references are allowed for the variadic 
      parameter of this method? 
      Be descriptive.
   
1. Create and checkout a branch called `driver` to perform
   the work related to this checkpoint. You can do this using
   the following command:
   
   ```
   $ git checkout -b driver
   ```
   
1. Confirm that you are on the desired branch using `git status` and/or
   `git branch`.
   
1. **NOTE:** When checking the next step, your instructor or PLA will look 
   at the list of things you tried. You should have a log entry for each. 
   They will not sign off on this checkpoint if you do 
   not do the steps above for each and every error as 
   _errors are expected_ if you perform the steps correctly.

1. **Read the previous step.**
   Now, write and document a `Driver` class in the `cs1302.ce15` package. 
   The `main` method should demonstrate that your `checkNull` method 
   only accepts references that all the same type. Since Java
   allows for subtype assignment to parent variables, also check that
   you can supply references to obects that are children of the type 
   you specifiy. You may make use of the `Shape`, `Ellipse`, and `Circle` 
   classes that are in the same package. 
   
   Try different statements. **If you do this properly, then 
   compile-time errors are expected** when calls to `checkNull`
   violate the conditions your earlier modifications adopted. 
   In other words, the changes you made are supposed to prevent 
   the programmer from using your method a particular way. 
   If you encounter any compilation errors:
   
   1. Look at the first error reported by `javac`;
   1. Write down the entire statement that caused the error.
   1. Write the error message down in your notes;
   1. In your notes, denote whether or not this error is expected;

	  1. If **yes**, then keep the line in your code but comment it 
	     out, and include the reason why it's expected in your notes.
	  1. If **no**, then fix the error in the code.
	  
   1. Recompile;
   1. Stage and commit your changes using Git; and
   1. Repeat as needed. 

1. Now that everything on this branch compiles, ensure that all changes 
   in the current branch have been staged and committed, then 
   checkout the `master` branch.
   
1. Merge changes from the `driver` branch into the current branch
   (`master`).

1. View the condensed, graphical version of your Git log using `git adog`
   What is the entire line of output for the most recent entry produced
   by the `git adog` command from the previous class exercise?

**CHECKPOINT**

1. Delete the code inside of your `Driver` class's `main` method, then commit this change to your 
   local copy of the exercise repository. Don't worry, you can also checkout what you had before because
   you committed your earlier changes while working on the previous checkpoint.
   
1. Add the following code to your `Driver` class's `main` method, make sure it compiles, then 
   commit this change to your local copy of the exercise repository.
   
   ```java
   Circle[] circles = new Circle[] {
	   new Circle(5.0),
	   new Circle(3.3),
	   new Circle(4.1),
	   new Circle(1.2)
   };
   ```
   
   We will come back to this code in a few steps.

1. You may have noticed `cs1302-ce15.jar` in the `lib` subdirectory. In your notes, write down the command
   to list the contents as well as its output. The API documentation for the compiled code contained in this
   file can be found [here](http://cobweb.cs.uga.edu/~mec/cs1302/cs1302-ce15-api/).
   
1. Examine the [`ArrayUtility.sort(T[])`](http://cobweb.cs.uga.edu/~mec/cs1302/cs1302-ce15-api/cs1302/util/ArrayUtility.html#sort-T:A-)
   method overload in the `cs1302.util.ArrayUtility` API documentation. Actually read the documentation.
   In your notes, answer the following:
   
   1. What is the complete signature for this method?
   1. What is the datatype and role of each method parameter?
   1. Suppose you want to parameterize `T` (i.e., replace it with some specific type). What requirement must that type satisfy?
   1. What other questions do you have related to this method?
   
1. **[TRICKY]** _Read this entire step, including substeps, very carefully before attempting it._ 
   Modify the source code for the `Circle` class so that `Circle` satisfies the requirement to 
   replace `T` when calling `ArrayUtility.sort`. Your modification should result in the induced
   ordering for `Circle` objects to be based on their radius values, in ascending (increasing)
   order. 
   
   * As you attempt this, remember that the goal is to allow the `T` to be replaced with `Circle`
     when calling the `sort` method. This means that you can test whether or not you've done this
     correctly by appropriately calling `ArrayUtility.sort` on the array referred to by `circles`
     in your `Driver` class's `main` method. You will know that you satisfy the type requirement
     when the `Driver` class compiles.
	 
   * Once you are sure that the type requirement is being satisfied, you can test that your
	 induced ordering is correct by looping through the array referred to by `circles` and 
	 printing out the return value of `getRadius()`. This should be done after your call to `sort`.
	 
1. Commit the changes to your local copy of the exercise repository.
   Be sure to include a good log message.

**CHECKPOINT**

1. In the previous checkpoint, you were able to modify the `Circle` class so that arrays of
   circles can be sorted using `ArrayUtility.sort`. However, consider what would happen if
   you now wanted to sort according to a different ordering (e.g., area or perimeter). You
   would have to edit `Circle.java` again! This is where the other overload for `sort` 
   comes into play. Examine the 
   [`ArrayUtility.sort(T[], Comparator<T>)`](http://cobweb.cs.uga.edu/~mec/cs1302/cs1302-ce15-api/cs1302/util/ArrayUtility.html#sort-T:A-java.util.Comparator-)
   method overload in the `cs1302.util.ArrayUtility` API documentation.
   Actually read the documentation.
   In your notes, answer the following:
   
   1. What is the complete signature for this method?
   1. What is the datatype and role of each method parameter?
   1. Suppose you want to parameterize `T` (i.e., replace it with some specific type). What requirement must that type satisfy?
   1. What other questions do you have related to this method?

1. **[TRICKY]** _Read this entire step, including substeps, very carefully before attempting it._ 
   Create a class called `AreaComparator` in the `cs1302.ce15` package that correctly
   implements the comparator required for the overloaded `ArrayUtility.sort` when parameterized 
   to operate on arrays of type `Circle`. The induced ordering for `Circle` objects here should
   be based on their area values, in descending (decreasing) order. 

   * As you attempt this, remember that the goal is to allow you to sort arrays of circles using
     `ArrayUtility.sort` by some other ordering criteria **without** modifying `Circle.java`. This
	 involved creating a proper class for the comparator, then calling the `sort` method with
	 and object of that comparator class. You can test whether or not the comparator class is
	 snytactically correct by calling the overloaded `ArrayUtility.sort` on the array referred to 
	 by `circles` in your `Driver` class's `main` method. You will know that it is syntactically correct 
     	when the `Driver` class compiles.
	 
   * Once you are sure that comparator class is syntactially correct, then you can test that your
	 comparator's induced ordering is correct by looping through the array referred to by `circles` and 
	 printing out the return value of `getArea()`. This should be done after your call to `sort`.

1. Commit the changes to your local copy of the exercise repository.
   Be sure to include a good log message.

**CHECKPOINT**

<hr/>

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc-nd/4.0/)

<small>
Copyright &copy; Michael E. Cotterell, Brad Barnes, and the University of Georgia.
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a> to students and the public.
The content and opinions expressed on this Web page do not necessarily reflect the views of nor are they endorsed by the University of Georgia or the University System of Georgia.
</small>
