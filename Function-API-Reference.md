## Functions that Start and Load Saves
### "Start Save to Slot" Blueprint function
#### Description
This will create a save game object in memory or load from disk to memory for the given slot name.

#### Inputs
* *FString* **Slot** - The name of the slot used to create a save game. 
* *bool* **Attempt Load** - Whether or not to  attempt to load a save game for a specified slot, if one is found. If not, it will be created in memory. 
#### Outputs
* *FScopedSaveGame* **OutSave** - The created or loaded save game. 
* *bool* **Return Value** - The return value is True if OutSave was loaded or created successfully. This will be false otherwise.

[[/images/StartSaveToSlot.png|Start Save to Slot Image]]
### "Load Save from Slot" Blueprint function
#### Description
Load a given save into memory.
#### Inputs
* *FString* **Slot** - Save to load 
#### Outputs
* *FScopedSaveGame* **OutSave** - The loaded save if successful.
* *bool* **Return Value** - True if save was found and loaded, false otherwise

[[/images/LoadSaveFromSlot.png|Load Save from Slot Image]]
### ""Flush Save" Blueprint function
#### Description
Writes out save to disk.
#### Inputs
* *FScopedSaveGame* **Save** - The save game to write to disk
#### Outputs
* *bool* **Return Value** - Returns true when successful or false otherwise

[[/images/FlushSave.png|Flush Save Image]]
### "Remove Save Slot" Blueprint function
#### Description
The deletes the save slot from disk with given slot name
#### Inputs
* *FString* **Slot** - The slot name to delete
#### Outputs
* *bool* **Return Value** - Returns true when successful or false otherwise

[[/images/RemoveSaveSlot.png|Remove Save Slot Image]]
## Functions that Write / Get Data
### "Write Actor" Blueprint function
#### Description
Adds given actor's save data to the save game in memory
#### Inputs
* *FScopedSaveGame* **SaveGame** - The save game to write to
* *AActor* **Actor** - Actor To Write
#### Outputs
* *int32* **Return Value** - '-1' if the write failed or the index into the save game that represents this actor

[[/images/WiteActor.png|Write Actor Image]]
### "New Scope Level" Blueprint function
#### Description
Creates and returns a new scope from the given save game
#### Inputs
* *FScopedSaveGame* **Save Game** - The save game to create the scope from
* *FString* **Scope** - The scope level to append to the original scope 
#### Outputs
* *FScopedSaveGame* **Return Value** - The newly created save game with new scope

[[/images/NewScopeLevel.png|New Scope Level Image]]
### "Load Actor From Memory" Blueprint function
#### Description
Loads a given actor from memory, when multiple actors are stored in a particular cache the load order must be the exact same as the save order, as they are loaded and removed in the same order as they are read from disk
#### Inputs
* *FScopedSaveGame* **Save Game** - The save game to load from
* *AActor* **Actor** - The actor to load
#### Outputs
* *bool* **Return Value** - True if successful

[[/images/LoadActorFromMemory.png|Load Actor From Memory Image]]
### "Load Actors From Memory" Blueprint function
#### Description
Loads and spawns all actors from a given save game that is already loaded into memory.
#### Inputs
* *FScopedSaveGame* **SaveGame** - The save game to load from
#### Outputs
* *TArray\<AActor\>* **Spawned Actors** - The spawned actors

[[/images/LoadActorsFromMemory.png|Load Actors From Memory Image]]
## Validation Functions
### "Is Valid" Blueprint function
#### Description
Checks if given save game is valid
#### Inputs
* *FScopedSaveGame* **Save Game**
#### Outputs
* *bool* **Return Value** - whether or not the save game is valid

[[/images/IsValid.png|Is Valid Image]]
