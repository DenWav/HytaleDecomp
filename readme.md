# Hytale Decompiled Sources

The Hytale server sources will be released eventually, but until then this is a small little script to make it easy to
decompile the Hytale server into a workable source tree.

## Info

Java 25 is required to run the setup script.

This script uses [VineFlower](https://vineflower.org/) as the decompiler – important note, VineFlower does not yet
reliably decompile `switch` blocks. VineFlower also does not decompile `assert` statements correctly. There is at least
one method that fails to decompile at all
(`com.hypixel.hytale.server.core.asset.type.blocktype.config.BlockPlacementSettings#toPacket()`).

The project structure is my best guess based on the Maven metadata available in the jar; I guarantee it's not right. In
particular, the exact mappings of classes and packages with each module is a best-guess. I already know that the `NPC`
module isn't right, it references the `Flock` plugin which it doesn't have access to in the current layout. Either the
`NPC` module is wrong, or the `Flock` plugin is wrong, or both.

I toyed with the idea of creating decompilation patches with this to make it compilable, but it just doesn't seem worth
it considering the full source release is coming anyway. So that said, this script will create a source tree that is
navigable, searchable, and most references will resolve, but it is _far_ from compilable.

The `poms` directory contains parent pom files that couldn't be extracted from the server jar. I put it together just to
tie the project structure together and make the Maven project resolve properly, it's not intended to replicate the
actual build logic. I tried naming them `p.xml` to stop IntelliJ from trying to pick them up as Maven built files, but
it still tries sometimes. Make sure you're importing `HytaleServer/pom.xml` once you've run the setup script.

## Usage:

In your shell, the `java` executable in your `PATH` (output of `java -veresion`) must be at least Java 25. The shebang in
the script will only work with Java 25 or greater.

Linux, macOS, and Windows:
```bash
./setup <path_to_HytaleServer.jar>
```

If Java 25 isn't in your `PATH` you can execute the script manually:
```bash
/path/to/jdk/25/bin/java --source 25 ./setup <path_to_HytaleServer.jar>
```

## License

The license is of course only for the `setup` script and does _not_ cover any of the decompiled sources.
