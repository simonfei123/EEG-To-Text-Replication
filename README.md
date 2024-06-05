# what's new?
updated full paper of this issue on [https://arxiv.org/abs/2405.06459](https://arxiv.org/abs/2405.06459)
we add teacher-forcing and non-teacher forcing, input_noise and not-input-noise conditions in evaluation

fix bugs in original code, so you can run without debugging.

note: new metrics used torchmetrics, which may be different from original one. results and metrics are in ./results folder

**as for my implementation, input noise can get higher or equal scores on bleu, which means the decoding is not effective!**
We strongly suggest everyone when doing brain decoding text, you should compare your results with input noise!
*results*
![image](https://github.com/NeuSpeech/EEG-To-Text/assets/151606332/63965b7a-8664-47ea-a5fe-57b35d8f1c3f)

## Create Environment
+ For mac and linux:
```
virtualenv pyenv --python=3.10.12
source pyenv/bin/activate
pip install -r requirements.txt
```
+ For Windows:
```
virtualenv pyenv --python=3.10.12
pyenv\Scripts\activate
pip install -r requirements.txt
```

## Download ZuCo datasets
- Download ZuCo v1.0 'Matlab files' for 'task1-SR','task2-NR','task3-TSR' from https://osf.io/q3zws/files/ under 'OSF Storage' root,  
unzip and move all `.mat` files to `~/datasets/ZuCo/task1-SR/Matlab_files`,`~/datasets/ZuCo/task2-NR/Matlab_files`,`~/datasets/ZuCo/task3-TSR/Matlab_files` respectively.
```bash
wget https://files.osf.io/v1/resources/q3zws/providers/osfstorage/5b4eee366d4eb300106ec69c/?zip=
mkdir -p datasets/ZuCo/task1-SR/Matlab_files
unzip index.html?zip= -d datasets/ZuCo/task1-SR/Matlab_files
rm index.html?zip=
wget https://files.osf.io/v1/resources/q3zws/providers/osfstorage/5b4eee6d33f0b9000cba7151/?zip=
mkdir -p datasets/ZuCo/task2-NR/Matlab_files
unzip index.html?zip= -d datasets/ZuCo/task2-NR/Matlab_files
rm index.html?zip=
wget https://files.osf.io/v1/resources/q3zws/providers/osfstorage/5b4eee966d4eb300106ec71c/?zip=
mkdir -p datasets/ZuCo/task3-TSR/Matlab_files
unzip index.html?zip= -d datasets/ZuCo/task3-TSR/Matlab_files
rm index.html?zip=
```
- Download ZuCo v2.0 'Matlab files' for 'task1-NR' from https://osf.io/2urht/files/ under 'OSF Storage' root, unzip and move all `.mat` files to `~/datasets/ZuCo/task2-NR-2.0/Matlab_files`.
```bash
wget https://files.de-1.osf.io/v1/resources/2urht/providers/osfstorage/5ddea2baab905e0009e77b0d/?zip=
mkdir -p datasets/ZuCo/task2-NR-2.0/Matlab_files
unzip index.html?zip= -d datasets/ZuCo/task2-NR-2.0/Matlab_files
rm index.html?zip=
```
## Preprocess datasets
run `bash ./scripts/prepare_dataset.sh` to preprocess `.mat` files and prepare sentiment labels. 

For each task, all `.mat` files will be converted into one `.pickle` file stored in `~/datasets/ZuCo/<task_name>/<task_name>-dataset.pickle`. 

Sentiment dataset for ZuCo (`sentiment_labels.json`) will be stored in `~/datasets/ZuCo/task1-SR/sentiment_labels/sentiment_labels.json`. 

Sentiment dataset for filtered Stanford Sentiment Treebank will be stored in `~/datasets/stanfordsentiment/ternary_dataset.json`

## Usage Example
### Open vocabulary EEG-To-Text Decoding
To train an EEG-To-Text decoding model, run `bash ./scripts/train_decoding.sh`.

To evaluate the trained EEG-To-Text decoding model from above, run `bash ./scripts/eval_decoding.sh`.

For detailed configuration of the available arguments, please refer to function `get_config(case = 'train_decoding')` in `/config.py`

### Zero-shot sentiment classification pipeline 
We first train the decoder and the classifier individually, and then we evaluate the pipeline on ZuCo task1-SR data.

To run the whole training and evaluation process, run `bash ./scripts/train_eval_zeroshot_pipeline.sh`.

For detailed configuration of the available arguments, please refer to function `get_config(case = 'eval_sentiment')` in `/config.py`

## Citation
```
@inproceedings{jo2024are,
  title={Are EEG-to-Text Models Working?},
  author={Hyejeong Jo, Yiqian Yang, Juhyeok Han, Yiqun Duan, Hui Xiong, Won Hee Lee},
  booktitle={Arxiv},
  year={2024}
}
```
