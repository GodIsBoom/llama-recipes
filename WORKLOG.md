## 单卡训练
python -m finetuning --use_peft --peft_method lora --quantization 4bit --dataset traj_dataset  --model_name  /home/gxk/mycv/model/Llama-2-7b-hf --output_dir /home/gxk/mycv/llama-recipes/output
## 多卡训练
torchrun --nnodes 1 --nproc_per_node 3  finetuning.py --enable_fsdp --dataset traj_dataset --model_name /home/gxk/mycv/model/Llama-2-7b-hf --use_peft --peft_method lora --output_dir /home/gxk/mycv/llama-recipes/output

## 推理
### 原模型
python inference.py --model_name  /home/gxk/mycv/model/Llama-2-7b-hf --prompt_file traj_prompt.txt --use_auditnlg
### 微调后模型
python inference.py --model_name  /home/gxk/mycv/model/Llama-2-7b-hf  --peft_model /home/gxk/mycv/llama-recipes/output --prompt_file traj_prompt.txt --use_auditnlg