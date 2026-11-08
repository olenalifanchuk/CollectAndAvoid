# Collect and Avoid



## Project Details

* **Engine Version:** 5.8.4

* **Version Control:** Git LFS is used to track and store all `.uasset` and `.umap` binary files.

* **Performance Note:** Editor scalability settings were lowered to 'Medium'.


## Controls

* **W, A, S, D:** Move
* **Shift:** Sprint
* **Space:** Jump
* **Esc:** Pause


## How to run the packaged build

1. Download the `CollectAndAvoid_Build.zip` archive using the Google Drive link https://drive.google.com/drive/folders/1EPNUUzE6DGPopmDZPQ8MCaljuqZvGArF?hl=uk-UA .
2. Extract the downloaded `.zip` archive to any folder on your PC.
3. Open the extracted folder and navigate into the `Windows` folder.
4. Double-click the `CollectAndAvoid.exe` file to start the game.


## Blueprints Description

* **BP_Hero:** The main player character. Handles camera rotation, basic movement, jumping, sprinting, initializing the HUD on Begin Play, and toggling the Pause menu.
* **BP_Enemy:** The AI enemy character. Sets its movement speed on BeginPlay and uses `OnComponentHit` to detect collisions with the player. When it catches the player, it updates the GameMode state to 'Lost', spawns the Game Over widget, adds camera shake, and pauses the game.
* **BP_Coin:** The collectible item. Detects player overlap to increase the score, updates the HUD, plays audio/visual effects, and destroys itself. It also checks if the target score is reached to display the Win screen.
* **BP_GameMode:** Acts as the central data manager. It holds the variables for the current score, the target score (8 coins), and the current game state, which are updated via Casts from other actors.
* **BP_EnemyAIController:** Handles the AI Perception (sight). When it sees the player, it updates the Blackboard variables (`CanSeePlayer` and `TargetActor`) to start chasing and plays an alert sound.
* **BTT_FindPatrolPoint:** A custom Behavior Tree Task. It gets the array of patrol points from `BP_Enemy`, picks a random one, and sets its location in the Blackboard for the AI to move to.
* **UI Widgets (WBP_HUD, WBP_Lose, WBP_Pause, WBP_Win):** User interface elements that display the current score during gameplay and handle the interactive screens for pausing, winning, and losing the game.


## Character Movement Changes

* **Max Walk Speed:** 600 -> 550

* **Jump Z Velocity:** 500 -> 600

* **Air Control:** 0.35 -> 0.5


## Why the Cast check is needed for the Coin?

The `Cast to BP_Hero` node is strictly necessary to verify the identity of the actor touching the coin.


## UI Optimization:

The HUD score is updated via a custom function only when a coin is collected. Per-frame property bindings were avoided because they evaluate the value every frame, which wastes CPU performance.

## Asset List

* **Audio sources:** Free sound effects from https://mixkit.co/ (Mixkit Free License).

* **Environment Assets:** Level arena built using standard Unreal Engine basic geometric shapes.


## Profiling and Optimization

During profiling with `stat fps` and `stat unit` on Medium scalability, my frame time was ~33ms (running at 30 FPS). The most expensive items were the `Draw` thread and `GPU Time` (~33ms). The `Game` thread was running faster (~22ms). This proves that my Blueprint logic is optimized. I do not use `Get All Actors of Class` or any heavy logic on `Event Tick`. The slight bottleneck is purely graphical rendering, not the code.


## Known Bugs

* None observed during the final playtest. Everything works as intended.


## What I learned and what was hard

As this was my very first experience with both Unreal Engine 5 and Git, it was quite challenging for me at first. I learned the fundamentals of version control, such as creating a repository, staging, committing, and pushing code. I also built my first 3D game in Unreal Engine, learning level layout, placing actors, and logic building using visual node-based Blueprint scripts. 

The hardest part was working without step-by-step instructions for every feature. Understanding the core logic of my first Blueprints, connecting nodes correctly, managing executable wires, and troubleshooting unexpected errors required a lot of independent problem-solving and research. Despite these challenges, overcoming these roadblocks gave me a solid foundation in engine workflows and Blueprint logic.

