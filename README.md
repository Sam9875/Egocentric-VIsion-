# Egocentric-VIsion-Natural Language Queries in Egocentric Videos (Ego4D NLQ)
This project focuses on answering natural language queries from egocentric videos, leveraging the Ego4D dataset and the VSLNet architecture. It supports both baseline training and extended methods such as using LLMs or VLMs for improved performance.


 Project Structure
main.py — Core training and evaluation pipeline.

VSLNet.py — VSLNet and VSLBase model definitions.

data_loader.py — Data loading and preprocessing routines.

data_gen.py — Dataset conversion and vocabulary/embedding creation.

layers.py — Model architecture components (encoders, attention, predictors, etc.).

(Also all the models were run on separate video features.)


 
 Project Objective
Given a natural language query and a video from the Ego4D dataset, the task is to localize the segment of the video that answers the query.

Examples of queries:

"Where was the phone last seen?"

"How many frying pans can I see on the shelf?"

The project is based on the Ego4D NLQ benchmark and implements the VSLBase and VSLNet architectures, allowing training on frozen visual features extracted using Omnivore and EgoVLP.


Installation


Make sure to install:

torch

transformers

submitit

nltk

tqdm

Any other missing dependencies used in your notebooks



 Dataset Setup
Request Access to Ego4D and sign the data usage agreement here.


Download NLQ annotations (v1) and features from Ego4D CLI:
we have used already downloaded files for the project you can also go ahead if you have the keys 


ego4d --download-annotations nlq
ego4d --download-features omnivore_video_swinl_fp16



Organize features and annotations as expected under:



data/
├── features/
│   └── <task>/<feature_version>/
└── dataset/
    └── <task>/
        ├── train.json
        ├── val.json
        └── test.json
Running the Model


python main.py \
    --mode train \
    --task ego4d \
    --fv omnivore \
    --max_pos_len 128 \
    --predictor rnn \
    --epochs 10 \
    --batch_size 32   (this part can be changed depending upon your environment and video features you use)


    
Evaluation

python main.py \
    --mode test \
    --task ego4d \
    --fv omnivore \      (Tensorboard was also used in the case, you want to visualize it graphically the loss and view)
    --predictor rnn
    
    Extensions
We implemented Proposal 2: From video interval to a textual answer. Once the NLQ model retrieves the correct video segment, we use models like Video-LLaVA to generate direct textual answers.

 
 Results
Performance is evaluated using:

Recall@k at various tIoU thresholds

Optionally: ROUGE/BLEU for textual answer generation (in extensions)


Notebooks
Jupyter notebooks are provided separately for:

Exploratory data analysis

Feature visualization

Query-based qualitative result inspection

Fine-tuning and evaluation workflows

 
 References
Ego4D Dataset (Grauman et al. 2022)

VSLNet (Zhang et al. 2020)

Omnivore (Girdhar et al. 2022)

EgoVLP (Lin et al. 2022)

Video-LLaVA (Lin et al. 2023)

Acknowledgements
This project was developed for the Egocentric Video Understanding course, supported by the teaching assistants Simone Alberto Peirone and Gaetano Salvatore Falco
