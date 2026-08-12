# Train Qwen on how to speak using LoRa

Set the runtime to a T4,

The first cell asks how you want the model to speak. Type any voice ("a Victorian butler",
"an over-caffeinated surfer"), or press Enter for the default pirate.

Method:
Loads 4-bit (QLoRA) so it fits in 16 GB, builds 500 training pairs from dolly-15k with the
answers restyled — through a regex filter for the pirate, or by having the base model
rewrite them for any voice you type. Trains LoRA adapters on the attention and
MLP projections for 3 epochs, reruns the same prompts, and toggles the adapter off
to show the base model is untouched. Saves the adapter to `qwen-<style>-adapter/`.
