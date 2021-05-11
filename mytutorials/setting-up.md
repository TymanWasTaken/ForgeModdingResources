# How to set up the forge development workspace
(this is mostly for 1.8.9 but may work for other things)

1. Go to http://files.minecraftforge.net/ and download the MDK for your desired Minecraft version and forge version.
2. Unzip the downloaded file into the directory where you want your mod's code to be.
3. (Optional) Delete the unnecessary .txt files, they are not needed for development.

## The following is different depending on IDE

### Intellij IDEA

### Import project
1. Open Intellij and click open project.
2. Navigate to your project's build.gradle (in the folder you just unzipped) and double click it. When it asks you if you want to import as a project, select yes.
3. Wait for Intellij to import the project. (it will likely ask you to update gradle, just click on the blue text and it auto-updates for you)

#### Fix gradle
Recent changes by forge have broken gradle, so you will need to fix this before being able to use it.
To fix it, just do what this says: https://gist.github.com/asbyth/ba2cd9b66925f2437bbcfcd884d60af7.

#### Set up minecraft decompilation
Once imported, open the gradle sidebar (hover over the symbol in the bottom left) and run `setupDecompWorkspace` in the forgegradle folder.
This will likely take a few minutes, as it has to decompile minecraft.

#### Optional: Setup runs
This step will allow you to start minecraft from Intellij and allow you to test easier.
1. Locate the `genIntellijRuns` task in the gradle sidebar, and run it.
2. Click the dropdown menu seen below, and select edit configurations.<br>
![Image of the dropdown](https://media.discordapp.net/attachments/792642646907945000/797142149099552778/unknown.png)
3. Select the new "Minecraft Client" run from the menu and change the `-cp` dropdown to `.main` as seen below.<br>
![Image of the dropdown](https://media.discordapp.net/attachments/792642646907945000/797142288056451082/unknown.png)
4. (Optional) If you want to be able to use your account for testing, you need to do the following.
    1. Click expand on the program arguments.<br>
    ![Image of the program arguments field](https://media.discordapp.net/attachments/792642646907945000/797142652394274866/unknown.png)
    2. Add the `--username` and `--password` arguments, as seen below.<br>
    ![Image of arguments](https://media.discordapp.net/attachments/792642646907945000/797142663080968222/unknown.png)
5. Save the run.

### Eclipse
To be totally honest, I don't even remember how to do it so this may not be entirely correct <sub><sup>Intellij is better in my opinion anyway<sup><sub>
1. Open Eclipse and open the folder you just unzipped as a project
2. Open powershell/cmd/bash (whatever form of terminal you prefer), navigate to your project directory (likely using `cd path/to/project`)
3. Run `./gradlew setupDecompWorkspace` (This will likely take a few minutes, as it has to decompile minecraft.)
4. After that is done, run `./gradlew eclipse` to set up for eclipse.

## Next steps

The MDK has default folders and directories to help you get started. You should rename these to fit your mod. The mdk contains the package `com.example.examplemod` and an `ExampleMod.java` file. It is recommended to rename this with the scheme `topleveldomain.name.modid` (for example `com.tyman.coolmod`). You should also rename the ExampleMod file to fit your mod. Inside the newly renamed file, edit the modid and version string to your needs.

Next is the build.gradle file in the root of your project. This is where you need to specify your package name, modid, and version. You should edit the following values as so: 
```groovy
version = "Mod version"
group = "Package name" 
archivesBaseName = "Mod id"
```

## Optional but recommended steps

In your build.gradle file, there are two optional things you can change. 
1. The first is the `mappings = "stable_20"` line in the `minecraft` block (this is only applicable for the 1.8.9 mdk). These mappings were designed for 1.8.8, so it is recommended to update them for 1.8.9. You can do this by changing `stable_20` to `stable_22`.
2. The second is the `makeObfSourceJar = false` line. It is in a comment by default, and if it is kept in a comment, will make building your mod create a second file, `modid-version-sources.jar` allong with the normal `modid-version.jar` file. This extra file is simply your normal mod jar file, but includes the source code too. If you do not need this, uncomment the `makeObfSourceJar = false` line.

<br><br><br>

You now have your project set up, you just need to make the mod itself.
