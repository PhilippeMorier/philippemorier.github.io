---
title: Tree Generation
definition: Procedural generation of trees
tags: procedural generation tree model realistic creation rendering
---

## Parametric Approaches

### Weber and Penn

[Creation and Rendering of Realistic Trees](https://www2.cs.duke.edu/courses/cps124/fall01/resources/p119-weber.pdf)

### Charlie Hewitt's adaption of Weber and Penn

[Procedural generation of tree models for use in computer graphics](https://chewitt.me/Papers/CTH-Dissertation-2017.pdf)

- [friggog/tree-gen](https://github.com/friggog/tree-gen)
- [tree-get wiki](https://github.com/friggog/tree-gen/wiki)

  - [Tree Parameters](https://github.com/friggog/tree-gen/wiki/Tree-Parameters)
  - [Branch-Parameters](https://github.com/friggog/tree-gen/wiki/Branch-Parameters)
  - [Leaf-Parameters](https://github.com/friggog/tree-gen/wiki/Leaf-Parameters)

#### Add repo (which is an addon) to Blender

1. clone repo
2. copy `ch_trees` folder to `~/.config/blender/2.82/scripts/addons`
3. In Blender open: File -> User Preferences -> Add-ons
   1. Community (Tab) -> Filter: Object -> Object: TreeGen
   2. Activate Sidebar: View -> Sidebar OR with shortcut key `N`
4. Open `~/.config/blender/2.82/scripts/addons/ch_blender` in IDE
5. Make changes in IDE
6. Swap to Blender and hit `F8` to refresh the add-ons

#### Other Blender Plugin based on Weber & Penn

[Sapling Tree Gen](https://docs.blender.org/manual/en/latest/addons/add_curve/sapling.html)
[abpy/improved-sapling-tree-generator](https://github.com/abpy/improved-sapling-tree-generator)
