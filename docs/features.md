# Cats Blender Plugin — Feature Reference

## Model

![](https://i.imgur.com/dYYAfb4.png)

This tries to completely fix your model with one click.

##### Import/Export Model
- Imports a model of the selected type with the optimal settings
- Exports a model as an .fbx with the optimal settings

##### Fix Model
- Fixes your model automatically by:
  - Reparenting bones
  - Removing unnecessary bones
  - Renaming and translating objects and bones
  - Mixing weight paints
  - Rotating the hips
  - Joining meshes
  - Removing rigidbodies, joints and bone groups
  - Removing bone constraints
  - Deleting unused vertex groups
  - Using the correct shading
  - Making it compatible with Full Body Tracking
  - Combining similar materials

##### Start Pose Mode
- Lets you test how bones will move.

##### Pose to Shape Key
- Saves your current pose as a new shape key.

##### Apply as Rest Pose
- Applies the current pose position as the new rest position. This saves the shape keys and repairs ones that were broken due to scaling


## Model Options

![](https://i.imgur.com/ZPj2VUJ.png)

##### Translation
- Translate certain entities from any japanese to english. This uses an internal dictionary and Google Translate.

##### Separate by material / loose parts / shapes
- Separates a mesh by materials or loose parts or by whether or not the mesh is effected by a shape key

##### Join meshes
- Joins all/selected meshes together

##### Merge Weights
- Deletes the selected bones and adds their weight to their respective parents

##### Delete Zero Weight Bones
- Cleans up the bones hierarchy, deleting all bones that don't directly affect any vertices

##### Delete Constraints
- Removes constrains between bones causing specific bone movement as these are not used by VRChat

##### Recalculate Normals
- Makes normals point inside of the selected mesh
- Don't use this on good looking meshes as this can screw them up

##### Flip Normals
- Flips the direction of the faces' normals of the selected mesh.

##### Apply Transformations
- Applies the position, rotation and scale to the armature and its meshes.

##### Remove Doubles
- Merges duplicated faces and vertices of the selected meshes.


## Custom Model Creation

![](https://i.imgur.com/szIWglS.png)
![](https://i.imgur.com/04O63q1.png)

**This makes creating custom avatars a breeze!**

##### Merge Armatures
- Merges the selected armature into the selected base armature.
- **How to use:**
  - Use "Fix Model" on both armatures
    - Select the armature you want to fix in the list above the Fix Model button
    - Ignore the "Bones are missing" warning if one of the armatures is incomplete (e.g hair only)
    - If you don't want to use "Fix Model" make sure that the armature follows the CATS bone structure (https://i.imgur.com/F5KEt0M.png)
    - DO NOT delete any main bones by yourself! CATS will merge them and delete all unused bones afterwards
  - Now you have two options:
    - Only move the mesh:
      - Uncheck the checkbox "Apply Transforms"
      - Move the mesh (and only the mesh!) of the merge armature to the desired position
        - You can use Move, Scale and Rotate
        - CATS will position the bones according to the mesh automatically
    - OR move the armature (and with it the mesh):
      - Check the checkbox "Apply Transforms"
      - Move the armature to the desired position
        - You can use Move, Scale and Rotate
        - Make sure that both meshes and armatures are at their correct positions as they will stay exactly like this
    - If you want to merge multiple objects from the same model it is often better to duplicate the armature for each of them and merge them individually
  - Select the base armature and the armature you want to merge into the base armature in the panel
  - If CATS can't detect the bone structure automatically: select a bone you want to attach the new armature to
    - E.g.: For a hair armature select "Head" as the bone
  - Press the "Merge Armatures" button -> Done!

##### Attach Mesh to Armature
- Attaches the selected mesh to the selected armature.
- **How to use:**
  - Move the mesh to the desired position
    - You can use Move, Scale and Rotate
    - INFO: The mesh will only be assigned to the selected bone
    - E.g.: A jacket won't work, because it requires multiple bones.
    - E.g.: A ring on a finger works perfectly, because the ring only needs one bone to move with (the finger bone)
  - Select the base armature and the mesh you want to attach to the base armature in the panel
  - Select the bone you want to attach the mesh to in the panel
  - Select the bone you want to attach the mesh to in the panel
  - Press the "Attach Mesh" button -> Done!


## Decimation

![](https://i.imgur.com/5u3teLp.png)

**Decimate your model automatically.**

##### Smart Decimation
- This will decimate all meshes while keeping every shapekey.

##### Save Decimation
- This will only decimate meshes with no shape keys.

##### Half Decimation
- This will only decimate meshes with less than 4 shape keys as those are often not used.

##### Full Decimation
- This will decimate your whole model deleting all shape keys in the process.

##### Custom Decimation
- This lets you choose the meshes and shape keys that should not be decimated.


## Eye Tracking

![](https://i.imgur.com/yw8INDO.png)
![](https://i.imgur.com/VHw73zM.png)

**Eye tracking is used to artificially track someone when they come close to you.**
It's a good idea to check the eye movement in the testing tab after this operation to check the validity of the automatic eye tracking creation.

##### Disable Eye Blinking
- Disables eye blinking. Useful if you only want eye movement.

##### Disable Eye Movement
- Disables eye movement. Useful if you only want blinking. **IMPORTANT:** Do your decimation first if you check this!

##### Eye Movement Speed
- Configure eye movement speed


## Visemes (Lip Sync)

![](https://i.imgur.com/muM2PTS.png)

**Mouth visemes are used to show more realistic mouth movement in-game when talking over the microphone.**
The script generates 15 shape keys from the 3 shape keys you specified. It uses the mouth visemes A, OH and CH to generate this output.


## Bone parenting

![](https://i.imgur.com/mgadT4R.png)

**Useful for Dynamic Bones where it is ideal to have one root bone full of child bones.**
This works by checking all bones and trying to figure out if they can be grouped together, which will appear in a list for you to choose from. After satisfied with the selection of this group you can then press 'Parent bones' and the child bones will be parented to a new bone named RootBone_xyz

##### To parent
- List of bones that look like they could be parented together to a root bone. Select a group of bones from the list and press "Parent bones"

##### Refresh list
- Clears the group bones list cache and rebuild it, useful if bones have changed or your model

##### Parent bones
- Starts the parent process


## Texture atlas

![](https://i.imgur.com/XcoF0Ek.png)

**Texture atlas is the process of combining multiple textures into one to drastically reduce draw calls and therefore make your model much more performant**

##### Create Atlas
- Combines all selected materials into one texture. If no material list is generated it will combine all materials.

##### Generate Material List
- Lists all materials of the current model and lets you select which ones you want to combine.

### Useful Tips
- Split transparent and non-transparent textures into separate atlases to avoid transparency issues
- Make sure that the created textures are not too big, because Unity will downscale them to 2048x2048. Split them across multiple atlases or reduce the individual texture sizes. This can be easily done in the MatCombiner tab.
- You can tell Unity to use up to 8k textures. Do so by selecting the texture and then choose a different Max Size and/or Compression in the inspector: https://i.imgur.com/o01T4Gb.png


## Bone merging

![](https://i.imgur.com/FXwOvho.png)

**Lets you reduce overall bone count in a group set of bones.**
This works by checking all bones and trying to figure out if they can be grouped together, which will appear in a list for you to choose from. After satisfied with the selection of this group you can then set a percentage value how much bones you would like to merge together in itself and press 'Merge bones'

##### Refresh list
- Clears the group bones list cache and rebuild it, useful if bones have changed or your model

##### Merge bones
- Starts the merge process


## Bake

![](https://user-images.githubusercontent.com/1109288/97830517-147d1500-1c82-11eb-8b20-feba732ad672.png)<img src="https://cdn.discordapp.com/attachments/790488253764730920/791146826774216744/unknown.png" height="735" />

**This is a non-destructive way to instantly produce a optimized/Quest variant of (almost) any avatar!**

For more information please visit the **[Bake Panel Wiki Page](https://github.com/GiveMeAllYourCats/cats-blender-plugin/wiki/Bake)**.


## Shape Key

![](https://i.imgur.com/LgFK4KO.png)

**Apply Shape Key as Basis**
- Applies the selected shape key as the new Basis and creates a reverted shape key from the selected one.


## Settings and Updates

![](https://i.imgur.com/hYy7gD8.png)

**This plugin has an auto updater.** It checks for a new version automatically once every day.
