# PHP Code Standards


## General Styles

* Files which are all PHP should not include a closing php tag `?>`
* PHP which is inline with HTML will include only fully formed tags `<?php` &amp; `?>`, all short tags are
prohibited
* Use __hard tabs__ `\t` for indention
* All [PHP keywords](http://php.net/manual/en/reserved.keywords.php), as well as constants `true`,`false`, and
`null` must be fully lowercase
* Lines MUST use UNIX standard line endings `\n`
* There MUST be no trailing whitespace on lines
* There MUST NOT be more than one statement per line
* Opening curly braces `{` must be preceded by a space
* Closing curly braces `}` should always be on a line by themselves
* Closing curly braces should always align with the first character of the line they open
* Code blocks contained by curly braces should have a single tab indentation to denote the block
* Class methods should always be preferred to stand alone functions  --under review
* Global variables outside of PHP defined globals (`$_SERVER`, `$_SESSION`, etc&hellip;) are prohibited.
* Comment blocks should be included for every class and method.  Class members should be commented when not obvious.
definitions should be given in the [PHPDoc Style](http://www.phpdoc.org/)
* C style comments for both single line `//` and blocks `/* */` are allowable comments, Perl style comments
`#` are prohibited
* PHP's stdClass should never be used, defined classes are the preferred object
* If a defined class is unavailable or undesirable an array should be used
* Null values are part of the PHP language, and often unavoidable.  However `null` should not be used to create a ternary state, no method or function should be defined to return an Object/Value, `false` or `null`. _[Classic](http://thedailywtf.com/articles/What_Is_Truth_0x3f_)_
* Functions that cannot return their expected result time should throw exceptions rather than returning null.

## Strings &amp; Output

* Single Quotes are preferred unless in-line variables are included in the string.

```php
$a = 'I am a constant string';
```

* Variables inline with strings should be prefaced with a `$`. For consistency, the `{$variable}` form is
prohibited.  __Variable variables are STRICTLY PROHIBITED__

```php
//Correct:
$a = "I am a $variable string";

//Prohibited:
$a = "I am a {$variable} string";
$a = "I am a ${variable} string";
$a = "I am a $$variableName string";
$a = "I am a ${$variableName} string";
```

* Echo MUST NOT use parentheses, and should utilize parameters for variables

```php
//Accepted:
echo "I am a $variable string";
    OR
echo 'I am a ', $variable, ' string';


//Prohibited:
echo("I am a $variable string");
```

* Longer concatenation operator must be on the upper line, with separating whitespace when necessary

```php
$a = 'I am a very long string that needs to ' .
     'be wrapped around a line';
```

* Concatenation operators MUST be flanked on left by a single space, and on the right by either a space or newline

```php
$a = 'I am a ' . 'string ' .
     'that is concatenated';
```

* For blocks of HTML that are iterated over, functional call to echo are preferred over closing PHP tags to increase readability.
Excessive whitespace in string should be avoided when possible.  HTML should be formatted as close as possible to
[Dynamit HTML standard guide](http://standards.dynamitdev.com/html.html).  __HEREDOCS and NOWDOCS are prohibited__


```php
// Preferred:
<?php
    foreach($objects as $object) {
    echo '<tr>',
           '<td>', $object->firstProperty, '</td>',
           '<td>', $object->secondProperty, '</td>',
           '<td>', $object->thirdProperty, '</td>',
        '</tr>';
    }
?>
    OR
<?php
    foreach($objects as $object) {
    echo "<tr>",
           "<td>$object->firstProperty</td>",
           "<td>$object->secondProperty</td>",
           "<td>$object->thirdProperty</td>",
        "</tr>";
    }
?>

// Prohibited:
    <?php foreach($objects as $object) { ?>
        <tr>
           <td><?php echo $object->firstProperty; ?></td>
           <td><?php echo $object->secondProperty; ?></td>
           <td><?php echo $object->thirdProperty; ?></td>
        </tr>
    <?php } ?>

    <?php
        foreach($objects as $object) {
        echo "<tr>
           <td>$object->firstProperty</td>
           <td>$object->secondProperty</td>
           <td>$object->thirdProperty</td>
         </tr>";
     ?>

    <?php
        foreach($objects as $object) {
           echo <<<HERE
               <tr>
                   <td>$object->firstProperty</td>
                   <td>$object->secondProperty</td>
                   <td>$object->thridProperty</td>
               </tr>
        HERE;
        }
    ?>
```


## Classes &amp; Functions

* Classes refer to all defined objects such as: `class`, `interface`, and `traits`
* Classes MUST be named in UpperCamelCase
* Classes which cannot be instantiated should be prefaced with a single lowercase character denoting their type:

```php
   <table>
     <tr>
       <td> a </td><td>abstract</td><td>aSomeAbstractClass</td>
     </tr>
     <tr>
       <td> i </td><td>interface</td><td>iSomeInterface</td>
     </tr>
     <tr>
       <td> t </td><td>trait</td><td>tSomeTrait</td>
     </tr>
   </table>
```

* Classes' opening brace should be on the same line as class definition
* Methods must be named in lowerCamelCase
* Methods'opening parentheses must not be spaced away from the function name.
* Methods opening brace should be on the same line as the function's closing parenthesis
* Class members (variables) must use lowerCamelCase
* Class constants should be defined in all uppercase with underscores
* Constants are preferred to static members when possible
* Every member &amp; method must have a scoping definition
* Member variables MUST NOT be proceeded with an `_` to denote private or protected
* Scoping definition keyword for both members and methods should be the first keyword in definition
* Any inheritance (`extends`,`implements`) MUST be declared on the same line as class

```php
/**
* PHPDoc Description of this class
*/
class SomeChildClass extends aSomeAbstractClass implements iSomeInterface, iAnotherInterface
{

    /** @var string **/
    private $firstMember = 'DefaultValue';
    /** @var mixed **/
    protected $secondMember;
    /** @var mixed **/
    public $thirdMember;

    /**
    * PHPDoc Documentation block
    */
    public function doOneTask() {
       return 'foo';
    }

    /**
    * PHPDoc Documentation block
    */
    private static function doStaticTask() {
       return 'bar';
    }
}
```

* When making function calls there MUST be no whitespace between any operators, and names

```php
//Correct:
  doOneTask();
  $myInstance->doOneTask();
  SomeChildClass::doStaticTask();

//Prohibited:
  doOneTask( );
  $myInstance -> doOneTask ();
  SomeChildClass:: doStaticTask();
```

* When Passing Parameters, a space MUST NOT be used before a comma, and a space MUST be used after a comma

```php
//Correct:
   $myInstance->myFunction($a, $b, $c);

//Prohibited:
   $myInstance->myFunction($a ,$b,$c);
```

* Long lists of arguments/parameters may be split onto multiple lines, and should align with the first given parameters,
this is true for method/functions definitions as well

```php
$myInstance->someFunction(
   $a, $b, $c,
   $d, $e, $f
);


// AND

/**
* PHPDoc Documentation
*
* @param string $arg1
* @param int $arg2
* ....
*/
public function myFunction(
   $arg1,$arg2,$arg3
   $arg4,$arg5
) {
   //...
}
```

* Return statements MUST NOT use parenthesis

```php
//Correct:
return $foo;

//Prohibited:
return($foo);
```

* Return statements should be only at the top of the function, or at the bottom.

```php
//Correct:
public function foo($bar) {
   if (!$foo) {
       return null;
   }

   //some
   //code
   //and
   //logic
   //here
   return $someVal;

}

//Harder To Read:
public function foo($bar) {
   if($foo){
       //some
       //code
       //and
       //logic
       //here
       return $someVal;
   }else{
       return null;
   }
}
```

## Control Structures &amp; Arrays

* Control keywords MUST be followed by 1 space
* There must not be spaces after the opening parenthesis, nor before the closing.
* The `:` `end` structure for controls are forbidden, use only curly braces
* Control blocks should be separated by a blank line for improved readability
* Long conditionals can, and should be broken up on multiple lines when necessary
* Long conditionals should be split with the operator at the beginning of the new line

```php
if ($myVariable == 1
 && $myVariable2 == 3
 && !is_null($myVariable4)) {
   //body...
}
```

* Better would be to bind long conditionals into easier to read if statements

```php
$isFoo = ($condition1 == 1 && $condition2 == 2);
$isBar = ($condition3 == 3 || $condition4 == 4);
if ($isFoo && !$isBar) {
   //body...
}
```

* Ternary Operator `?` should only be used in simple assignment, or print/echo statements.  __NESTED TERNARIES ARE PROHIBITED__
* Case statements should be preferred to long elseif chains when possible
* None empty cases which do not have a `break` statement should have a comment donating the missing break
* Final cases must be default, and must include a `break`

```php
switch ($expr) {
   case 0:
       echo 'this is case 1';
       break;
   case 1:
       echo 'this is the 2nd case';
       // no break, fall through desired
   case 2:
   case 3:
   case 4:
       echo 'this is the 2-5th case';
       break;
   default:
      echo 'default';
      break;
}
```

* Closure should follow keyword principles

```php
$closureWtihArgsAndValues = function($arg1, $arg2) use ($var1, $var2) {
   // ....
}

$doubleClosureExample = function(
   $arg1,
   function($arg2) use ($var2) {
       //body...
   },
   $arg3
) {
   //body...
}
```

* Arrays must be defined by the shorthand `[...]`
* Key => Value arrays should be aligned along the assignment operator, on the nearest tab

```php
//correct
$myArray = [
    'foo'       => 'fooVal',
    'bar'       => 'barVal',
    'foobar'    => 'foobarVal'
];

//prohibited
$myArray = array(
    'foo'      => 'fooVal',
    'bar'   => 'barVal',
    'foobar' => 'foobarVal'
);
```
