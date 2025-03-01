systray is a cross-platform Go library to place an icon and menu in the notification area.

## Features

* Supported on Windows, macOS, and Linux
* Menu items can be checked and/or disabled
* Methods may be called from any Goroutine

## API

```go
func main() {
	// Should be called at the very beginning of main().
	systray.Run(onReady, onExit)
}

func onReady() {
	systray.SetIcon(icon.Data)
	systray.SetTitle("Awesome App")
	systray.SetTooltip("Pretty awesome超级棒")
	mQuit := systray.AddMenuItem("Quit", "Quit the whole app")

	// Sets the icon of a menu item. Only available on Mac.
	mQuit.SetIcon(icon.Data)
}

func onExit() {
	// clean up here
}
```

## Try the example app!

Have go v1.12+ or higher installed? Here's an example to get started on macOS:

```sh
git clone https://github.com/getlantern/systray
env GO111MODULE=on go run systray/example/main.go
```

The following text will then appear on the console:


```sh
go: finding github.com/skratchdot/open-golang latest
go: finding github.com/getlantern/systray latest
go: finding github.com/getlantern/golog latest
```

Now look for *Awesome App* in your menu bar!

![Awesome App screenshot](example/screenshot.png)

## Platform notes

### Linux

* Building apps requires the `gtk3` and `libappindicator3` development headers to be installed. For Debian or Ubuntu, you can may install these using:

```sh
sudo apt-get install libgtk-3-dev libappindicator3-dev
```

* Checked menu items are not yet implemented


### Windows

* To avoid opening a console at application startup, use these compile flags:

```sh
go build -ldflags -H=windowsgui
```

### macOS

On macOS, you will need to create an application bundle to wrap the binary; simply folders with the following minimal structure and assets:

```
SystrayApp.app/
  Contents/
    Info.plist
    MacOS/
      go-executable
    Resources/
      SystrayApp.icns
```

Consult the [Official Apple Documentation here](https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html#//apple_ref/doc/uid/10000123i-CH101-SW1).

## Credits

- https://github.com/xilp/systray
- https://github.com/cratonica/trayhost
