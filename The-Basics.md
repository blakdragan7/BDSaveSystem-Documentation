## Basic Types

### FScopedSaveGame (ScopedSaveGame in blueprints)

A FScopedSaveGame is an opaque struct that is used as a reference for a save game instance. It contains a "slot" and a "scope". "slots" are essentially the name of the save file used on disk. "scope" is a string that is used as a sub directory into that file. The combination of the two is used to uniquely identify save game data.

FScopedSaveGame's are backed by a custom USaveGame object that handles all the actual disk read and writes. So most concepts that apply to the default unreal save game system also apply here.

### UDSCSaveSystemModuleBlueprintLibrary

UDSCSaveSystemModuleBlueprintLibrary is a blueprint function library used to expose all of the functions required for FScopedSaveGame to blueprints. It is a static class that can be accessed from any blueprint.

### ADSCPlayerController (DSCPlayerController in blueprints)

ADSCPlayerController is a provided player controller that contains functions to save and load both player state and player pawn of the owning player. It is not required to use this class, but it is provided as a convenience. This player controller will automatically attempt to load the player state and pawn inside of `BeginPlay`

#### UpdateSaveCache

This function takes no arguments and will update the held save cache in memory for the current state of the controller pawn and player state.

#### SaveNow

This function takes one arguments and will save the cached state of the controller pawn and player state to disk. The arguments is a bool that if true, it will update the stored cache before saving to disk.

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

### Save Actor and Flush to Disk

[[/images/SaveActorExample.png|Save Actor Example Image]]

### Load Actor from Disk

[[/images/LoadActorExample.png|Load Actor Example Image]]

### Load and spawn actors from disk

[[/images/LoadAndSpawnActorsExample.png|Load and Spawn Actors Example Image]]