Download Link: https://assignmentchef.com/product/solved-cs0445-project5-trees-solved
<br>



In this project, you will be dealing with a tree data structure that can represent <strong>mathematical expressions.</strong> Don’t worry, there’s no parsing this time, and the evaluation is far easier!

Starting point

<a href="/teaching/classes/cs0445/projects/cs0445_proj5_materials.zip">Download and extract these materials.</a> Contained are:

<ul>

 <li>Expression.java, <strong>the file you will modify.</strong></li>

 <li>ExpressionError.java, just an exception type.</li>

 <li>Driver.java, which is used to test Expression.

  <ul>

   <li>I’ve given you a starting point, but <strong>you should expand upon this and add more tests!</strong></li>

  </ul></li>

</ul>

To compile and run, do:

javac *.javajava Driver

You’ll see that it prints out a bunch of 0s and &lt;not implemented&gt;s. You need to fix that &#x1f642;

<h2>Expression trees</h2>

Like I showed in class, trees come up a lot in representing languages, such as math and programming languages.

The Expression class represents a <strong>node</strong> in an expression tree. Each instance of Expression can be one of three things:

<ul>

 <li>a <strong>Number</strong>

  <ul>

   <li>in which case its _value is a string representation of the value.</li>

   <li>you can use getNumberValue() to easily convert that string to a double.</li>

  </ul></li>

 <li>a <strong>Variable</strong> name

  <ul>

   <li>in which case its _value is the variable’s name.</li>

  </ul></li>

 <li>an <strong>Operator</strong>

  <ul>

   <li>in which case its _value is one of these operators: “+”, “-“, “*”, “/”, or “^”</li>

   <li>also, <strong>_left</strong><strong> and </strong><strong>_right</strong><strong> are its children</strong> – the operands to that operator.</li>

  </ul></li>

</ul>

There are no “bracket” nodes; order of operations is entirely determined by the tree’s structure.

Here are some examples of mathematical expressions and the trees which represent them:

Compare the last two trees. You can think of parentheses as saying, “force this part of the expression to be a sub-tree.”

<h2>Your task</h2>

Open Expression.java and look through it. There are already some methods written, but there are several stubbed-out ones with TODO inside them.

Each method gives you practice writing very common kinds of tree algorithms: <strong>visiting</strong> all the nodes in a tree; <strong>searching</strong> through a tree; creating a <strong>new tree</strong> which is a modification of an old one; and <strong>building a tree from scratch.</strong>

The next section documents some methods I wrote for you that will be helpful in writing these.

<h3>String toString()</h3>

<ul>

 <li>returns a human-readable <strong>infix</strong> string representation of this expression tree.</li>

 <li><strong>for numbers:</strong> return the string representation of its value.</li>

 <li><strong>for variables:</strong> return the variable name (the _value member).</li>

 <li><strong>for operators:</strong> return a string of the form “(left op right)”, where:

  <ul>

   <li>left is the string representation of the _left member</li>

   <li>op is this operator (the _value member)</li>

   <li>right is the string representation of the _right member</li>

  </ul></li>

 <li>the result will have lots of parentheses. that’s correct &#x1f642;</li>

</ul>

<h3>String toPostfix()</h3>

<ul>

 <li>returns a human-readable <strong>postfix</strong> string representation of this expression tree.</li>

 <li>this should be a very slight modification of toString().</li>

 <li><em>don’t forget to call </em><em>toPostfix()</em><em> recursively.</em></li>

 <li>there should be no parentheses in the output.</li>

</ul>

<h3>double evaluate(Map&lt;String, Double&gt; variables)</h3>

<ul>

 <li>given a set of variables, evaluate the expression tree and return the result.</li>

 <li><strong>for numbers:</strong> return the numerical value of the node (getNumberValue()).</li>

 <li><strong>for variables:</strong>

  <ul>

   <li>check if the variable’s name (_value) exists in the set of variables, using variables.containsKey()</li>

   <li>if not, throw an ExpressionError with a descriptive error message.</li>

   <li>if so, return the value from variables.get().</li>

   <li><a href="https://docs.oracle.com/javase/8/docs/api/java/util/Map.html">Here is the documentation for Map</a>. You can find the docs for containsKey() and get() there.</li>

  </ul></li>

 <li><strong>for operators:</strong>

  <ul>

   <li>recursively evaluate the _left and _right children, using the same variables argument to them.</li>

   <li>based on this operator (_value), perform the right calculation on those two values and return the result.</li>

  </ul></li>

</ul>

<h3>Expression reciprocal()</h3>

<ul>

 <li>returns a <strong>completely new</strong> expression tree that is the reciprocal of this one.</li>

 <li>you will not be making recursive calls to reciprocal(), but <strong>you should use </strong><strong>clone()</strong><strong> where appropriate.</strong></li>

 <li>there are 3 cases:

  <ul>

   <li><strong>numbers:</strong> return a <strong>new</strong> number node whose value is the reciprocal.</li>

   <li><strong>division:</strong> return a <strong>new</strong> division node whose children are cloned and swapped.</li>

   <li><strong>everything else:</strong> return a <strong>new</strong> division node whose children are 1 and a clone of this.</li>

  </ul></li>

</ul>

<h3>Set&lt;String&gt; getVariables()</h3>

<ul>

 <li>returns a set containing all the unique variable names which appear in the expression tree.</li>

 <li>the code I gave already creates the Set&lt;String&gt; for you.

  <ul>

   <li>it has an .add() method that you can use to add Strings to it.</li>

  </ul></li>

 <li>you will have to write a <strong>private recursive method</strong> to actually find the variables, and have this call that one.

  <ul>

   <li>you will pass that variables set as an argument to it.</li>

   <li>think about how each kind of node will change the set (if at all).</li>

  </ul></li>

</ul>

<h3>static Expression geometricMean(double[] numbers)</h3>

You may not use quickParse() to implement this method. Sorry &#x1f609;

<ul>

 <li>creates an Expression that represents the <a href="https://www.mathsisfun.com/numbers/geometric-mean.html">geometric mean</a> of the array of numbers given as an argument.</li>

 <li>the resulting Expression should be of the form:

  <ul>

   <li>(numbers[0] * numbers[1] * … * numbers[n-1]) ^ (1 / n)</li>

   <li>where n is the length of the array.</li>

   <li>(it’s OK to assume that the array is always at least 1 item long.)</li>

  </ul></li>

 <li>use the Number(), Operator(), and reciprocal() methods to create the expression.</li>

 <li>making the chain of multiplications can be done iteratively or recursively.

  <ul>

   <li>it’s a fun little puzzle &#x1f642;</li>

  </ul></li>

</ul>

<h2>The methods I wrote for you</h2>

<ul>

 <li>Number(double)

  <ul>

   <li>makes a new Expression node containing a number.</li>

   <li>e.g. Expression e = Number(3.1415);</li>

  </ul></li>

 <li>Variable(String)

  <ul>

   <li>makes a new Expression node containing a variable name.</li>

   <li>e.g. Expression e = Variable(“num_people”);</li>

  </ul></li>

 <li>Operator(Expression, String, Expression)

  <ul>

   <li>makes a new Expression node containing an operator, and which points to two children.</li>

   <li>e.g. Expression e = Operator(Number(4), “/”, Number(5)); for the expression 4 / 5.</li>

  </ul></li>

 <li>quickParse(String)

  <ul>

   <li>parses a string into a tree of Expression nodes. supports +-*/^ and regular parentheses ().</li>

   <li>e.g. Expression complex = Expression.quickParse(“1 / (5*x^2 + 3*x – 9)”);</li>

  </ul></li>

</ul>

quickParse has very little error checking and will likely crash or give weird results with erroneous input. But it’s really there for testing purposes, so just give it valid expressions please &#x1f642;

<ul>

 <li>isOperator(), isNumber(), isVariable()

  <ul>

   <li>return booleans saying what type of node this is.</li>

   <li>e.g. if(expr.isOperator()) …</li>

  </ul></li>

 <li>getNumberValue()

  <ul>

   <li>for number nodes, parses the _value member into a double.</li>

   <li>for operator and variable nodes, will probably crash. (that’s why it’s private.)</li>

  </ul></li>

 <li>clone()

  <ul>

   <li>makes a complete copy of an expression, recursively.</li>

   <li><strong>have a look at how this method is implemented!</strong></li>

  </ul></li>

</ul>

<h2>Testing</h2>

Driver.java has a small amount of code in it to test your Expression methods. However it does pretty minimal testing. Like it tells you, <strong>TEST MORE THOROUGHLY!!!</strong> Use Expression.quickParse() to easily create test cases.

Here are the outputs I got from my implementation:

toString:        (((4.0 * x) + (y / 9.0)) + 12.0)toPostfix:       4.0 x * y 9.0 / + 12.0 +evaluate:        55.0reciprocal:      (1.0 / (((4.0 * x) + (y / 9.0)) + 12.0))reciprocal(num): 0.14285714285714285reciprocal(div): (10.0 / x)getVariables:    [x, y]geometricMean:   (((((4.0 * 9.0) * 3.0) * 7.0) * 6.0) ^ 0.2)it evalutes to:  5.3868466094227525

<h2>Extra Credit [+10]</h2>

<h3>String toNiceString()</h3>

<ul>

 <li>Turns the expression into a nice string. &#x1f609;</li>

 <li>This is like toString() but it will <strong>only put parentheses where needed.</strong></li>

 <li>Hints:

  <ul>

   <li>Don’t forget to call toNiceString() recursively.</li>

   <li>Decide whether to put parentheses around <em>each</em> of an operator’s <em>children.</em></li>

   <li>Think about when you, as a human, need to put parentheses in an expression. What is the rule there? What does it have to do with?</li>

  </ul></li>

</ul>

Done correctly, if you just have toString() call this method, the relevant lines of the above output would now look like:

toString:        4.0 * x + y / 9.0 + 12.0reciprocal:      1.0 / (4.0 * x + y / 9.0 + 12.0)reciprocal(div): 10.0 / xgeometricMean:   (4.0 * 9.0 * 3.0 * 7.0 * 6.0) ^ 0.