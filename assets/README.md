## Syntax Highlighting in bat

`bat` uses the [syntect](https://github.com/trishume/syntect) library to highlight source
code. As a basis, syntect uses [Sublime Text](https://www.sublimetext.com/) syntax definitions
in the `.sublime-syntax` format.

In order to add new syntaxes to `bat`, follow these steps:

1. Find a Sublime Text syntax for the given language, preferably in a separate Git repository
   which can be included as a submodule (under `assets/syntaxes`).

2. If the Sublime Text syntax is only available as a `.tmLanguage` file, open the file in
   Sublime Text and convert it to a `.sublime-syntax` file via *Tools* -> *Developer* ->
   *New Syntax from XXX.tmLanguage...*. Save the new file in the `assets/syntaxes` folder.

3. Run the `create.sh` script. It calls `bat cache --build` to parse all available
   `.sublime-syntax` files and serialize them to a `syntaxes.bin` file (in this folder).

4. Re-compile `bat`. At compilation time, the `syntaxes.bin` file will be stored inside the
   `bat` binary.

5. If you send a pull request with your changes, please do *not* include the changed `syntaxes.bin`
   file. A new binary cache file will be created once before every new release of `bat`.

### Troubleshooting

Make sure that the local cache does not interfere with the internally stored syntaxes and
themes (`bat cache --clear`).

### Manual modifications

The following files have been manually modified after converting from a `.tmLanguage` file:

* `Dart.sublime-syntax` => removed `#regex.dart` include.
* `INI.sublime-syntax` => added `.hgrc`, `hgrc`, and `desktop` file types.
* `Org mode.sublime-syntax` => removed `task` file type.

### Non-submodule additions

* `Assembly (x86_64)` has been manually added from https://github.com/13xforever/x86-assembly-textmate-bundle due to `git clone` recursion problems
