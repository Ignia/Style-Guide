# C# Class Libraries

As class libraries are typically intended to be used by a broad selection of developers who may not have any insight (or access to) the internal workings of the library, they introduce their own unique challenges. While these are documented separately from our general [C# Style Guide](../C%23/Readme.md), Ignia considers these guidelines a best practice for all C# development.

> # Placeholder Content
> This page is a placeholder; additional content will be provided at a later date.

## Identifiers
- Namespaces should use `<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]` convention ([source](https://msdn.microsoft.com/en-us/library/ms229026%28v=vs.110%29.aspx))
- Ignia uses `Ignia` for the `<company>` on internal projects and reusable libraries, but the client name for custom client code

## Spacing
- The `namespace` may be introduce above a file header; this allows the file header to document the `class`, not the `namespace` (which is usually not unique to the file)

## Formatting
- Each attribute should be placed on its own line

## Language Features
- `Dictionary<>` and `List<>` objects should not be exposed publicly; instead, use `Collection<>` or `KeyedCollection<>`
- Local variables *should* use type inference (i.e., the `var` keyword for declaring variables)
- Any `using` directives should be placed inside the `namespace`, not outside of it

## Acknowledgments
- [Microsoft Framework Design Guidelines](https://msdn.microsoft.com/en-us/library/ms229042(v=vs.110).aspx)
- [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries (2nd Edition)](http://www.amazon.com/Framework-Design-Guidelines-Conventions-Libraries/dp/0321545613)
