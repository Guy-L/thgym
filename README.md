# thgym - OpenAI Gym environment for Touhou

You can change the selected game in `interface.py` and change things like the reward method in `environment.py`.
Training a Reinforcement Learning agent with this is probably impossible with current techniques, but you're more than welcome to try.

TODO:
* Smarter implementation of the reset method
* Extracting more relevant game info: player coordinates, bullet coordinates list, enemy coordinates list...
* Adding parameters to select the observation space (single frame/buffer (with specific size), with/without game variables, with/without visual input...)
* Better documentation & code clean-up
* Re-write `interface.py` as a DLL for cleaner game interaction
* Custom policy for training with visual and game variable data
* Manage to train a model that at least learns not to bomb every other frame...
