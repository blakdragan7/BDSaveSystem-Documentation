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
Writes out save to disk.
#### Inputs
* *const FScopedSaveGame&* **Save** - The save game to write to disk
#### Outputs
* *bool* - Returns true when succesful or false otherwise

[[/images/LoadSaveFromSlot.png|Load Save from Slot Image]]
### Flush Save
[[/images/FlushSave.png|Flush Save Image]]
#### Description
#### Inputs
#### Outputs
### Remove Save Slot
#### Description
The deletes the save slot from disk with given slot name
#### Inputs
* *FString&* **Slot** - The slot name to delete
#### Outputs
* *bool* - Returns true when succesful or false otherwise

[[/images/RemoveSaveSlot.png|Remove Save Slot Image]]
## Witing / Getting Data
### Write Actor
#### Description
#### Inputs
#### Outputs
[[/images/WiteActor.png|Write Actor Image]]
### New Scope Level
#### Description
#### Inputs
#### Outputs
[[/images/NewScopeLevel.png|New Scope Level Image]]
### Load Actor From Memory
#### Description
#### Inputs
#### Outputs
[[/images/LoadActorFromMemory.png|Load Actor From Memory Image]]
### Load Actors From Memory
#### Description
#### Inputs
#### Outputs
[[/images/LoadActorsFromMemory.png|Load Actors From Memory Image]]
## Validation
### Is Valid
#### Description
#### Inputs
#### Outputs
[[/images/IsValid.png|Is Valid Image]]
