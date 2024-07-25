python -m finetuning --use_peft --peft_method lora --quantization 4bit --dataset traj_dataset  --model_name  /home/gxk/mycv/model/Llama-2-7b-hf --output_dir /home/gxk/mycv/llama-recipes/output

torchrun --nnodes 1 --nproc_per_node 4  finetuning.py --enable_fsdp --model_name /home/gxk/mycv/model/Llama-2-7b-hf --use_peft --peft_method lora --output_dir /home/gxk/mycv/llama-recipes/output