## Basic Types

### FScopedSaveGame (ScopedSaveGame in blueprints)

An FScopedSaveGame is an opaque struct used as a reference for a save game instance. It contains a slot and a scope. Slots are essentially the name of the save file used on disk. Scope, is a string used as a subdirectory into that file.The combination of the two uniquely identify the save game data.

FScopedSaveGames' are backed by a custom USaveGame object that handles all the actual disk read and writes. So, most concepts that apply to the default unreal save game system also apply here.

To create a new scope, use `NewScopeLevel` function. This function takes a FScopedSaveGame and a scope. It will return a new FScopedSaveGame backed by the same USaveGame object as the parent. This new FScopedSaveGame will have the same slot as the parent, but will have the new scope. This concept allows for partitioning data, so saving and loading data is easy. For example, you can have a scope for the player state, and a scope for the player pawn. This way, you can load the player state and pawn separately without manually filter the data.

The default save path is in `{ProjectDir}/Saved/SaveGames/` just like the standard `USaveGame` system that comes with unreal.

### UDSCSaveSystemModuleBlueprintLibrary

UDSCSaveSystemModuleBlueprintLibrary is a blueprint function library used to expose all functions required for FScopedSaveGame to blueprints. It is a static class that is accessible from any blueprint.

### ADSCPlayerController (DSCPlayerController in blueprints)

ADSCPlayerController is a provided player controller that contains functions to save and load both player state and player pawn of the owning player. It is not required to use this class, but it is provided as a convenience. This player controller will automatically attempt to load the player state and pawn inside of `BeginPlay`

#### UpdateSaveCache

This function takes no arguments and will update the held save cache for the controller pawn and the player state's current state.

#### SaveNow

This function will save the current cache to disk. If the argument is true, it will update the cache before saving. 

### ADSCActorBase (DSCActorBase in blueprints)

ADSCActorBase is a convenience class that can be used to automatically save the entire scene component stack of this actor when saved with `WriteActor`. This included any dynamically added components (added at run-time) and even static mesh changes with custom material overrides. It is not required to use this class, but it is provided as a convenience.

## Writing Data

to add data to a save game, you must use the `WriteActor` function. This function takes an actor and a FScopedSaveGame. The actor is serialized into a byte array and stored in the save game object. By default, the actors' transform, class and name are stored. If more data is wanted then the property needs to be marked as a "save game" property. This can be done in the advanced menu in blueprints or by using the `SaveGame` specifier in C++. This can be used on any property that is serializable.

After writing all desired actors call `FlushSave` on the FScopedSaveGame to write the save game to disk.

## Getting Data

to get data from a save game, you must use the `LoadActorFromMemory` function. This function takes an actor and a FScopedSaveGame. The actor is deserialized from a byte array that is stored in the save game object. By default, the actors' transform, class and name are read. If more data is wanted then the property needs to be marked as a "save game" property. This can be done in the advanced menu in blueprints or by using the `SaveGame` specifier in C++. This can be used on any property that is serializable.

**It is important to load the actors from the save game in the exact order they are written to it. Otherwise, the wrong actor will be loaded and a crash can occur.**

If you want to load and spawn the actors saved then call `LoadActorsFromMemory` instead. It is recommend to have a different scope for actors that you want to also spawn at runtime to avoid loading the wrong actor.

## Example Usage

### Create a new scope from a save game

[[/images/NewScopeLevelExample.png|New Scope Level Example Image]]

### Save Actor and Flush to Disk

[[/images/SaveActorExample.png|Save Actor Example Image]]

### Load Actor from Disk

[[/images/LoadActorExample.png|Load Actor Example Image]]

### Load and spawn actors from disk

[[/images/LoadAndSpawnActorsExample.png|Load and Spawn Actors Example Image]]