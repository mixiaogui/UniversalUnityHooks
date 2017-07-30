## Synopsis

UniversalUnityHooks aims to bring a adaptable modding API to any unity game. This is acomplished by hooking into methods found in the Assembly-CSharp.dll and modifying them while avoiding having to decompile and recompile.

## Code Example

```cs
public class printStart
{
	[Hook("SvNetMan.StartServerNetwork")]
	public static void startServerNetwork(SvNetMan man)
	{
		Debug.Log("Plugin Loaded!");
	}

}
```

In this example the game hooks the examples ServerStartNetwork method in the SvNetMan Class, and prints Plugin Loaded when the server connects to the network
## Motivation

The inital motivation behind the project was to provide a way for server owners to develop plugins for the game Broke Protocol (https://brokeprotocol.com). But due to the way unity games are made, this program can be ported to any other game relatively easily

## Installation

Assuming Linux (x64)

For windows:

* Change `/`'s to `\`'s for file names in the HooksInjector Project.
* Build the files from Visual Studio or under Bash For Windows
Prerequites:
* mono-complete

To build the files from source and install them simply:

*Build HookAttribute with `xbuild HookAttribute.csproj` and place the HookAttribute.dll in $Gamedir/Game_Data/Managed
*Build Hooks Injector with `xbuild HooksInjector.csproj` and place HooksInjector.exe along with the `Mono.Cecil` dll's in $Gamedir


## API Reference

The program is fairly straight forward, to hook a method, simply put 
`[Hook("Class.Method")]` 
Then supply the instance as the first variable, and the rest of the variables as refs.
So if I were to want to modify Damage of the SvPlayer Class with variables otherId and damage, That would become
```cs
damage(SvPlayer player, ref int otherId, ref float damage);
```

## License

This code is licenced under the GNU GPL3 Licence, Information can be found by clicking on it at the top of the repository.