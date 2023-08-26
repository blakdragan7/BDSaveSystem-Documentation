# Dynamic Scene Component - Save & Load 

Dynamic Scene Component - Save & Load is an unreal code plugin that allows for dynamically saving and loading complex blueprint structures that are created at runtime. This means that even components that are added or modified after the level has started will be saved and load correctly. All template components, like those added in the editor so not at runtime, will also work perfectly with this system. This is great if you are tired of having a million different structs for custom data involving procedural components. This plugin was made to handle saving and loading of any instance scene components, even if they are added at runtime (via `NewObject` and `AttatchComponent`) 

Dynamic Scene Component - Save & Load is not designed to be an "all in one save", but will make procedurally generated actors with procedural components, easy to save and load. Without having to use a million different custom structs for saving and loading such data. If you want to add custom data (like none UStruct data) then you need some level of C++ knowledge. 

## Technical Details
### Basic Features
* Save and load any UObject or UStruct based data from blueprints or C++
* Easily extend what gets saved via C++ by overriding Serialize on the Class 
* Blueprint compatible. So you can save and load from within blueprints
* SaveGame Attribute compatible, so marking a property as SaveGame will automatically make it get saved assuming the actor or object is saved
### Advanced Features
* DSCPlayerController class provided for automatic saving & loading of player data.
* Automatically save & load dynamically created scene components.
* Automatically save & load modified static mesh components, so any custom material or mesh modified at runtime will be kept
