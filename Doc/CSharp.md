# C# (`Language.CSharp`)

**C#** has been implemented with the [Roslyn engine](https://github.com/dotnet/roslyn).

[Implementation](https://github.com/mrousavy/Fiddle/tree/master/Fiddle.Compilers/Implementation/CSharp) / [Compiler](https://github.com/mrousavy/Fiddle/blob/master/Fiddle.Compilers/Implementation/CSharp/CSharpCompiler.cs)

## Completeness

- [x] Syntax highlighting
- [x] Compilation
- [x] Execution
- [x] Console ouput
- [x] Return values
- [x] Diagnostics
- [x] Errors

[Example Code](https://github.com/mrousavy/Fiddle/blob/master/Fiddle.Compilers/Implementation/CSharp/CSharpDemo.cs) | [Projects](https://github.com/mrousavy/Fiddle/projects)

## About

With C# you can write **Scripts**, aswell as **full source code**. So:
```cs
return 1+1;
```
will compile just as fine as:
```cs
public class MainClass {
    public static void main(string[] args) {
    	Console.WriteLine(1+1);
    }
}
```

## Globals
You can use the following **Globals/Variables** inside your code:

* `Random` (**object**, .NET `System.Random`, [msdn](https://msdn.microsoft.com/en-us/library/system.random(v=vs.110).aspx)): **Create random numbers** with [`Random.Next(..)`](https://msdn.microsoft.com/en-us/library/system.random.next(v=vs.110).aspx)

* `Console` (**object**, .NET `System.IO.StringWriter`, [msdn](https://msdn.microsoft.com/en-us/library/system.io.stringwriter(v=vs.110).aspx)): **Write to Console** with [`Console.WriteLine(string)`](https://msdn.microsoft.com/en-us/library/system.console.writeline(v=vs.110).aspx) or [`Console.Write(string)`](https://msdn.microsoft.com/en-us/library/system.console.write(v=vs.110).aspx)

* `CurrentThread` (**object**, .NET `System.Threading.Thread`, [msdn](https://msdn.microsoft.com/en-us/library/system.threading.thread(v=vs.110).aspx)): The thread this got initialized on (**mostly UI Thread**), can be used to access all properties or functions from a [`System.Threading.Thread`](https://msdn.microsoft.com/en-us/library/system.threading.thread(v=vs.110).aspx).

* `Editor` (**object**, Fiddle `Fiddle.UI.Editor` (from `System.Windows.Window`, [msdn](https://msdn.microsoft.com/en-us/library/system.windows.window(v=vs.110).aspx))): Fiddle's Editor window, can be used to access all [`UIElements`](https://msdn.microsoft.com/en-us/library/system.windows.uielement(v=vs.110).aspx), properties, public functions or functions derived from `System.Windows.Window`. ([Editor XAML code](https://github.com/mrousavy/Fiddle/blob/master/Fiddle.UI/Editor.xaml), [Editor source code](https://github.com/mrousavy/Fiddle/blob/master/Fiddle.UI/Editor.xaml.cs))

* `App` (**object**, .NET `System.Windows.Application`, [msdn](https://msdn.microsoft.com/en-us/library/system.windows.application(v=vs.110).aspx)): Fiddle's calling `Application`/`App`, can be used to access all properties or functions derived from [`System.Windows.Application`](https://msdn.microsoft.com/en-us/library/system.windows.application(v=vs.110).aspx))

* `RunUi(Action)` (**function**, `void Invoke(Action)`, [declaration](https://github.com/mrousavy/Fiddle/blob/master/Fiddle.UI/FiddleGlobals.cs#L13)): A function with an anonymous function or [`Action`](https://msdn.microsoft.com/en-us/library/018hxwa8(v=vs.110).aspx) as a parameter **to execute code on the UI Thread**. This is **required for getting/setting properties or calling functions from `Editor` or `App`** because those are **not thread safe**. Example:

```cs
RunUi(()=>{
	Editor.Opacity = 0.5;
});
```

## Properties
- `string[] imports`: A list of assemblies to be referenced and imported by the script. If empty, **Fiddle** will import **all found referenced assemblies of it's own executable** via reflection. _(If you are experiencing performance problems/long compile & execute times, you may want to **customize this list to only import assemblies you need**.)_
