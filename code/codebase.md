# Sleep Apnea ML/DL Resources

Compiled: 5 October 2026

This list covers machine learning and deep learning projects, papers, reviews, and datasets related to sleep apnea. The code repositories have not been run or verified, and several are small personal projects, so they should be checked before being relied upon.

## GitHub code: ECG-based

- [mahsaabahrami/Sleep-Apnea](https://github.com/mahsaabahrami/Sleep-Apnea): compares classical ML and DL methods on single-lead ECG, including modified AlexNet, ZFNet, and VGG. Linked to papers in IEEE TIM (2022) and MeMeA (2021).
- [JackAndCole: modified LeNet-5](https://github.com/JackAndCole/Sleep-apnea-detection-through-a-modified-LeNet-5-convolutional-neural-network): modified LeNet-5 CNN that uses adjacent segments, evaluated on Apnea-ECG.
- [JackAndCole: time-window ANN](https://github.com/JackAndCole/Detection-of-sleep-apnea-from-single-lead-ECG-signal-using-a-time-window-artificial-neural-network): exploits time dependence between consecutive ECG segments.
- [SE-MSCNN](https://www.github.com/Bettycxh/Toward-Sleep-Apnea-Detection-with-Lightweight-Multi-scaled-Fusion-Network): lightweight multi-scale CNN with channel attention, aimed at wearable deployment.

## GitHub code: other signals

- [UtsavBhalani-101/Sleep-apnea-detection](https://github.com/UtsavBhalani-101/Sleep-apnea-detection): modular PyTorch pipeline for OSA detection and AHI estimation on UCDDB, SHHS, and MESA, using airflow, respiratory effort, and SpO2 channels.
- [SomnNET (arlenejohn/Sleep_apnea_SpO2)](https://github.com/arlenejohn/Sleep_apnea_SpO2): SpO2-based network for smartwatches, with pruned and binarized model variants.
- [jwc-rad/osa-ai](https://github.com/jwc-rad/osa-ai): hybrid CNN-Transformer for radar-based apnea-hypopnea event detection (Sleep, 2024).
- [SebasTS15/Sleep-Apnea-Detection-Model](https://github.com/SebasTS15/Sleep-Apnea-Detection-Model): classifies respiratory audio segments as apnea or non-apnea, based on PSG-Audio.
- [SleepFM-Clinical (zou-group)](https://github.com/zou-group/sleepfm-clinical): multimodal PSG foundation model trained on more than 585,000 hours from about 65,000 participants.

## GitHub topic pages

These pages list further repositories, including SpO2 and ECG diagnostic systems, a TinyML microcontroller prototype, and PSG segmentation models.

- [sleep-apnea](https://github.com/topics/sleep-apnea)
- [apnea-ecg](https://github.com/topics/apnea-ecg)
- [obstructive-sleep-apnea](https://github.com/topics/obstructive-sleep-apnea)

## Papers

- [SleepFM: A multimodal sleep foundation model for disease prediction (Nature Medicine)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12920147/): reports accuracies of 0.69 and 0.87 for apnea severity and presence.
- [SleepFM-2 (arXiv, 2026)](https://arxiv.org/pdf/2609.06849): pretrained on over two million hours of PSG, and targets the finer-grained respiratory events that the first version could not score.
- [Original SleepFM (arXiv, 2024)](https://arxiv.org/pdf/2405.17766): contrastive multimodal representation learning on PSG.
- [Apnea Burden-Guided Framework (arXiv, 2026)](https://arxiv.org/pdf/2608.12229): out-of-distribution generalization for PPG-based apnea characterization.
- [Deep Learning Approaches for Sleep Apnea Classification from Polysomnographic EEG Signals (arXiv, 2026)](https://arxiv.org/pdf/2607.15477)
- [A Recall-First CNN for Sleep Apnea Screening from Snoring Audio (arXiv)](https://arxiv.org/pdf/2510.00052)
- [Deep-learning based sleep apnea detection using sleep sound, SpO2, and pulse rate](https://link.springer.com/article/10.1007/s41870-024-01906-x): mel-spectrogram input from 24 PSG-Audio patients.
- [Detection of Obstructive Sleep Apnoea using a 1D CNN on segmented ECG (arXiv)](https://arxiv.org/pdf/2002.00833)
- [Detection of Obstructive Sleep Apnea Using Deep Learning on Audio Signals (UCAmI 2025)](https://link.springer.com/chapter/10.1007/978-3-032-16995-2_17)

## Reviews and meta-analyses

- [Diagnostic accuracy of AI for OSA detection: a systematic review (BMC Med Inform Decis Mak, 2025)](https://link.springer.com/article/10.1186/s12911-025-03129-x): reported accuracy ranged from 67.03% to 98.6%, highest for hybrid and DL models. PROSPERO registered.
- [Accuracy of deep learning in diagnosis of apnea syndrome: systematic review and meta-analysis (Frontiers in Neurology, 2025)](https://pmc.ncbi.nlm.nih.gov/articles/PMC12702770): pooled sensitivity and specificity of 0.94 each on cross-validation sets; QUADAS-2 used for risk of bias.
- [Obstructive Sleep Apnea Prediction: A Comprehensive Review and Comparative Study (Machine Learning, 2026)](https://link.springer.com/article/10.1007/s10994-025-06937-4): covers diagnosis problems, input types, data biases, pre-processing, and model performance.
- [Deep learning for image-based snoring sound analysis: a systematic review](https://pmc.ncbi.nlm.nih.gov/articles/PMC12476793/): includes an overview of snoring-based datasets.

## Datasets

- [PhysioNet Apnea-ECG Database](https://www.physionet.org/content/apnea-ecg/1.0.0/challenge/): 70 ECG recordings of about 8 hours each with per-minute apnea annotations for the learning set.
- [Sleep Heart Health Study PSG Database (PhysioNet)](https://physionet.org/content/shhpsgdb/): the larger SHHS set, along with MESA, is available through the National Sleep Research Resource (NSRR).
- [PSG-Audio (Scientific Data, 2021)](https://www.nature.com/articles/s41597-021-00977-w): scored PSG with synchronized audio recordings.
- [PSG-Audio Apnea Audios (Kaggle subset)](https://www.kaggle.com/datasets/bryandarquea/psg-audio-apnea-audios)
- [Multimodal PSG and audio dataset (Scientific Data, 2025)](https://www.nature.com/articles/s41597-025-05583-8): annotates obstructive, central, and mixed apnea and hypopnea.
