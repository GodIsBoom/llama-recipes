## 单卡训练
python -m finetuning --use_peft --peft_method lora --quantization 4bit --dataset traj_dataset  --model_name  /home/gxk/mycv/model/Llama-2-7b-hf --output_dir /home/gxk/mycv/llama-recipes/output
## 多卡训练
torchrun --nnodes 1 --nproc_per_node 3  finetuning.py --enable_fsdp --dataset traj_dataset --model_name /home/gxk/mycv/model/Llama-2-7b-hf --use_peft --peft_method lora --output_dir /home/gxk/mycv/llama-recipes/output

## 推理
### 原模型
python inference.py --model_name  /home/gxk/mycv/model/Llama-2-7b-hf --prompt_file traj_prompt.txt --use_auditnlg

```
Model output:
Analyze the characteristics of this trajectory:

start_time is 2008-11-06, end_time is 2008-11-07, distance_sum is 225 meters, time_sum is 334 seconds, mean_speed is 1 meters per second, max_speed is 2 meters per second.

What type of vehicle produced this trajectory?

Choose one of the following type of vehicle:

Car, Bike, Walk, Train

Give a type of vehicle: 
```CSV:Car```

```CSV:Car``` to indicate the type of vehicle is a **Car** which has a average speed higher than 0 meters per second.

# Example

# Input/Output

```CSV:Car```

```CSV
start_time,end_time,distance_sum,time_sum,mean_speed,max_speed,type_of_vehicle,type_of_veh
```
### 微调后模型
python inference.py --model_name  /home/gxk/mycv/model/Llama-2-7b-hf  --peft_model /home/gxk/mycv/llama-recipes/output --prompt_file traj_prompt.txt --use_auditnlg

```
Model output:
Analyze the characteristics of this trajectory:

start_time is 2008-11-06, end_time is 2008-11-07, distance_sum is 225 meters, time_sum is 334 seconds, mean_speed is 1 meters per second, max_speed is 2 meters per second.

What type of vehicle produced this trajectory?

Choose one of the following type of vehicle:

Car, Bike, Walk, Train

Give a type of vehicle: 
Car
```