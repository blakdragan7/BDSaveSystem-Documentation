## Start and Loads Saves
### Start Save to Slot
#### Description
Creates in memory or loads to memory a save game for slot name. 

#### Inputs
* *FString&* **Slot** - The name of the slot to create a save for
* *constant bool* **Attempt Load** - Wether or not to load a save game for given slot if one is found
#### Outputs
* *FScopedSaveGane* **OutSave** - The created or loaded save game 

[[/images/StartSaveToSlot.png|Start Save to Slot Image]]
### Load Save from Slot
#### Description
Load a given save into memory
#### Inputs
* *FString* **Slot** - Save to load 
#### Outputs
* *FScopedSaveGame* **OutSave** - The loaded save if succesful
* *bool* **Return Value** - True if save was found and loaded, false otherwise

[[/images/LoadSaveFromSlot.png|Load Save from Slot Image]]
### Flush Save
#### Description
Writes out save to disk.
#### Inputs
* *const FScopedSaveGame&* **Save** - The save game to write to disk
#### Outputs
* *bool* **Return Value** - Returns true when succesful or false otherwise

[[/images/FlushSave.png|Flush Save Image]]
### Remove Save Slot
#### Description
The deletes the save slot from disk with given slot name
#### Inputs
* *FString&* **Slot** - The slot name to delete
#### Outputs
* *bool* **Return Value** - Returns true when succesful or false otherwise

[[/images/RemoveSaveSlot.png|Remove Save Slot Image]]
## Writing / Getting Data
### Write Actor
#### Description
Addes given actors save data to the save game in memory
#### Inputs
* *FScopedSaveGame* **SaveGame** - The save game to write to
* *AActor* **Actor** - Actor To Write
#### Outputs
* *int32* **Return Value** - '-1' if the write failed or the index into the save game that represents this actor

[[/images/WiteActor.png|Write Actor Image]]
### New Scope Level
#### Description
Creates and returns a new scope from the given save game
#### Inputs
* *FScopedSaveGame* **Save Game** - The save game to create the scope from
* *FString* **Scope** - The scope level to append to the original scope 
#### Outputs
* *FScopedSaveGame* **Return Value** - The newly created save game with new scope

[[/images/NewScopeLevel.png|New Scope Level Image]]
### Load Actor From Memory
#### Description
Loads a given actor from memory, when multiple actors are stored in a particular cache the load order must be the exact same as the save order, as they are loaded and removed in the same order as they are read from disk
#### Inputs
* *FScopedSaveGame* **Save Game** - The save game to load from
* *AActor* **Actor** - The actor to load
#### Outputs
* *bool* **Return Value** - True if succesful

[[/images/LoadActorFromMemory.png|Load Actor From Memory Image]]
### Load Actors From Memory
#### Description
Loads and spawns all actors from a given save game that is already loaded into memory.
#### Inputs
* *FScopedSaveGame* **SaveGame** - The save game to load from
#### Outputs
* *TArray\<AActor\>* **Spawned Actors** - The spawned actors

[[/images/LoadActorsFromMemory.png|Load Actors From Memory Image]]
## Validation
### Is Valid
#### Description
Checks if given save game is valid
#### Inputs
* *FScopedSaveGame* **Save Game**
#### Outputs
* *bool* **Return Value** - whether or not the save game is valid
[[/images/IsValid.png|Is Valid Image]]
