## So, you want to create a VS2 addon?

### Well, here is the template for you!

__This template's dependencies include:__
- Architectury API (*its easier than the weird custom services Eureka uses*)
- Valkyrien Skies 2
- VS Core
- Kotlin for Forge

### How to use this template

While this template is technically functional as-is, you will probably want to
refactor some things (Usually at least namespace and modid). 
Below is a full list of what you will need to refactor.

<details open>
<summary>The great refactoring</summary>

#### In Root:

1. Change the `gradle.properties`. You probably want to change:
   - `mod_name`
   - `mod_id`
   - `mod_version`
   - `mod_description`
   - `mod_license`
   - `mod_author`
   - `homepage`
   - `sources`
   - `issue_tracker`
   - `archives_base_name`
   - `maven_group`
   
   Don't change other properties unless you know what you are doing, as it could break the gradle setup. 
2. Change `rootProject.name` in `settings.gradle.kts`
3. If you want the github "build and test" action to work, you will need to run the following commands to grant it permission:
   ```Bash
   git update-index --chmod=+x gradlew
   git commit -m "Make gradlew executable"
   ```

#### In Common:

1. The `kotlin` packages (e.g. `io.github.techtastic.vs_addon_template` -> `com.my.namespace.modid`)
2. The `kotlin` main class filename (e.g. `VSAddonTemplateMod` -> `MyVSMod`)
3. The const `MOD_ID` in the main mod class
3. The architectury config (`resources/architectury.common.json`) access widener path
4. The access widener filename (`resources/vs_addon_template.accesswidener`)
5. The `accessWidenerPath` set in the `build.gradle`
6. With the mixin config (`resources/vs_addon_template-common.mixins.json`) you should change
   - The filename
   - The `package` (doesn't have to exist, but should be your namespace)

#### In Fabric:

1. The `kotlin` packages (note that they must end with a `fabric` package)
2. The `kotlin` main class filename (must be the same as the **common** main class, with `Fabric` on the end)
3. With the mixin config (`resources/vs_addon_template.mixins.json`) you should change
   - The filename
   - The `package` (doesn't have to exist, but should be your namespace, and should end in `.fabric.mixin`)
5. The `fabric.mod.json`
   - In `entrypoints`, the packages of `main`, `client` and `preLaunch`.
   - The `client` entrypoint should be your `main` entrypoint, but with `${'$'}Client` on the end
   - In `mixins`, the filename of the **common** and **fabric** mixin configs
6. The icon file (`resources/assets/vs_addon_template/icon.png`)

#### In Forge:
1. The `kotlin` packages (note that they must end with a `forge` package)
2. The `java` packages, with it ending in `.forge.mixin` with the `...ForgeMixinConfigPlugin` class
3. The `kotlin` main class filename (must be the same as the **common** main class, with `Forge` on the end)
4. With the mixin config you should change
   - The filename
   - The `package` value (ending in `.forge.mixin`)
   - The `plugin` value (pointing to the mixin plugin class in the `java` packages)
5. The `build.gradle`, in the `loom { forge { ` section, the `mixinConfig`
   filenames for the **fabric** and **common** mixin configs
6. The icon file (`resources/icon.png`)

</details>

