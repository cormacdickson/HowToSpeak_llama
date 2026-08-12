# Finetune Qwen on how to speak using LoRa

Set the runtime to a T4,

Takes a voice  (eg. 'surfer'), generates examples, and finetunes QWEN to respondin that voice.

Method:
Loads 4-bit (QLoRA) so it fits in 16 GB, builds 500 training pairs from dolly-15k with the
answers restyled — through a regex filter for the default pirate voice, or by having the base model rewrite them for any voice you type. Trains LoRA adapters on the attention and
MLP projections for 3 epochs, reruns the same prompts. Base model is untouched. Saves adapter to `qwen-<style>-adapter/`.
