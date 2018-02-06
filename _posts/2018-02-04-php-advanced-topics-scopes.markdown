---
layout: post
title:  "PHP Advanced Topics- Scopes"
date:   2018-02-04 16:19:24 -0500
categories: PHP advanced
---
The purpose of this tutorial is to help understand the PHP language features better and brush up your existing knowledge. In this blog we are going to learn about scopes in PHP.

PHP Scopes

Scope refers to the lifetime of a variable in a script. In PHP the following types of scopes are available.

1.	Super Globals : They refer to the predefined variables that are always available everywhere throughout the PHP script. Example: $GLOBALS, $_SERVER, $_GET, $_POST etc.
2.	Global: A variable with global scope is accessible throughout the script and are defined outside a function or loop.
3.	The keyword ‘global’ : To access or modify a global variable inside a fuction or loop the same variable is declared inside the function or loop using the keyword  ‘global’
4.	Local: The lifetime of the variables inside a function or loop is said to be local, once the execution of the function or the loop is over, the variables used in it expires.
5. Static: To retain the life of a local variable outside of a function or loop then we should declare the variable as static.

The below code snippets demonstrates the global scope and the keyword 'global'.  

{% highlight php %}
<?php

	$a = 6;
	$b = 2; // $a, $b are Global variables

	function sum()
	{	
		echo $a + $b; // $a, $b are local variables and are NOT the same as $a, $b mentioned outside the function
	}

	sum();

?>
{% endhighlight %}

 The output will be: 
Notice: Undefined variable: b 

Notice: Undefined variable: a 

Now if you want to access the global variables $a, $b inside the function use the keyword global as below.

{% highlight php %}
<?php

	$a = 6;
	$b = 2; // $a, $b are Global variables

	function sum()
	{	
		global $a,$b;
		echo $a + $b; // $a, $b are local variables and are NOT the same as $a, $b mentioned outside the function
	}

	sum();

?>
{% endhighlight %}

The output will be 8


An example of local scope is mentioned below:

{% highlight php %}
<?php

	$a = 6;
	$b = 2; // $a, $b are Global variables

	function sum()
	{	
		$a = 3;
		$b = 7;
		$c = $a + $b;
		echo $a,"\n", $b, "\n", $c;  // $a, $b are local variables and are NOT the same as $a, $b mentioned outside the function
	}

	echo "Value of local variable'c' outside the function", $c; //$c is a local variable and will not be available outside the function hence will error with the message Undefined variable: c.

	sum();

?>
{% endhighlight %}

The output will be 3 7 10.
Undefined variable: c 

Static scope example:
The below example shows a function that counts till number 'n', we have to declare the counter variable as static otherwise everytime the function is invoked the counter variable will be reset to 0.

{% highlight php %}
<?php

    function countill($a)
    {

		static $counter = 0;
        $counter++; 
        
		
		if ($counter > $a)
		{
			
			$counter--;
			exit;
		}
		else
		{
            echo $counter;
			countill(10);
		}			
			
    }
    
	countill(10);
?>
{% endhighlight %}

The output will be: 1 2 3 4 5 6 7 8 9 10



Thus we conclude 



