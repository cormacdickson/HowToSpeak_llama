# Train Qwen on how to speak using LoRa

Set the runtime to a T4,

Method:
Loads 4-bit (QLoRA) so it fits in 16 GB, builds 500 training pairs from dolly-15k with the
answers put through a regex style filter. Trains LoRA adapters on the attention and
MLP projections for 3 epochs, reruns the same prompts, and toggles the adapter off
to show the base model is untouched. Saves the adapter to `qwen-<style>-adapter/`.
