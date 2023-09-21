
## The Basics of Custom Loading

It's possible to customize how actors are serialized into the save system. This is done through C++. It is not currently possible to do this through Blueprints as it is a limitation of the built in save system or unreal.

## C++ Setup

Inside of your actors header file, you need to add the following function override:

```cpp
virtual void Serialize(FArchive& Ar) override;
```

When an actor is serialized into the DSC save system Serialize is called on each actor. The FArchive passed in is a custom implementation for DSC, however, it is a child of the standard FArchive. This means that you can use the standard FArchive functions to serialize your data. For example, if you have a variable called "MyInt" that you want to save, you can do the following:

```cpp
void MyActor::Serialize(FArchive& Ar)
{
    Super::Serialize(Ar);

    // note this handles both saving and loading MyInt
    Ar << MyInt;
}
```

In practice you should prefer to use `SaveGame` attribute for something as simple as an int32. However, this is useful for something like child actors. For example, if you have a child actor that you want to save / load as a part of another actors serialization, you can do the following:

```cpp
void MyActor::Serialize(FArchive& Ar)
{
    Super::Serialize(Ar);

    // we need to have a variable to hold the child actor because << operator
    // handles both saving and loading, so it must be a modifiable. 
    AActor* ChildActor = MyChildActorComponent->GetChildActor();
    Ar << ChildActor;
}
 ```

If you want to spawn the child actor, you can do the following:

 ```cpp
 void MyActor::Serialize(FArchive& Ar)
 {
    Super::Serialize(Ar);
    // this will both save and load the child actor class, depending on if the 
    // archive is loading or saving
    Ar << ChildActorClass = ChildActor->GetChildActorClass();
    if (Ar.IsLoading())
    {
        // this will spawn the child actor
        MyChildActorComponent->SetChildActorClass(ChildActorClass);
        MyChildActorComponent->CreateChildActor();
        AActor* ChildActor = MyChildActorComponent->GetChildActor();

        // this will load the spawned child actor from the archive
        Ar << ChildActor;
    } 
    else
    {
        AActor* ChildActor = MyChildActorComponent->GetChildActor();
        Ar << ChildActor;
    }
}
```

## Saving Custom Structs

You can use `<<` operator on the FArchive for any built in data type for unreal. For example, you can use it for `FVector`, `FTransform`, `FColor`, etc. However, if you want to save a custom struct, you need to define the `<<` operator for that struct. For example, if you have a struct called `MyExampleStruct` defined like this

```cpp
struct MyExampleStruct
{
    int32 MyInt;
    float MyFloat;
    FString MyString;
};
```

you would need to define the following function

```cpp
inline FArchive &operator <<(FArchive & Ar,MyExampleStruct & Sd)
{
    Ar << Sd.MyInt;
    Ar << Sd.MyFloat;
    Ar << Sd.MyString;

    return Ar;
}
```

This would allow you to use the `<<` operator on `MyExampleStruct` in the `Serialize` function. For example:

```cpp

void MyActor::Serialize(FArchive& Ar)
 {  
    Super::Serialize(Ar);
    // this both read and writes St to Ar depending on if Ar is loading or saving
    MyExampleStruct St;
    Ar << St;
 }

```

## Important Notes

* You should always call `Super::Serialize(Ar)` before you do any custom serialization. This is because the default implementation of `Serialize` for `AActor` handles some default saving and loading behaviors that need to happen.
* Never try to save any objects of type TObjectPtr<>, TWeakObjPtr, TSharedPtr etc.. Instead you should get the raw pointer from these objects and save that directly. For example:

```cpp
void MyActor::Serialize(FArchive& Ar)
{
    Super::Serialize(Ar);

    // this will work fine
    UObject* object = MyObjectPtr.Get();
    Ar << object;

    // this will cause a crash on load
    Ar << MyObjectPtr;
}
```
