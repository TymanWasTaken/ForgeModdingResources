# How to set up the forge development workspace
(this is mostly for 1.8.9 but may work for other things)

Download https://github.com/romangraef/Forge1.8.9Template for an updated template.

## The following is different depending on IDE

### Intellij IDEA

### Import project
1. Open Intellij and click open project.
2. Navigate to your project's build.gradle (in the folder you just unzipped) and double click it. When it asks you if you want to import as a project, select yes.
3. Wait for Intellij to import the project. (it will likely ask you to update gradle, just click on the blue text and it auto-updates for you)
4. In the gradle tab configure your Gradle settings to use Java 17. If you don't have Java 17 already downloaded you can download it using the "Download JDK" button. <br>
![Image of the settings button](https://cdn.discordapp.com/attachments/832652653292027904/1056281324761120768/image.png)
 
![image](https://user-images.githubusercontent.com/91034467/209448176-58f8adbe-1d23-40df-863a-3d7853b977b2.png)

5. In your project structure set your SDK to 8, as well as your language level to 8. To open project structure press [Ctrl (CMD if mac) + Alt + Shift + S]. <br>
![image](https://user-images.githubusercontent.com/91034467/209448203-02700c47-4515-4098-ae54-a6f37f9effc7.png) <br>
Make sure to select the project tab. <br>
![image](https://user-images.githubusercontent.com/91034467/209448201-7cac2fb2-98ab-42ac-be3c-631cd51dc250.png) <br>


#### Optional: Setup runs
This step will allow you to start minecraft from Intellij and allow you to test easier.
1. Locate the `genIntellijRuns` task in the gradle sidebar, and run it.
![Image of the dropdown](https://media.discordapp.net/attachments/792642646907945000/797142149099552778/unknown.png)
2. (Optional) If you want to be able to use your account for testing, you need to follow https://github.com/DJtheRedstoner/DevAuth. DevAuth comes pre installed in the template.
3. (Applicable only if doing 2nd step) Save the run.


### Eclipse
To be totally honest, I don't even remember how to do it so this may not be entirely correct <sub><sup>Intellij is better in my opinion anyway<sup><sub>
1. Open Eclipse and open the folder you just unzipped as a project
2. Open powershell/cmd/bash (whatever form of terminal you prefer), navigate to your project directory (likely using `cd path/to/project`)
3. Run `./gradlew setupDecompWorkspace` (This will likely take a few minutes, as it has to decompile minecraft.)
4. After that is done, run `./gradlew eclipse` to set up for eclipse.

## Next steps

The template has default folders and directories to help you get started. You should rename these to fit your mod. The mdk contains the package `com.example.examplemod` and an `ExampleMod.java` file. It is recommended to rename this with the scheme `topleveldomain.name.modid` (for example `com.tyman.coolmod`). You should also rename the ExampleMod file to fit your mod. Inside the newly renamed file, edit the modid and version string to your needs.

Next is the build.gradle file in the root of your project. This is where you need to specify your package name, modid, and version. You should edit the following values as so: 
```groovy
version = "Mod version"
group = "Package name" 
archivesBaseName = "Mod id"
```

<br><br><br>

You now have your project set up, you just need to make the mod itself.
