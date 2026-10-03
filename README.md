# Awake Plugin Template

A starter editor plugin for [Awake](https://github.com/awakekt/awake). Copy it to build your own.
It depends only on Awake Core's Apache-2.0 plugin contract (`com.awakekt.awake.editor:contract`),
never on an editor's own code, so it runs in Awake Studio or any other Awake editor host.

The sample is a small weather plugin:

| File | Hook | What it adds |
|---|---|---|
| `WeatherPanel.kt` | `PanelProvider` | A "Weather" tab in the bottom panel |
| `RainToggle.kt` | `ToolbarProvider`, `KeybindingProvider` | A toolbar button and Ctrl+R to toggle rain |
| `RainCloudTemplate.kt` | `EntityTemplateProvider` | "Rain cloud" in the insert menu, built from Core scene components |
| `WeatherPlugin.kt` | `EditorPlugin` | The entry point that hands the host those providers |

Every hook and its use is listed in the
[contract README](https://github.com/awakekt/awake/blob/main/awake/editor/contract/README.md).

## Make it yours

1. Rename the package `com.awakekt.awake.plugin.template` and the plugin ID in `WeatherPlugin.kt`
   and `plugin/plugin.json` to your own reverse domain. Every provider ID starts with the plugin ID.
2. Replace the sample providers with your own.
3. Keep runtime out of the plugin: a plugin edits data the game reads. Anything a shipped game must
   run belongs in Awake Core or the game itself.

## Build

```bash
./gradlew :plugin:desktopTest :plugin:awakePlugin
```

The archive lands in `plugin/build/awakeplugin/`. It holds `plugin.json` and the plugin's classes
under `lib/`; the host supplies the contract, so it is not bundled.

## Install

| Platform | How the plugin gets in |
|---|---|
| Desktop | Studio → Marketplace → Import, pick the `.awakeplugin` file. It loads at run time. |
| Android, iOS, web | Add the `plugin` module to the app's build as a Gradle dependency. These platforms cannot load downloaded code at run time. |

Studio shows a warning before installing a plugin from an unverified developer. Plugins listed in the
Awake marketplace, and paid plugins, are signed and install without one. Until Studio ships that
warning, a release build accepts only signed plugins; a development build (`AWAKE_ALLOW_UNSIGNED=true`)
accepts this archive as is.

## Repository map

| Repository | What it holds |
|---|---|
| [awakekt/awake](https://github.com/awakekt/awake) | Awake Core: the engine and the plugin contract |
| [awakekt/awake-template](https://github.com/awakekt/awake-template) | The starting project for a new game |
| [awakekt/awake-plugin-template](https://github.com/awakekt/awake-plugin-template) | This starter plugin |
| [awakekt/awake-game-agent-skills](https://github.com/awakekt/awake-game-agent-skills) | Agent skills for building games, tools and plugins on Awake |

## License

Apache-2.0. See [LICENSE](LICENSE).
