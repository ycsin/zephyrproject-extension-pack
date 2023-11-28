# ZephyrProject🪁 Extension Pack

A collection of extensions helpful for [ZephyrProject](https://zephyrproject.org/) (vendor neutral) development in Visual Studio Code.

> [!NOTE]
> This extension is an independent community contribution, and is not part of the ZephyrProject.

## Configuration

### IDE

This section will walk through the setup for some of the extensions included in this extension pack, to give VSCode an IDE-feel for Zephyr. The configurations below assumes that the `*.code-workspace` file is in the `zephyrproject` directory (same level as `zephyr`), and `Workspace` configs are recommended whenever possible.

#### [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

This extensions just works out of the box, signing-in via GitHub would allow you to open the PR that introduced the line change directly.

#### [checkpatch](https://marketplace.visualstudio.com/items?itemName=idanp.checkpatch)

1. Points to the Zephyr's `checkpatch.pl` script
   1. Search for `checkpatch.checkpatchPath` in Settings
   2. Set the path accordingly, i.e. `~/zephyrproject/zephyr/scripts/checkpatch.pl`
2. Modify the arguments to checkpatch
   1. Search for `checkpatch.checkpatchArgs` in Settings
   2. Click `Edit in settings.json`
   3. Replace the `"checkpatch.checkpatchArgs"` array with configs from [Zephyr](https://github.com/zephyrproject-rtos/zephyr/blob/main/.checkpatch.conf), the end result should be something like this:

```json
"checkpatch.checkpatchArgs": [
	"--emacs",
	"--summary-file",
	"--show-types",
	"--max-line-length=100",
	"--min-conf-desc-length=1",
	"--typedefsfile=scripts/checkpatch/typedefsfile",
	"--ignore BRACES",
	"--ignore PRINTK_WITHOUT_KERN_LEVEL",
	"--ignore SPLIT_STRING",
	"--ignore VOLATILE",
	"--ignore CONFIG_EXPERIMENTAL",
	"--ignore PREFER_KERNEL_TYPES",
	"--ignore PREFER_SECTION",
	"--ignore AVOID_EXTERNS",
	"--ignore NETWORKING_BLOCK_COMMENT_STYLE",
	"--ignore DATE_TIME",
	"--ignore MINMAX",
	"--ignore CONST_STRUCT",
	"--ignore FILE_PATH_CHANGES",
	"--ignore SPDX_LICENSE_TAG",
	"--ignore C99_COMMENT_TOLERANCE",
	"--ignore REPEATED_WORD",
	"--ignore UNDOCUMENTED_DT_STRING",
	"--ignore DT_SPLIT_BINDING_PATCH",
	"--ignore DT_SCHEMA_BINDING_PATCH",
	"--ignore TRAILING_SEMICOLON",
	"--ignore COMPLEX_MACRO",
	"--ignore MULTISTATEMENT_MACRO_USE_DO_WHILE",
	"--ignore ENOSYS",
	"--ignore IS_ENABLED_CONFIG"
]
```

#### [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

For `west` to generate the `compile_commands.json` in the `build` folder for the IntelliSense to work, do:

```
west config build.cmake-args -- -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
```

See [reference](https://docs.zephyrproject.org/latest/develop/west/build-flash-debug.html#permanent-cmake-arguments).

Then, search for `C_Cpp.default.compileCommands` in the Settings and set the path accordingly, i.e.:

```
${workspaceFolder}/build/compile_commands.json
```

Intellisense should work after you build your project once, if it doesn't, do `Rescan IntelliSense`.

#### [nRF Kconfig](https://marketplace.visualstudio.com/items?itemName=nordic-semiconductor.nrf-kconfig)

This extension supercedes the original [Kconfig for the Zephyr Project](https://marketplace.visualstudio.com/items?itemName=trond-snekvik.kconfig-lang) extension, despite it being published by Nordic Semiconductor now, it works just fine for any other SoCs. Simply search for `kconfig.zephyr.base` in Settings and set that to the `zephyr` dir, i.e. `"~/zephyrproject/zephyr"`.

#### [DeviceTree for the Zephyr Project](https://marketplace.visualstudio.com/items?itemName=trond-snekvik.devicetree)

1. Configure `devicetree.west` in the Settings to the path of `west`, you can do `which west` in Linux to find out the path, i.e.: `"~/zephyrproject/.venv/bin/west`
2. Configure the `devicetree.zephyr` in the Settings to the path of `zephyr`, i.e.: `"~/zephyrproject/zephyr"`

## Additional tips

1. Check the format of last commit by doing `gitlint` before submitting:

```
(.venv) ycsin@LAPTOP-ROG:~/zephyrproject/zephyr$ gitlint
1: UC2 Commit message does not contain a 'Signed-off-by:' line
1: UC3 Commit title does not follow [subsystem]: [subject] (and should not start with literal subsys:): "stash"
1: UC6 Commit message body is empty, should at least have 1 line(s).
3: B6 Body message is missing
```

2. Format the whole file by doing <kbd>SHIFT</kbd> + <kbd>ALT</kbd> + <kbd>TAB</kbd>, format the highlighted line(s) by doing <kbd>CTRL</kbd> + <kbd>K</kbd>, <kbd>CTRL</kbd> + <kbd>F</kbd>

3. Run checkpatch if it doesn't already by <kbd>CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>P</kbd>, and type `Checkpatch Selected File`.

4. Preview markdown file by <kbd>CTRL</kbd> + <kbd>K</kbd>, <kbd>V</kbd>.


## Credits
- [Logo created by Freepik - Flaticon](https://www.flaticon.com/free-icons/kite)
