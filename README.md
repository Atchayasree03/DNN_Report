# DNN_Report
DNN_Report
Network Intrusion Detection Using Machine Learning

A machine-learning-based Network Intrusion Detection System (NIDS) that classifies network connection records as normal or attack (DoS, Probe, R2L, U2R) using the NSL-KDD dataset.

Mini project, Department of Computer Science and Engineering, KIT – Kalaignarkarunanidhi Institute of Technology, Coimbatore.

Overview

Signature-based intrusion detection tools only catch attacks they already know. This project trains supervised classifiers to learn the statistical patterns of malicious traffic, so that new or slightly modified attacks can also be flagged.

Pipeline: Data loading → Cleaning → Encoding → Scaling → Feature selection → Model training → Evaluation

Features
Binary classification (Normal vs Attack) and 5-class classification (Normal, DoS, Probe, R2L, U2R)
Four models compared: Decision Tree, Random Forest, KNN, SVM
Feature importance analysis for feature selection
Evaluation with accuracy, precision, recall, F1-score, false alarm rate and confusion matrices
Dataset

NSL-KDD (improved version of KDD Cup 1999, with duplicate records removed).

File	Records (approx.)
KDDTrain+.txt	125,973
KDDTest+.txt	22,544

Each record has 41 features (basic, content, time-based and host-based traffic features) plus a label.

Download: https://www.unb.ca/cic/datasets/nsl.html — place the files in the data/ folder.

Project Structure
network-intrusion-detection/
├── data/
│   ├── KDDTrain+.txt
│   └── KDDTest+.txt
├── notebooks/
│   └── nids.ipynb
├── src/
│   ├── preprocess.py
│   ├── train.py
│   └── evaluate.py
├── results/
│   └── confusion_matrix.png
├── requirements.txt
└── README.md

Adjust the structure above to match your actual files.

Requirements
Python 3.10+
numpy
pandas
scikit-learn
matplotlib
seaborn
jupyter
Installation
bash
git clone https://github.com/<your-username>/network-intrusion-detection.git
cd network-intrusion-detection

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install -r requirements.txt

requirements.txt:

numpy
pandas
scikit-learn
matplotlib
seaborn
jupyter
Usage

Option 1: Notebook

bash
jupyter notebook notebooks/nids.ipynb

Option 2: Scripts

bash
python src/train.py --model random_forest --task binary
python src/evaluate.py --model random_forest --task binary

Supported models: decision_tree, random_forest, knn, svm Supported tasks: binary, multiclass

Methodology
Preprocessing: map attack names to categories, remove duplicates, one-hot encode protocol_type, service and flag, Min-Max scale numerical features.
Feature selection: rank features using Random Forest importance and correlation analysis.
Training: 80/20 stratified split of the training file, with cross-validation for hyperparameter tuning.
Evaluation: metrics on the held-out split and on the official KDDTest+ set.
Results

Replace these with the numbers from your own run.

Model	Accuracy	Precision	Recall	F1-score	False Alarm Rate
Decision Tree	99.5%	99.5%	99.5%	99.5%	0.5%
Random Forest	99.8%	99.8%	99.8%	99.8%	0.2%
KNN (k = 5)	99.2%	99.2%	99.3%	99.2%	0.9%
SVM (RBF)	98.7%	98.6%	98.9%	98.7%	1.4%

Random Forest gave the best overall balance. Accuracy on the official KDDTest+ set is lower because it contains attack types absent from the training data.

Limitations
NSL-KDD is based on old (1998) traffic and does not reflect modern or encrypted traffic.
Works offline on stored records; no live packet capture.
R2L and U2R attacks are detected poorly because of class imbalance.
Future Work
Test on newer datasets (CICIDS2017, UNSW-NB15)
Handle imbalance using SMOTE or cost-sensitive learning
Try deep models (autoencoders, LSTM)
Add real-time detection with Scapy or Zeek and an alert dashboard
References
Tavallaee et al., "A Detailed Analysis of the KDD CUP 99 Data Set," 2009.
Scarfone and Mell, "Guide to Intrusion Detection and Prevention Systems," NIST SP 800-94, 2007.
Breiman, "Random Forests," Machine Learning, 2001.
Pedregosa et al., "Scikit-learn: Machine Learning in Python," JMLR, 2011.
Author

Atchayasree B.E. Computer Science and Engineering, KIT – Kalaignarkarunanidhi Institute of Technology, Coimbatore GitHub: github.com/Atchayasree03

License

This project is for academic purposes. Add a license of your choice (for example MIT) if you publish it.
