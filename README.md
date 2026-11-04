# Collect and Avoid



## Engine Version: 5.8.4

## Performance Note

Editor scalability settings were lowered to 'Medium'

## Version Control

Git LFS is used to track and store all `.uasset` and `.umap` binary files.


## Character Movement Changes

* **Max Walk Speed:** 600 -> 550

* **Jump Z Velocity:** 500 -> 600

* **Air Control:** 0.35 -> 0.5


## Why the Cast check is needed for the Coin?

The `Cast to BP_Hero` node is strictly necessary to verify the identity of the actor touching the coin.
