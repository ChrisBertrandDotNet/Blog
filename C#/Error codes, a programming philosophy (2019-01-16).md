# Error codes, a programming philosophy

The proposed philosophy is to return codes on errors, not Exceptions.

## Why ?

First, Exceptions have drawbacks:

-   Non-caught exceptions crash applications in the wild.
-   Caught exceptions are very slow and resource-hungry.

Second problem:  
Normally, programmers should catch separately all exceptions a function (a _method_ in .NET's jargon) can throw.  
For example, `System.IO.File.Open()` can throw 9 different exceptions. Every call should be followed by 9 catches.  
In practice, I never see any programmer doing that.  
At best, they just catch the all 9 exceptions at once using a global `catch { }`, which can be seen as a bad practice (not discriminant enough).

All well-designed programming languages should enforce programmers to manage all errors a function can produce.  
Of course, that is so annoying and repetitive that in practice programming languages do not enforce anything at all.  
In short, that practice is highly error-prone and probably causes a lot of problems ("bugs" for entomologists). On the other hand, it takes into account the natural laziness that affects all human beings (including programmers)..

## The proposal

-   All methods (functions and procedures) return error codes on _expected_ errors. For example when a needed file does not exist.
    -   Every function declares, using a specific attribute, the list of all error codes it can return.
-   Every method call manages _all_ the errors that function declares (usually using a switch-case code block).
-   Exceptions are thrown only on _unexpected_ errors, in fact on programming errors. Ideally, they should happen only when "debugging".

Of course, that affects only your own source code. So you still have to catch Exceptions from external libraries, such as the .NET and Core frameworks, that apply the regular exception scheme.

## A library you can use

Recently, I published [CB Helpers](https://github.com/ChrisBertrandDotNet/CB-Helpers), an open-source library that contains structures you can use in your functions to return errors code.

They are in this name space: `CB.Execution`

### Main structures

-   **`ReturnSuccess`** is a common error code enumeration.  
    You can return it in a _procedure_ (instead of `void`).
-   `Return<T,E>` is a return structure that contains both a return value and an error code. The value can be null.
-   **`Ret<T>`** is a shortcut for `Return<T, ReturnSuccess>`.  
    This is the preferred structure to use in _functions_.
-   `ReturnNonNull<T,E>` is similar to `Return<T,E>`, but the value can't be null (except if there is an error, of course).
-   `RetNonNull<T>` is a shortcut for `ReturnNonNull<T, ReturnSuccess>`.

### Simple example

We declare a function:

```C#
[ReturnSuccessCodes(ReturnSuccess.ArgumentOutOfRange)]
Ret<double> Sqrt(double d)
{
  if (d < 0.0) return ReturnSuccess.ArgumentOutOfRange;
  return Math.Sqrt(d);
}
```

Then we call this function:

```C#
var a = this.Sqrt(0.0);
switch(a.ErrorCode)
{
  case ReturnSuccess.ArgumentOutOfRange:
    a = -1; break;
}
```

### Example with a procedure

We declare a procedure:

```C#
[ReturnSuccessCodes(ReturnSuccess.ArgumentOutOfRange)]
ReturnSuccess DisplayLine(int lineNumber)
{
  if (lineNumber < 0) return ReturnSuccess.ArgumentOutOfRange;
  ... // do some work
  return ReturnSuccess.Success;
}
```

Then we call this procedure:

```C#
var e = this.DisplayLine(100);
if (e == ReturnSuccess.ArgumentOutOfRange)
  ... // Take the error in consideration.
```

### Example with a customized error code enumeration

First we declare an error set:

```C#
enum MyErrorCodes
{ NotInitialized, Success, StringIsEmpty, StringIsNull }
```

Then a function that returns errors from the set:

```C#
[ReturnCodes((int)MyErrorCodes.StringIsEmpty, (int)MyErrorCodes.StringIsNull)]
static ReturnNonNull<String, MyErrorCodes> EnsuresStringIsDefined(string p)
{
  if (p == null)
    return new ReturnNonNull<string, MyErrorCodes>(MyErrorCodes.StringIsNull);
  if (p == string.Empty)
    return new ReturnNonNull<string, MyErrorCodes>(MyErrorCodes.StringIsEmpty);
  return new ReturnNonNull<string, MyErrorCodes>(p);
}
```

And finally we call the function:

```C#
var s = EnsuresStringIsDefined("good");
switch (s.ErrorCode)
{
  case MyErrorCodes.StringIsEmpty:
    s = "!Empty!"; break;
  case MyErrorCodes.StringIsNull:
    s = "!Null!"; break;
}
```

### Additional structures

-   The structure `ReturnError` contains both a ReturnSuccess and an _Exception_.  
    It can be used when a function returns a detailed exception message: for example "Write access to file **x.y** is denied because it is open by process **z**".