# C# Class Libraries

As class libraries are typically intended to be used by a broad selection of developers who may not have insight (or access to) the internal workings of the library, they introduce their own unique challenges. While these are documented separately from our general [C# Style Guide](../C%23/README.md), Ignia considers these guidelines a best practice for all C# development.

> *Note:* This style guide inherits rules from the [C# Style Guide](../C%23/README.md), [C-Based Languages Style Guide](../README.md), and the [Global Style Guide](../../README.md)

> *Note:* The majority of the items below are from the (excellent) book "[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries (2nd Edition)](http://www.amazon.com/Framework-Design-Guidelines-Conventions-Libraries/dp/0321545613) (Krzysztof Cwalina, Brad Abrams; 2008) which is required reading for all developers at Ignia. The items highlighted below are some of the most important and common conventions from the book.

## Contents
- [Identifiers](#identifiers)
- [Spacing](#spacing)
- [Formatting](#formatting)
- [Language Features](#language-features)
  - [Collection](#colletions)
  - [Exceptions](#exceptions)
  - [Enums](#enums)
- [Acknowledgments](#acknowledgments)

## Identifiers
- Namespaces should use `<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]` convention ([source](https://msdn.microsoft.com/en-us/library/ms229026%28v=vs.110%29.aspx))
- Assemblies (DLLs) should generally be named `<Company>.(<Product>|<Technology>)[.<Feature>].dll` for consistency with namespaces

> *Note:* Ignia uses `Ignia` for the `<company>` on internal projects and reusable libraries, but the client name for custom client code

- Namespace identifiers should typically be pluralized (exceptions: proper names, abbreviations) ([source](https://msdn.microsoft.com/en-us/library/ms229026(v=vs.110).aspx))
- Do not use the same identifier for a namespace as well as a class ([source](https://msdn.microsoft.com/en-us/library/ms229026(v=vs.110).aspx))
- "If your brand employs nontraditional casing, you should follow the casing defined by your brand, even if it deviates from normal namespace casing" ([source](https://msdn.microsoft.com/en-us/library/ms229026(v=vs.110).aspx))
- Avoid generic identifier names that are likely to introduce conflicts with other class names ([source](https://msdn.microsoft.com/en-us/library/ms229026(v=vs.110).aspx))
- Interfaces should begin with `I` and use adjective phrases; nouns are more appropriate for abstract classes ([source](https://msdn.microsoft.com/en-us/library/ms229040(v=vs.110).aspx))
- `Attribute`, `EventHandler`, `EventArgs`, `Exception`, `Collection`, and `Permission` are all expected suffixes for corresponding class types ([source](https://msdn.microsoft.com/en-us/library/ms229040(v=vs.110).aspx))

## Language Features
- Only use public fields for constants; otherwise, expose properties ([source](https://msdn.microsoft.com/en-us/library/ms229057(v=vs.110).aspx))
- Consider using extension methods as a means of providing concrete implementations for general interface methods ([source](https://msdn.microsoft.com/en-us/library/dn169395(v=vs.110).aspx))
- Use the least derived type for method parameters; e.g., use an interface or base class when its properties are sufficient ([source](https://msdn.microsoft.com/en-us/library/ms229015(v=vs.110).aspx))
- Avoid using `out` or `ref` types for parameters ([source](https://msdn.microsoft.com/en-us/library/ms229015(v=vs.110).aspx))
- Consider using the `params` keyword for short array parameters; otherwise, place arrays as the last parameter in a method so this can be applied in the future ([source](https://msdn.microsoft.com/en-us/library/ms229015(v=vs.110).aspx))
- Prefer events to callbacks (e.g., `Func<>`, `Action<>`, and `Expression<>`) because they are easier to understand and implement across languages ([source](https://msdn.microsoft.com/en-us/library/ms229041(v=vs.110).aspx))
- Be wary of `virtual` members, as they provide potential security risks; when used, consider moving extensible functionality to a `protected` method to restrict scope ([source](https://msdn.microsoft.com/en-us/library/ms229044(v=vs.110).aspx))
- Provide concrete classes for both `abstract` classes as well as `interface` definitions; this helps validate the design, and provides simpler options for casual implementations ([source](https://msdn.microsoft.com/en-us/library/ms229019(v=vs.110).aspx))
- Consider providing reference tests for `abstract` classes and `interface` definitions to allow first- and third-party developers to easily test their implementations ([source](https://msdn.microsoft.com/en-us/library/ms229019(v=vs.110).aspx))
- For serialization, prefer [Data Contract Serialization](https://msdn.microsoft.com/en-us/library/system.runtime.serialization.datacontractattribute(v=vs.110).aspx) unless control over the XML schema is needed (then use [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer(v=vs.110).aspx)) or the objects will be used via .NET Remoting (then use [Runtime Serialization](https://msdn.microsoft.com/en-us/library/system.serializableattribute(v=vs.110).aspx)) ([source](https://msdn.microsoft.com/en-us/library/dn169405(v=vs.110).aspx))
- Avoid use of nested types

### Collections
- `Dictionary<>`, `Hashtable`, `ArrayList`, `List<>`, and `IEnumerator` objects should not be exposed publicly ([source](https://msdn.microsoft.com/en-us/library/dn169389(v=vs.110).aspx))
 - `IEnumerator` may be returned as the result of a `GetEnumerator()` method
 - Arrays should be avoided for similar reasons ([source](https://msdn.microsoft.com/en-us/library/k2604h5s(v=vs.110).aspx))
- Use the least derived collection type for parameters; ideally, this will be the `IEnumerable<T>` interface ([source](https://msdn.microsoft.com/en-us/library/dn169389(v=vs.110).aspx))
- Do not expose setters for collection properties ([source](https://msdn.microsoft.com/en-us/library/dn169389(v=vs.110).aspx))
- For writable properties and return values, prefer `Collection<>`, `ObservableCollection<>` (or a derived class); otherwise, use classes that implement `ICollection<>`, `IList<>`, or `IEnumerable<>` ([source](https://msdn.microsoft.com/en-us/library/dn169389(v=vs.110).aspx))
  - When practical, use a custom derived class for clarity of purpose, and to allow additional functionality to be added in the future
  - When creating custom derived classes, prefer the naming convention `TypeCollection` where `Type` maps to the item type (e.g., `AuthorCollection` is a collection of `Author` objects)
- For volatile collections (e.g., a file system object), return a snapshot (via a method) or an `IEnumerable<>` (via a property)
- For read-only collections, always use `ReadOnlyCollection<>` (or a derived class)
- Never return a `null` value for collection types; always return an empty collection instead

### Exceptions
- Avoid throwing exceptions from properties; any state checking should be done when an action is performed (e.g., by calling a method)
- Validate arguments, and throw `ArgumentException`, `ArgumentNullException`, `InvalidOperationException`, or a derived class on error ([source](https://msdn.microsoft.com/en-us/library/ms229015(v=vs.110).aspx))
  - Always set the `paramName` property when throwing `ArgumentException` or `ArgumentNullException`; use `value` when validating property setters ([source](https://msdn.microsoft.com/en-us/library/ms229007(v=vs.110).aspx))
- With the exception of unforeseeable problems (e.g., system failures), users should be able to pre-check conditions without throwing an exception via the Tester-Doer pattern ([source](https://msdn.microsoft.com/en-us/library/ms229030(v=vs.110).aspx))
  - e.g., the `FileStream` class offers a `CanWrite` property to conditionally determine if a stream can be written to
  - Fall back to the Try-Parse pattern for scenarios where providing pre-condition checks is not performant ([source](https://msdn.microsoft.com/en-us/library/ms229009(v=vs.110).aspx))
- Never throw a `NullReferenceException`, `AccessViolationException`, or `IndexOutOfRangeException`; these should be caught as part of argument checking ([source](https://msdn.microsoft.com/en-us/library/ms229007(v=vs.110).aspx)).
- Do not throw or catch `Exception` or `SystemException`; use more specific exceptions instead (exception: top-level exception handlers) ([source](https://msdn.microsoft.com/en-us/library/ms229007(v=vs.110).aspx))

### Enums
- Prefer enums over arbitrary strings (e.g., `Status="Complete"`) or static constants to set or receive values from a set of predefined (non-dynamic) choices
- Prefer enums as method parameters to multiple Boolean arguments, or Boolean arguments which may have more options in the future ([source](https://msdn.microsoft.com/en-us/library/ms229015(v=vs.110).aspx))
- Enums should be singular, unless they implement the `[flag]` attribute; enums should *not* be suffixed with `Enum` or `Flags` ([source](https://msdn.microsoft.com/en-us/library/ms229040(v=vs.110).aspx))
- Only set enum values for capabilities currently supported; do not reserve values for future use ([source](https://msdn.microsoft.com/en-us/library/ms229058(v=vs.110).aspx))
- Always provide an enum value for `None` (or the semantic equivalent) ([source](https://msdn.microsoft.com/en-us/library/ms229058(v=vs.110).aspx))
- Flag enums can be used to allow multiple values; assigned integers should be based on powers of two (2, 4, 8...) ([source](https://msdn.microsoft.com/en-us/library/ms229058(v=vs.110).aspx))

## Acknowledgments
- [Microsoft Framework Design Guidelines](https://msdn.microsoft.com/en-us/library/ms229042(v=vs.110).aspx)
- [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries (2nd Edition)](http://www.amazon.com/Framework-Design-Guidelines-Conventions-Libraries/dp/0321545613)
