---
layout: post
title:  "PHP Lambdas And Closures"
date:   2018-02-04 16:19:24 -0500
categories: jekyll update
---

Before we learn about Lambdas and Closures we must first learn about anonymous functions. 

Anonymous function.
An anonymous function is a function with no name. 
For example:

{% highlight php %}
<?php

function() { // function with no name is called anonymous function
	return (1 + 2);
}

?>
{% endhighlight %}

What are Lambdas and why do we need them?

Lambdas are anonymous functions (function with no name) that can be assigned to a variable or that can be passed as an argument to another function. The usefulness of lambda will be realized when you need a small piece of function that will be run one in a while or just once. Instead of writing the function in global scope or including it as part of your main program you can toss around few lines of code when needed to a variable or another function. Also when you pass the function as an argument to another function during the function call you can change the argument (the anonymous function) making the function itself dynamic.

example 1:

{% highlight php %}
<?php

  $sum = function() { // assign a function to a variable
    	return (1 + 2);
  };

  echo $sum(); // call the variable as a function

?>
{% endhighlight %}

output: 3

example 2:

{% highlight php %}
<?php

     function sum($val){
     	echo $val();
     }

     sum(function () { return 2 + 3; }); // pass function as an arguement to another function
?>
{% endhighlight %}
output: 5

What are closures and why do we need them?

Closures are the same as lambdas with an additional feature that is, it can access variables outside its scope.
They are useful in PHP callback functions like array_map, array_filter, array_walk etc.

example1:

{% highlight php %}
<?php

  $a = 10;
  $b = 20;

  $sum = function () use ($a,$b) {  // assigning a function to a variable as well as use $a, $b which are out its scope
  	return ($a  = $a + $b); // $a, $b are only copies of $a, $b declared outside the function
  };

  echo $sum(); // The output will be 30

  echo $a; // the output will be 10 as the closure only works on the copies of the variables outside its scope

?>
{% endhighlight %}

If we have to modify the global variables $a, $b thn we have to use '&' symbol to create reference to them as shown below. Also we can observe here that we have passed the function as an arguement to another function.
example2:

{% highlight php %}
<?php

     $a = 10;
     $b = 20;
     function sum($val){
     	echo $val(); // output will be 30
     }

     sum(function () use(&$a,&$b) { return ($a = $a + $b); }); // pass function as an arguement to the function sum()

     echo $a; // $a is now modified and is equal to 30
?>
{% endhighlight %}

Lets look at a practical application of closures in PHP.

example3:

{% highlight php %}
<?php

    // find the square of elements of an array
    function square($val){
    	return $val *$val;
    }
    
    $a = range(1,5);
    $result = array_map("square", $a);
    print_r($result);
?>
{% endhighlight %}

output: Array ( [0] => 1 [1] => 4 [2] => 9 [3] => 16 [4] => 25 )

We thus conclude about Lambdas and Closures in PHP.