# Sotsera.Blazor.Toaster

A Blazor port of [Toastr.js](https://github.com/CodeSeven/toastr/) in pure .Net. 

__Razor components__ currently [cannot reference static assets from component libraries](https://blogs.msdn.microsoft.com/webdev/2019/01/29/aspnet-core-3-preview-2/#sharing-component-libraries).
As a temporary workaround the [css](https://raw.githubusercontent.com/sotsera/sotsera.blazor.toaster/master/src/Sotsera.Blazor.Toaster/Content/toastr.min.css)
can be saved into the server project wwwroot and loaded by the index.html with something like `<link href="toastr.min.css" rel="stylesheet"/>`.

The sample project has been published [here](https://blazor-toaster.sotsera.com/).

The transitions are implemented using `System.Threading.Timer` so this library should be used only by client side blazor (webassembly).

## Changes

See the [RELEASE-NOTES](https://raw.githubusercontent.com/sotsera/sotsera.blazor.toaster/master/RELEASE-NOTES.md)

## Configuration

`Install-Package Sotsera.Blazor.Toaster`

Configure the dependency injection

```c#
services.AddToaster(config =>
{
    config.PositionClass = Defaults.Classes.Position.TopRight;
    config.PreventDuplicates = true;
    config.NewestOnTop = false;
});
```

and add the toast container to `App.cshtml` (or to another component always loaded in the application)

```c#
@addTagHelper *, Sotsera.Blazor.Toaster
<toastContainer />
```

## Usage

In a component

```c#
@inject Sotsera.Blazor.Toaster.IToaster toaster
```

In a class

```c#
[Inject] 
protected Sotsera.Blazor.Toaster.IToaster Toaster { get; set; }
```

then call one of the display methods:

```c#
toaster.Info("toast body text");
toaster.Success("toast body text");
toaster.Warning("toast body text");
toaster.Error("toast body text");
```

Each of these methods can accept a title and an action for the toast specific configuration

```c#
toaster.Info("toast body text");
toaster.Info("toast body text", "toast title");
toaster.Info("toast body text", "toast title", options =>
{
    options.Clicked += toast => Console.WriteLine($"Toast '{toast.Message}' Clicked!");
});
```

## Credits

This is a simple attempt to port [Toastr.js](https://github.com/CodeSeven/toastr/) to Blazor.

Currently the [css styles](https://github.com/CodeSeven/toastr/blob/50092cc604850a16c985520b63df184d3e0b4086/build/toastr.min.css) used are literally COPIED from Toastr.js.

The [logo](https://www.flaticon.com/free-icon/breakfast_1381870) has been made by [Freepik](https://www.freepik.com/) from [Flaticon](https://www.flaticon.com/) and is licensed by [CC 3.0 BY](http://creativecommons.org/licenses/by/3.0/)


## License

Sotsera.Blazor.Toaster is licensed under [MIT license](http://www.opensource.org/licenses/mit-license.php)
