# Ignore "Expression value not used" for fluent interfaces

This diagnostic suppressor allows you to specify a list of types for which method return values can be ignored.

This is particularly useful for "fluent interfaces," such as `System.Text.StringBuilder`, where the return values are just the current instance. However, IDE0058 ("Expression value not used") would be reported on such types, even though "using" (i.e. storing) the value was useless. This suppressor was created for this type of situations

## Usage

First, add the package to your .csproj file:
```xml
  <ItemGroup>
    <PackageReference Include="Blokyk.Roslyn.ValueNotUsedSuppressor" Version="*" />
  </ItemGroup>
```

Once the package restored, you can configure the types affected by this suppressor by adding the `dotnet_fluent_types` key to your `.editorconfig` file and then specifying a comma-separated list of (fully-qualified metadata) type names.

For example, if you had an interface `FluentRecord<T>` inside the namespace `MyStuff.Utils`, you'd add :
```editorconfig
dotnet_fluent_types = System.Text.StringBuilder, MyStuff.Utils.FluentRecord`1
```

The default value for `dotnet_fluent_types` is currently `System.Text.StringBuilder`.
