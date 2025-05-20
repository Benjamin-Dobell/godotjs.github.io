# Debugger

A debugger bridge is implemented is _GodotJS_ which supports v8 inspector protocol. `Chrome devtools` and `VSCode` are both supported to debug your JS/TS code.

> **NOTE:** The listening port can be changed in `Project Settings`, and a restart is required for it to take effect.  
> `Project Settings > GodotJS > Debugger > Editor Port` for `Editor` environment  
> `Project Settings > GodotJS > Debugger > Runtime Port` for `Runtime` environment.
> Check `Advanced Settings` if they are not listed in `Project Settings`.

## VSCode

Add the following configuration into `launch.json`:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "Attach (Inspector)",
      "protocol": "inspector",
      "address": "127.0.0.1",
      "port": 9229
    }
  ]
}
```

Then, press `Start debugging (F5)` on the `Run and Debug` panel after your app launched.

![vscode_debug](images/vscode_debugger.png)

## Chrome devtools

Open `devtools://devtools/bundled/inspector.html?experiments=true&v8only=true&ws=127.0.0.1:9229/1` in `Chrome` to start debugging the sources.

![browser debugging](images/browser-debugger.png)

## JetBrains IDEs

1. Goto `Main Menu > Run > Edit Configurations`
2. Press ➕ (Add new configuration)
3. Select `Attach to Node.js/Chrome`
4. Add a name to the configuration and select port `9229`
5. Start the configuration

![jetbrains ide debugger](images/jetbrains.png)

## Safari

Enable `Show features for web developers` in settings:
![safari_settings_enable_dev](images/safari_settings_enable_dev.png)

Select the session from menu:
![safari_inspector_select](images/safari_inspector_select.png)

A web inspector window will be open if successfully:
![safari_web_inspector](images/safari_web_inspector.png)

## Troubleshooting

Q: The debugger is connected successfully, but why no breakpoints can hit (or the devtools reports that a source can not be located)?  
A: The debugger is resolving the source from a wrong place. Please update the value of `sourceRoot` in your `tsconfig.json` to an appropriate path (can be a relative path).
