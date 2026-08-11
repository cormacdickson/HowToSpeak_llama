# How to speak with LoRa

fine-tune `Qwen2.5-1.5B-Instruct` with LoRA to speak in a given style.

Set the runtime to a T4,

Method:
Loads 4-bit (QLoRA) so it fits in 16 GB, records baseline answers
to four fixed prompts, then builds 500 training pairs from dolly-15k with the
answers put through a regex style filter. Trains LoRA adapters on the attention and
MLP projections for 3 epochs, reruns the same prompts, and toggles the adapter off
to show the base model is untouched. Saves the adapter to `qwen-<style>-adapter/`.


## Loading the saved adapter
```python
from peft import PeftModel
from transformers import AutoModelForCausalLM

base = AutoModelForCausalLM.from_pretrained("Qwen/Qwen2.5-1.5B-Instruct", device_map="auto")
model = PeftModel.from_pretrained(base, "qwen-pirate-adapter")  # or whatever style you trained
```
