The discussions about [C# 8 and the Nullable reference types](https://github.com/dotnet/csharplang/blob/master/proposals/nullable-reference-types.md) reminded a library I made a few years ago and I still use in my code.  
The main structure was called `NonNull<T>`. As you can imagine it was an implementation of the concept of non-null references, which is not new.

C# 8 now has its own non-null reference system, making my `NonNull` class useless on this version.  
Nevertheless it can be useful on projects that compile an earlier version of C#.

Anyway, this library contains related types that may be useful, _even on C# 8_, such as:

-   `DefinedString`
-   `DefinedEnum`
-   `Bounded`

## By the way, why would we need non-null references ?

The fact is regular nullable references are a potential problem.  
In regular C# programming, we have to check all references a function returns, in order to ensure they are not null. Unfortunately it is very easy to forget to write this check, and the compiler does not warn or generate an error.

The concept of non-null references prevents this threat by eliminating the possibility of a null reference.

## The library

[CB Helpers](https://github.com/ChrisBertrandDotNet/CB-Helpers) is an open-source library I recently published. It contains many types and functions that may help you.

About certified values, you will find the following structures in the name space `CB.Data`:

-   `NonNull<>` certifies the reference is non-null.
-   `DefinedString` certifies the string is not null _and_ is not empty.
-   `DefinedEnum<>` certifies the enumeration value is declared in its enumeration type. The `[Flags]` attribute can be checked too.
-   `Bounded<>` certifies the value is in its range. Useful for numbers.

## Examples

```C#
NonNull<TextInfo> GetTextInfo(NonNull<CultureInfo> culture)
{
  // No use to check the parameter: it can't be null.
  return culture.Value.TextInfo; // We certify the return value is defined.
}
DefinedString ToUpper(DefinedString s)
{
  // No use to check the parameter: it can't be null or String.Empty.
  return s.Value.ToUpper(); // We certify the return value is defined.
}
DefinedEnum<UnicodeCategory> GetUnicodeCategory(char c)
{
  return char.GetUnicodeCategory(c); // We certify the return value is a declared value of its enumeration.
}
...
var number1 = new Percentage(50); // this is a Bounded<Double>.
```

## structure `NonNull<T>`

Example of local variable or field:

```C#
NonNull<CultureInfo> culture = CultureInfo.CurrentUICulture; // implicitly transtyped. 'culture' is certified not to be null.
```

Example of function parameter:

```C#
NonNull<TextInfo> GetTextInfo(NonNull<CultureInfo> culture)
{
  // No use to check the parameter: it can't be null.
  return culture.Value.TextInfo; // We certify the return value is defined.
}
```

## structure `DefinedString`

Defines a reference to a String. This reference can't be null or String.Empty.

Example of local variable or field:

```C#
DefinedString name = CultureInfo.CurrentUICulture.Name; // implicitly transtyped. 'name' is certified not to be null or empty.
```

Example of function parameter:

```C#
DefinedString ToUpper(DefinedString s)
{
  // No use to check the parameter: it can't be null or String.Empty.
  return s.Value.ToUpper(); // We certify the return value is defined.
}
```

Note:  
If you want your reference can be String.Empty but not null, you can use `NonNull<string>` instead of `DefinedString`.

## structure `DefinedEnum<T>`

Here, a "declared enumeration value" is a value of an enumeration set that is explicitly declared.  
`DefinedEnum<T>` certifies such a value is a declared enumeration value.

Examples:

```C#
DefinedEnum<System.PlatformID> Windows = System.PlatformID.Win32NT; // ok, this value is declared in its enumeration.
DefinedEnum<System.PlatformID> MyOwnSystem = (System.PlatformID) 1000; // Wrong ! That will throw an ArgumentException.
```

### What about `[Flags]` ?

`System.FlagsAttribute` indicates that an enumeration can be treated as a bit field; that is, a set of flags.

A function let you know if a value is unique or is the addition of various values: `IsDeclaredAsAUniqueValue()`.

## Always initialize your structures [very important !]

You have to take extra precautions using these structures. C# does not let us write both constructors with parameters and a default (no-parameter) constructor in the same structure.  
So _you_ have to make sure you never use an uninitialized structure.

The following note is for `NonNull<>`, but it is true of the other structures too.

-   Never define a field of type `NonNull<>` without building an instance.
-   Never initialize a local variable by `default(NonNull<>)`.

The compiler will not warn you. The error will appear on the next value reading only: in most cases, an exception will be thrown.

Example:

```C#
string UnintializedNonNull()
{
  var nullRef = default(NonNull<CultureInfo>); // Never write that !
  return nullRef.Value.Name; // Will throw an InvalidOperationException.
}
```

The reason why I did not declare these types as classes, if you want to know, is for optimization.

## Bounded values

You can create a type that will certify values are in the right range.  
Commonly used with numbers, it can be applied to any type that implements both `IComparable<T>` and `IEquatable<T>`.

### class `Bounded<T>`

The lower and upper bounds are respectively called Minimum and Maximum. They form the range.  
Please note Minimum and Maximum can be included or excluded from the range. By default, they are included.

First we declare a bounded type:
```C#
/// <summary>
/// A number, bounded in [ 0 ; 100 [
/// </summary>
internal class Percentage : Bounded<int>
{
  public override int Minimum => 0;
  public override int Maximum => 100;
  public override bool RangeIncludesTheMinimum => true;
  public override bool RangeIncludesTheMaximum => false;

  public Percentage(int value)
    : base(value)
  { }

  public static implicit operator Percentage(int value)
  {
    return new Percentage(value);
  }
}
```
Then we use it to declare values:
```C#
var number1 = new Percentage(50); // ok, 50 is between 0 and 100.
try { var number2 = new Percentage(-200); } // Wrong ! That will throw an ArgumentOutOfRangeException();
catch (ArgumentOutOfRangeException) { }
```
###  If you don't want to declare a class

If you declare only a few values, maybe you don't want to implement a complete class.  
You can then instanciate a range generator:
```C#
var angleRange = Bounded<double>.CreateASimpleRange(0, 360, true, false); // Serves as a range for angles.
```
then use this range to create certified values (_angles_, here):
```C#
var angle180 = angleRange.NewValue(180.0); // ok, that angle is in the range.
```
You can create values that may be certified or not:
```C#
var wrongAngle = angleRange.TryCreateValue(1000); // Wrong, the value is not in the range. The result is null.
```
If you want to certify both the value is defined (not null) and is in the range, you can use the type NonNull:
```C#
var certifiedAngle = angleRange.NewValueAsNonNull(200); // returned type: NonNull<IBounded<double>>.
```
## class `ExistingDirectory` in CB.Files.cs

Following the same idea of certified objects, but in a different code file, CB.Files.ExistingDirectory certifies the directory exists, at least at the moment of the instanciation of the class.