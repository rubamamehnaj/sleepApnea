# Research Directions for Q1 Publication in Sleep Apnea ML/DL

Based on the literature review and dataset inventory, eight high-potential research directions are identified below. Each addresses a genuine gap in the field, is grounded in recent publications and systematic reviews, is mapped to specific datasets from the inventory, and is aligned with current trends in Q1 journals.

Each direction follows the same structure: the gap that motivates it, what already exists, the precise gap that remains, datasets and feasibility, research questions, and target journals.

---

## How These Directions Were Identified

This analysis cross-referenced three sources: (1) the explicit limitations and future-work sections in recent systematic reviews (Kilic et al., Fathima et al., Osa-Sanchez et al., Abd-Alrazaq et al.), (2) the methodological gaps highlighted in the newest narrative reviews on ML in OSA, and (3) the capabilities of the datasets already vetted. The gaps were then filled in by grounding each direction in recent publications, dataset specifications, and systematic reviews. The result is a set of directions that are both scientifically timely and practically feasible with the current data access.

---

## Direction 1: Foundation Models and Self-Supervised Pretraining for Sleep Apnea

### 1.1 The Gap

Nearly every DL model in sleep apnea research is trained from scratch on relatively small labeled datasets. This is a fundamental bottleneck. Recent systematic reviews consistently identify small sample sizes and poor generalizability as the field's most persistent limitations. The narrative review by Lima Diniz Araujo et al. (2025) found that study cohorts were predominantly overweight males with underrepresentation of women, younger obese adults, individuals over 60, and diverse racial groups. Foundation models, pretrained on large unlabeled physiological corpora and fine-tuned on downstream tasks, directly address this.

### 1.2 What Exists

**SynthSleepNet (Lee et al., 2025)** is a multimodal hybrid self-supervised learning framework that integrates masked prediction and contrastive learning across EEG, EOG, EMG, and ECG. It uses a Mamba-based temporal context module. On three downstream tasks, it achieved accuracies of 89.89% (sleep-stage classification), 99.75% (apnea detection), and 89.60% (hypopnea detection). In a semi-supervised setting with limited labels, it still achieved 87.98%, 99.37%, and 77.52% respectively. Source code is available on GitHub.

**Stanford Sleep Bench (Kjaer et al., 2025)** is a large-scale PSG dataset comprising 17,467 recordings totaling over 163,000 hours from a major sleep clinic, including 13 clinical disease prediction tasks alongside sleep staging, apnea diagnosis, and age estimation. The authors systematically evaluated SSRL pretraining methods and found that multiple pretraining methods achieve comparable performance for sleep staging, apnea diagnosis, and age estimation, but for mortality and disease prediction, contrastive learning significantly outperforms other approaches.

**SleepFM** is a multimodal sleep foundation model pretrained using self-supervised contrastive learning, with the Sleep Heart Health Study (SHHS) dataset reserved for external validation. It was published in *Nature Medicine* and uses overnight sleep data to predict long-term disease risk.

**A Low-Burden Sleep Foundation Model** was built on respiratory and heartbeat signals from 780,000+ hours of multi-ethnic sleep recordings, with the WSC4 dataset originating from a longitudinal Wisconsin study.

These are early efforts, and the space is far from saturated.

### 1.3 The Precise Gap

1. **No unified benchmark**: Stanford Sleep Bench addresses this partially, but it is single-institution. A multi-cohort, multi-device benchmark is still absent.
2. **Limited cross-cohort pretraining**: SleepFM was pretrained primarily on one large-scale PSG dataset. A model pretrained across the Human Sleep Project (119,234 recordings from 90,000+ patients across five US academic medical centers), SHHS, and MESA would be genuinely multi-cohort.
3. **Pediatric foundation models**: The Boston Children's Hospital Sleep Corpus (15,695 fully annotated pediatric PSG recordings, 2010–2024) exists within the Human Sleep Project but has not been used for foundation model pretraining.

### 1.4 Datasets and Feasibility

Available: **Human Sleep Project** (119,234 overnight recordings, 90,000+ patients, five US academic medical centers; clinical PSG with scoring, via BDSP credentialed access), **SHHS** (~5,800 recordings), **MESA** (~2,200 recordings), and **CinC Challenge 2018** (~1,985 recordings). This is an unusually strong pretraining corpus. Pretraining a multimodal foundation model on unlabeled or partially labeled PSG and fine-tuning on specific apnea detection tasks is entirely feasible. The **Stanford Sleep Bench** provides a ready-made evaluation protocol with 13 clinical disease prediction tasks.

### 1.5 Research Questions

- Can a foundation model pretrained on large-scale, multi-cohort PSG data (Human Sleep Project + SHHS + MESA) achieve better cross-dataset generalization for apnea/hypopnea event detection than models trained from scratch on individual datasets?
- Can such a model outperform SynthSleepNet (99.75% apnea detection) on cross-dataset evaluation?
- Does contrastive learning (as in SleepFM) or masked prediction (as in SynthSleepNet) yield better transfer for apnea detection specifically?
- Can a pediatric foundation model pretrained on the BCH Sleep Corpus (15,695 recordings) improve pediatric OSA detection over models trained from scratch?

### 1.6 Target Journals

IEEE Transactions on Cybernetics (IF ~11), Nature Communications (IF ~16), npj Digital Medicine (IF ~15).

---

## Direction 2: Cross-Dataset Generalization and Domain Adaptation

### 2.1 The Gap

This is perhaps the single most repeated limitation in the literature. The 2026 systematic review in *Sleep Medicine Reviews* explicitly states that "strong performance within one dataset does not guarantee robustness in an external population". The comprehensive imaging review by Bahraseman et al. (2025) lists data bias and overfitting among the primary barriers to clinical translation. The ML techniques review notes that "performance depends much on specific datasets or demographic groups" and that "small sample sizes diminish generalizability".

### 2.2 What Exists

**A multifaceted approach for OSA classification from ECG (Varghese et al., 2026)** presents a holistic framework using two datasets: PhysioNet Apnea-ECG (healthy patients with apnea) and OSASUD (stroke-unit patients). The framework integrates feature engineering rooted in dynamical systems theory and statistical analysis, with transfer learning in two ways: across datasets (adapting models trained on large cohorts to smaller clinical datasets) and at the patient level (personalizing models using limited individual data).

**SE-MSResNet (Zhang et al., 2025)** is a lightweight squeeze-and-excitation multi-scaled ResNet with domain generalization for SA detection from single-lead ECG. It proposes a jointly shared feature training strategy based on domain adversarial generalization to minimize feature distribution discrepancy between source domains (training subjects) and enhance common sleep apnea-related features.

**DUDE (Deep Unsupervised Domain Adaptation using variable nEighbors, 2025)** addresses OSA diagnosis from SpO2 as a regression task against AHI, and atrial fibrillation detection from ECG.

**Cross-cohort AHI harmonisation and prediction from multi-channel PSG (2025)** developed a unified framework for respiratory-event label reconstruction. A logistic regression model using ECG contributed most strongly, followed by SaO2 and respiratory-effort channels. The framework supports cross-cohort respiratory-label harmonisation.

**UCRDA (2026)** proposed unsupervised domain adaptation for mmWave radar.

**Adversarial domain adaptation for snoring-based SA detection (2025)** uses Wasserstein GANs with a Subject-Invariant Feature Refiner.

These remain isolated efforts on specific signal types.

### 2.3 The Precise Gap

1. **No systematic evaluation across sex, age, ethnicity, and device type**: The Varghese et al. framework uses only two datasets. A systematic study across MESA (multi-ethnic), SHHS (community cohort), MrOS (older men), WSC (longitudinal), and UCDDB (clinical) has not been performed.
2. **SpO2-specific domain shift**: The Zhang et al. (2025) multimodal model achieved 95.04% (Apnea-ECG) and 90.56% (UCD) per-segment accuracy, but the drop between datasets is notable. No study has systematically decomposed this drop into demographic vs. device vs. scoring-protocol components.
3. **Pediatric-to-adult domain shift**: No study has evaluated how models trained on adult cohorts perform on pediatric data and vice versa (developed further in Direction 8).

### 2.4 Datasets and Feasibility

Available datasets have overlapping modalities but different populations: **Apnea-ECG** (70 recordings), **UCDDB** (25 recordings), **MESA** (~2,200, multi-ethnic), **SHHS** (~5,800, community cohort), **MrOS** (~2,900, older men), **WSC** (longitudinal), and **ISRUC-Sleep** (~118 recordings). The **OSASUD** dataset (30 stroke-unit patients, 961,357 annotated seconds, single-lead ECG at 80 Hz) provides a real-world, noisy out-of-distribution test set. Together these allow a systematic evaluation of domain shift across sex, age, ethnicity, and device type.

### 2.5 Research Questions

- How do DL models for ECG-based and SpO2-based apnea detection degrade when trained on one cohort (e.g., MESA) and tested on another (e.g., SHHS, MrOS, UCDDB), and which domain adaptation strategies best mitigate this degradation?
- What is the contribution of demographic vs. device-related shift to that degradation?
- Can domain adversarial training (as in SE-MSResNet) reduce the performance gap between Apnea-ECG and OSASUD by more than 50%?
- Does cross-cohort AHI harmonisation (as in the 2025 framework) improve cross-dataset generalization for deep learning models?

### 2.6 Target Journals

IEEE Journal of Biomedical and Health Informatics (IF ~7), Computers in Biology and Medicine (IF ~7), Sleep Medicine Reviews (IF ~11, for a review/meta-analysis).

---

## Direction 3: Wearable and Consumer-Device Apnea Detection with PPG

### 3.1 The Gap

The Osa-Sanchez et al. (2025) systematic review identified a trend toward integrating patches, clocks, and rings with CNNs and transfer learning, but noted that validation remains limited. Two smartwatch-integrated sleep apnea detection algorithms received FDA clearance in 2024, signaling regulatory readiness but also highlighting the need for rigorous independent validation. The ordinal pattern similarity-guided framework for wearable PPG (2025) achieved 72.4% sensitivity and 0.687 F1-score, which is useful but far from clinical-grade.

### 3.2 What Exists

**DREAMT (v2.2.0, 2025)** provides high-resolution multichannel wearable device data paired with PSG from 100 patients with sleep apnea. It includes synchronized recordings of wearable data (PPG, accelerometry, etc.), sleep stage annotations, and sleep apnea events annotated by certified sleep technicians based on clinical PSG. It contains 100 overnight PPG measurements with labeled apnea events. The Hugging Face version includes fields for Obstructive_Apnea, Central_Apnea, Hypopnea, and Multiple_Events. This is exactly the kind of paired wearable-PSG data needed for supervised wearable model development.

**Lightweight Tree Ensembles (Silva et al., 2025)** used the DREAMT corpus with overnight PSG ground truth to examine whether PPG and tri-axial accelerometry alone can separate five clinically recognized breathing states: normal, hypopnea, obstructive, central, and mixed apneas. Random Forest and LightGBM achieved balanced accuracy of 62% and Cohen's κ of ≈0.53 on an independent test set. Recall was above 70% for central apneas and normal breathing, near 60% for obstructive apneas and hypopneas, and lower for mixed events.

**ECE12: Team Sleep** designed, implemented, and benchmarked a complete PPG-based apnea detection pipeline across six ML architectures using the DREAMT dataset.

**PPG-based DL for sleep staging in suspected apnea patients** achieved 80.8% median accuracy in a 2025 clinical evaluation.

### 3.3 The Precise Gap

1. **Five-class stratification remains weak**: Balanced accuracy of 62% is far from clinical-grade. Mixed events have particularly low recall.
2. **No deep learning model on DREAMT for five-class stratification**: The Silva et al. study used tree ensembles. A DL model (CNN, LSTM, Transformer) could potentially capture temporal dependencies better.
3. **Minimum sensor set unknown**: No study has systematically evaluated whether PPG alone, PPG + accelerometry, or PPG + accelerometry + additional sensors is sufficient.
4. **Demographic validation**: DREAMT's demographic diversity has not been fully characterized for fairness auditing.

### 3.4 Datasets and Feasibility

**DREAMT** is the key dataset (PhysioNet credentialed access + DUA). It was released in April 2025 specifically to enable wearable-based apnea detection research and includes synchronized PSG ground truth. The **BIDMC PPG** dataset (53 recordings × 8 min, ICU, no apnea labels, not sleep data) is useful only for method prototyping, not for apnea detection.

### 3.5 Research Questions

- Can a lightweight, edge-deployable DL model trained on DREAMT wearable data (PPG, accelerometer, etc.) achieve clinically acceptable sensitivity and specificity for moderate-to-severe OSA detection across demographics?
- Can a 1D-CNN or Transformer model trained on DREAMT PPG + accelerometry outperform the 62% balanced accuracy of tree ensembles for five-class apnea stratification?
- What is the minimum sensor set (PPG only vs. PPG + accelerometry vs. PPG + accelerometry + temperature) required for clinically acceptable sensitivity and specificity?
- Do model explanations (e.g., SHAP on PPG features) vary systematically by age, sex, or BMI in DREAMT?

### 3.6 Target Journals

IEEE Transactions on Biomedical Engineering (IF ~7), IEEE Journal of Biomedical and Health Informatics, Digital Health (IF ~5), Journal of Medical Internet Research (IF ~7).

---

## Direction 4: Pediatric Sleep Apnea Detection and Severity Assessment

### 4.1 The Gap

Pediatric OSA has distinct pathophysiology, diagnostic criteria, and signal characteristics compared to adult OSA, yet most DL models are developed and validated on adult cohorts. The García-Vicente et al. (2026) paper in *Measurement* explicitly states that "no prior study has applied these techniques to concurrently analyze ECG and SpO2 data" for pediatric OSA. The ML narrative review found underrepresentation of younger populations across the literature.

### 4.2 What Exists

**García-Vicente et al. (2026)** developed an explainable DL model integrating CNNs with overnight SpO2 and ECG signals to identify pediatric OSA. Using patients (n = 3,320) from CHAT, PATS, and the University of Chicago (UofC) databases, the model achieved Cohen's 4-class kappa of 0.549 (CHAT), 0.457 (PATS), and 0.378 (UofC). SHAP analysis showed that SpO2 is more relevant in moderate and severe cases, and ECG in mild or no OSA cases. SHAP visualizations identified SpO2 desaturations linked to clusters of apneic events, bradycardia-tachycardia patterns, and variations in P and T waves, PQ and QT intervals, and the QRS complex.

**A multi-modal Transformer approach (2025)** for at-home pediatric sleep apnea testing used NCH Sleep DataBank (large, free, PSG signals linked to EHRs) and CHAT. The model achieved F1-score of 83.1% and AUROC of 90% on CHAT, and 90.4% AUROC on NCH. Among all triple signal group combinations, the one including ECG and SpO2 was the top performer for apnea-hypopnea detection.

**A 2025 radar study** used millimeter-wave radar and pulse oximetry for automated diagnosis in 281 children (ages 1–18).

**An explainable DL approach for pediatric OSA from single-channel airflow** was published in 2025.

### 4.3 The Precise Gap

1. **Cross-dataset generalization between NCH and CHAT**: The multi-modal Transformer approach evaluated on both but did not systematically test cross-dataset transfer (train on NCH, test on CHAT and vice versa).
2. **EHR integration**: NCH Sleep DataBank includes linked EHR data (diagnoses, medications), but no published study has systematically evaluated whether incorporating EHR data improves performance over signal-only models.
3. **Age sub-group analysis**: García-Vicente et al. noted the "lack of interpretability and validation across patients from a wide range of ages." Pediatric OSA manifests differently in toddlers vs. school-age children vs. adolescents.
4. **Hypopnea detection in children**: Pediatric hypopnea criteria differ from adult criteria, and no DL model has been specifically optimized for pediatric hypopnea detection.

### 4.4 Datasets and Feasibility

Available: **NCH Sleep DataBank** (3,984 pediatric sleep studies, 3,673 patients, 2017–2019, with linked EHR data) and **CHAT** (464 children aged 5–9.9 with baseline and follow-up PSG). The combination of NCH (real-world, large-scale, EHR-linked) and CHAT (randomized trial, high-quality follow-up) is powerful. The **Boston Children's Hospital Sleep Corpus** (15,695 fully annotated pediatric PSG recordings, 2010–2024) is available within the Human Sleep Project. **PATS** provides additional pediatric data.

### 4.5 Research Questions

- Can a multimodal DL model trained on NCH Sleep DataBank generalize to CHAT (and vice versa) for pediatric OSA severity classification, and does incorporating EHR data (comorbidities, medications) improve performance over signal-only models?
- Does age-stratified modeling (toddlers vs. school-age vs. adolescents) improve pediatric OSA detection compared to a single age-agnostic model?
- Can SHAP-based explanations for pediatric OSA remain stable across age subgroups, and do the most important features differ by age?

### 4.6 Target Journals

Sleep (IF ~6), Pediatric Research (IF ~3.5), Computers in Biology and Medicine, IEEE Journal of Biomedical and Health Informatics.

---

## Direction 5: Audio and Smartphone-Based OSA Screening

### 5.1 The Gap

Smartphone audio offers a non-contact, low-cost path to population-scale screening, but the 2026 systematic review in *Sleep Medicine Reviews* found that while some studies achieved sensitivity ≥80%, there was a trade-off between sensitivity and specificity, and standardization was lacking. The ML techniques review notes that "concentration on diagnostic criteria and daytime sounds may overlook vital OSA-related elements" and calls for expanding data sources.

### 5.2 What Exists

**The Shenzhen Multimodal OSA Dataset (2025)** (50 patients, 400+ hours, smartphone audio synchronized with PSG) is a major new resource.

**A hybrid CNN-ResNet18 model** using smartphone tracheal audio achieved 91% accuracy, 90.1% sensitivity, and 93.7% specificity on PSG-Audio and a 52-subject dataset.

**Multi-task learning for acoustic OSA (2026)** used a dataset of 1,094 hours of smartphone audio and home sleep apnoea test data (157 nights, 103 participants). The best-performing MTL variant (hard parameter sharing) achieved sensitivity of 0.84 and specificity of 0.93 for detecting moderate-to-severe OSA (AHI ≥ 25). MTL generally outperformed single-task learning, with the greatest improvement in detecting moderate-to-severe OSA. The secondary task was estimating oxygen desaturation from SpO2 data, which was only required during training.

**A Cascaded Two-Stage CNN Pipeline for Audio-Based Snore and Sleep Apnea Detection on Smartphones (2026)** was released on Zenodo with reference baselines and multi-seed validation. It presents a non-contact, low-cost path to sleep health screening at population scale.

**Coordinate Attention for 1D Audio-Based Sleep Apnea Detection (2026)** presents a lightweight neural network architecture for detecting sleep-disordered breathing events directly from smartphone audio, eliminating the need for wearable devices.

**Convolutional Neural Networks for Apnea Detection from Smartphone Audio Signals (2025)** tested the potential of CNNs for apnea detection from smartphone audio, studying the effect of window size.

### 5.3 The Precise Gap

1. **Multi-task learning with more than two tasks**: The 2026 MTL study used only two tasks (OSA detection + SpO2 desaturation estimation). Adding snore type classification (4-class VOTE scheme from MPSSC) and body position estimation (6-class from SSBPR) as auxiliary tasks is unexplored.
2. **Cross-dataset audio validation**: No study has systematically evaluated how models trained on one audio dataset (e.g., Shenzhen) perform on others (e.g., PSG-Audio, MPSSC).
3. **Edge deployment**: The 2026 cascaded CNN pipeline and coordinate attention model address this partially, but no study has evaluated real-time on-device inference latency and energy consumption.
4. **Snore type classification on MPSSC with modern architectures**: Recent work achieved UAR of 67.1% on the MPSSC test set. Transformer-based or attention-based architectures have not been fully explored.

### 5.4 Datasets and Feasibility

Available: the **Shenzhen Multimodal OSA Dataset** (50 patients, 400+ hours, smartphone audio synchronized with PSG), **PSG-Audio** (212–287 patients, synchronized PSG + tracheal/ambient mic audio), **Snoring Dataset (Kaggle)** (1,000 clips for pretraining), **MPSSC** (828 snore sounds, 4-class VOTE scheme), and the **SSBPR** dataset (7,570 recordings, 6 body position labels). The **ONEI** dataset (breathing route and phase from snoring sounds) is also available by request. This is a rich audio corpus.

### 5.5 Research Questions

- Can a multi-task learning framework simultaneously detect apnea/hypopnea events, classify snore type (VOTE), and estimate body position from smartphone audio, and does joint learning improve performance over single-task models on the Shenzhen and PSG-Audio datasets?
- Does pretraining on the large but noisy Kaggle Snoring Dataset (1,000 clips) and MPSSC (828 clips) improve performance on the smaller but clinically synchronized Shenzhen and PSG-Audio datasets?
- What is the minimum audio segment length (1s, 5s, 30s) required for clinically acceptable apnea detection from smartphone audio?

### 5.6 Target Journals

Sleep Medicine Reviews (for a systematic review), IEEE Journal of Biomedical and Health Informatics, Expert Systems with Applications (IF ~8), Applied Acoustics (IF ~3.5).

---

## Direction 6: Explainable AI and Clinical Trust

### 6.1 The Gap

The explainable AI review in *Sleep and Breathing* (2026) states that "adoption of XAI within this field is still at a nascent stage, and overall, the optimal role of AI alongside clinicians continues to be unclear". The ML techniques review explicitly calls for research that maintains interpretability alongside accuracy. A 2025 paper in *Sleep Medicine Reviews* argued that "XAI tools like SHAP inherit model biases, and high prediction accuracy does not guarantee reliable feature importances".

### 6.2 What Exists

**García-Vicente et al. (2026)** used SHAP to identify SpO2 desaturations and ECG patterns linked to pediatric OSA, demonstrating that explainability can reveal clinically meaningful feature interactions.

**Chin electromyography-based explainable ML (2026)** used surface EMG features extracted from motor units decomposed from chin EMG in a clinical cohort (ACPN, 20 subjects). The AdaBoost model achieved high MU-level class-wise recall for mild, moderate, and severe OSA (96.2%, 98.2%, 99.3%) under subject-wise split and recovered the AHI-based severity label in 80% of subjects under leave-one-subject-out validation. Generalizability was examined through external validation on UCDDB (25 subjects) and SHHS1 (1,000 subjects), with stratified analyses by age, gender, BMI, daytime sleepiness, and sleep efficiency. Three-class accuracies remained clearly above chance across subgroups and were highest in individuals with greater OSA burden.

**Data-driven phenotyping and longitudinal feature modeling of sleep apnea subtypes using interpretable ML (2025)** used SHAP to extract both global rankings and class-specific insights for sleep apnea subtype classification in the SHHS cohort. Demographic, anthropometric, and lifestyle traits were compared across subtypes to enable risk stratification. The authors noted that "these approaches often lack a demographic and epidemiological perspective, with lifestyle variables underrepresented despite their critical role in population health cohorts".

**POxi-SleepNet (2025)** is an explainable DL approach for sleep staging in sleep apnea patients across all age subgroups from pulse oximetry signals. It was validated across six databases (CCSHS, CFS, CHAT, MESA, MrOS, SHHS). The model showed high performance in the six databases (4-class Acc 81.5%–84.5%). Performance was significantly lower with increasing age and OSA severity for some model variants.

**XAI-driven ECG frameworks and ECG-derived spectrogram approaches** have also been proposed.

Most of this work is still isolated.

### 6.3 The Precise Gap

1. **SHAP stability across demographic subgroups**: No study has systematically evaluated whether SHAP explanations for a multimodal OSA detection model remain stable across age, sex, ethnicity, and signal quality levels.
2. **XAI as out-of-distribution detection**: The instability of SHAP explanations as a proxy for out-of-distribution detection has not been explored.
3. **Clinician-facing XAI**: The "optimal role of AI alongside clinicians continues to be unclear." No study has conducted a user study with sleep physicians to evaluate whether XAI outputs improve diagnostic confidence or accuracy.
4. **Label noise and inter-scorer variability**: The PSG-IPA dataset (20 PSG recordings, 12 scorers) enables studying how label noise affects XAI reliability.

### 6.4 Datasets and Feasibility

Available datasets have rich, diverse signal types and clinical annotations: **PSG-IPA** (20 recordings, 12 scorers, inter-scorer variability), **CPS Dataset** (raw and derived channels with questionnaires), **MESA** (multi-ethnic), and **OSASUD** (real-world, noisy stroke-unit data with 1-second event annotations). These allow study not just of model explanations but also of how explanations vary across populations and signal quality levels. The **Chin EMG XAI study** provides a template for stratified analysis across age, BMI, and sleep profiles.

### 6.5 Research Questions

- Do SHAP-based explanations for a multimodal OSA detection model remain stable across demographic subgroups (age, sex, ethnicity) and signal quality levels, and can instability be used as a proxy for out-of-distribution detection?
- Does incorporating label noise from multiple scorers (PSG-IPA) into training improve or degrade the reliability of SHAP explanations?
- Can XAI visualizations (e.g., SHAP summary plots) improve sleep physicians' diagnostic confidence and accuracy in a prospective user study?

### 6.6 Target Journals

Artificial Intelligence in Medicine (IF ~7), Journal of Biomedical Informatics (IF ~4.5), Sleep Medicine Reviews (for a review on XAI in sleep), IEEE Journal of Biomedical and Health Informatics.

---

## Direction 7: Multi-Dataset Benchmarking and Standardized Evaluation

### 7.1 The Gap

Multiple reviews call for standardized evaluation protocols. The AI-driven screening review identifies "the absence of standardized protocols for data collection, signal preprocessing, and model benchmarking" as one of two significant research gaps. The ML techniques review notes that "study designs, heterogeneous datasets, and consistent techniques" are needed to minimize bias.

### 7.2 What Exists

No comprehensive, multi-dataset benchmark for sleep apnea DL currently exists. Individual studies evaluate on 1–2 datasets with inconsistent preprocessing, splitting, and metrics. The closest multi-cohort efforts are:

**CAISR (Complete Artificial Intelligence Sleep Report, 2025)** was developed and validated on a large diverse dataset from four cohorts (MGH, MESA, MrOS, SHHS) comprising 25,749 participants. It includes sleep staging, arousal detection, apnea identification, and limb movement analysis.

**POxi-SleepNet** was validated across six databases (CCSHS, CFS, CHAT, MESA, MrOS, SHHS) for sleep staging from pulse oximetry.

**SleepFM** was pretrained on a large-scale PSG dataset and validated externally on SHHS.

**A narrative review of computer-assisted diagnosis of OSA (2026)** found that "most models remain limited to benchmark dataset validation and lack hardware-level implementation" and called for "a comprehensive evaluation of data derived from various benchmark datasets and physiological signal sources".

### 7.3 The Precise Gap

1. **No unified, multi-dataset benchmark with standardized preprocessing**: Individual studies use inconsistent preprocessing, splitting, and metrics. CAISR uses four cohorts but focuses on sleep staging and arousal detection, not apnea-specific benchmarking.
2. **Subject-independent splits not standardized**: Most studies use random splits rather than subject-independent splits, inflating performance.
3. **Cross-modality evaluation**: No benchmark evaluates ECG, SpO2, PPG, audio, and PSG on the same set of subjects or with harmonized metrics.
4. **Pediatric inclusion**: Most benchmarks are adult-only. A benchmark spanning pediatric (NCH, CHAT) and adult (SHHS, MESA, MrOS) cohorts with age-stratified reporting is absent.

### 7.4 Datasets and Feasibility

The inventory spans ECG, PSG, PPG, audio, radar, and wearables, with diverse populations (pediatric, adult, elderly, multi-ethnic, stroke-unit). A benchmark could be defined with standardized preprocessing pipelines, subject-independent splits, and consistent evaluation metrics (per-segment, per-recording, per-event). The **Human Sleep Project** (119,234 recordings from 90,000+ patients) provides the largest single resource, and the **Stanford Sleep Bench** provides a ready-made evaluation protocol that could be extended.

### 7.5 Research Questions

- What is the state of the art in cross-dataset, cross-modality sleep apnea detection when evaluated under a unified benchmark with subject-independent splits and standardized metrics?
- How does model performance rank across ECG-only, SpO2-only, ECG+SpO2, PPG-only, and audio-only modalities when evaluated on the same subjects (where available)?
- Does a benchmark trained on adult cohorts (SHHS, MESA, MrOS) and evaluated on pediatric cohorts (NCH, CHAT) reveal systematic age-related performance degradation?

### 7.6 Target Journals

IEEE Transactions on Biomedical Engineering, Journal of Biomedical Informatics, Scientific Data (Nature Portfolio; for the benchmark paper or a data descriptor).

---

## Direction 8: Pediatric-to-Adult and Cross-Population Transfer Learning

### 8.1 The Gap

OSA manifests differently in children (e.g., adenotonsillar hypertrophy, different AHI cutoffs, distinct arousal patterns) versus adults (obesity, upper airway collapsibility). Whether knowledge learned from adult OSA datasets can transfer to pediatric detection, or vice versa, has barely been examined: the one direct study (Niu et al., 2025) is acoustic-only and uses 15 pediatric nights. The pediatric XAI paper notes the "lack of interpretability and validation across patients from a wide range of ages".

### 8.2 What Exists

**Transfer Learning for Paediatric Sleep Apnoea Detection using Physiology-Guided Acoustic Models (Niu et al., 2025)** proposes a transfer learning framework that adapts acoustic models pretrained on adult sleep data to pediatric OSA detection, incorporating SpO2-based desaturation patterns to enhance model training. Using a large adult sleep dataset (157 nights) and a smaller pediatric dataset (15 nights), the authors systematically evaluated: (i) single- vs. multi-task learning, (ii) encoder freezing vs. full fine-tuning, and (iii) the impact of delaying SpO2 labels to better align them with acoustics and capture physiologically meaningful features. Fine-tuning with SpO2 integration consistently improved pediatric OSA detection compared with baseline models without adaptation. The authors noted that "paediatric applications remain limited due to weaker respiratory sounds, developmental physiology variability, and scarcity of labelled datasets" and that "over 90% of OSA cases in children remain undiagnosed".

**Deep Learning for Pediatric Sleep Staging from Photoplethysmography (Haimov et al., 2025)** uses a transfer learning approach from adults to children. A transformer-based model was initially trained on 1,348 adult PSG recordings and then fine-tuned on pediatric PSG data.

**García-Vicente et al. (2026)** validated across CHAT, PATS, and UofC, but all three are pediatric.

**A 2025 radar-based study** included children aged 1–18.

### 8.3 The Precise Gap

1. **No systematic evaluation of adult-to-pediatric transfer for apnea detection (not just staging)**: Niu et al. (2025) is the only study directly addressing adult-to-pediatric transfer for apnea detection, and it uses only 15 pediatric nights. A larger-scale evaluation is needed.
2. **Pediatric-to-adult transfer**: No study has evaluated whether knowledge learned from pediatric OSA datasets can improve adult detection.
3. **Signal modality transfer**: Which modalities (ECG, SpO2, audio, PPG) transfer best across age groups is unknown.
4. **Age-stratified transfer**: No study has evaluated whether transfer learning effectiveness varies by pediatric age subgroup (toddlers vs. school-age vs. adolescents).

### 8.4 Datasets and Feasibility

Available: **NCH Sleep DataBank** (pediatric, 3,984 studies) and **CHAT** (pediatric, 464) on one side, and **SHHS, MESA, MrOS, WSC, Human Sleep Project** on the adult/elderly side. This enables systematic age-transfer experiments. The **Boston Children's Hospital Sleep Corpus** (15,695 pediatric PSG recordings, 2010–2024) provides a much larger pediatric pretraining corpus than the 15 nights used by Niu et al. The **PATS** dataset provides additional pediatric data.

### 8.5 Research Questions

- Does pretraining on adult PSG datasets (SHHS, MESA, MrOS) improve pediatric OSA detection performance compared to training from scratch on pediatric data alone (NCH, CHAT, BCH)?
- Which signal modalities (ECG, SpO2, audio, PPG) transfer best from adult to pediatric populations, and does the optimal modality differ by pediatric age subgroup?
- Can a pediatric-pretrained model improve adult OSA detection, and does the direction of transfer (pediatric→adult vs. adult→pediatric) matter?

### 8.6 Target Journals

Sleep (IF ~6), Pediatric Pulmonology (IF ~3), Computers in Biology and Medicine, IEEE Journal of Biomedical and Health Informatics.

---

## Summary Table

| # | Direction | Key Datasets | Specific Gap Addressed | Target Q1 Journals |
|---|---|---|---|---|
| 1 | Foundation models / SSL pretraining | Human Sleep Project, SHHS, MESA, CinC 2018, Stanford Sleep Bench | Multi-cohort pretraining; pediatric foundation model | IEEE T-Cybernetics, Nature Comms, npj Digital Medicine |
| 2 | Cross-dataset generalization / domain adaptation | Apnea-ECG, UCDDB, MESA, SHHS, MrOS, WSC, ISRUC, OSASUD | Systematic demographic/device decomposition; SpO2 domain shift | IEEE JBHI, Comput Biol Med, Sleep Med Rev |
| 3 | Wearable PPG detection | DREAMT, BIDMC PPG | DL for five-class stratification; minimum sensor set; demographic fairness | IEEE TBME, IEEE JBHI, Digital Health, JMIR |
| 4 | Pediatric OSA detection | NCH Sleep DataBank, CHAT, PATS, BCH Corpus | Cross-dataset NCH↔CHAT transfer; EHR integration; age-stratified modeling | Sleep, Pediatric Research, Comput Biol Med, IEEE JBHI |
| 5 | Audio / smartphone screening | Shenzhen Multimodal, PSG-Audio, Kaggle Snoring, MPSSC, SSBPR, ONEI | Multi-task >2 tasks; cross-dataset audio validation; edge deployment | Sleep Med Rev, IEEE JBHI, Expert Systems with Applications, Applied Acoustics |
| 6 | Explainable AI / clinical trust | PSG-IPA, CPS, MESA, OSASUD | SHAP stability across demographics; XAI as OOD detection; clinician user study | Artif Intell Med, J Biomed Inform, Sleep Med Rev, IEEE JBHI |
| 7 | Multi-dataset benchmarking | All of the above | Unified benchmark with subject-independent splits; cross-modality comparison | IEEE TBME, J Biomed Inform, Scientific Data |
| 8 | Cross-age / cross-population transfer | NCH, CHAT, BCH, PATS (pediatric) + SHHS, MESA, MrOS, WSC, Human Sleep Project (adult) | Systematic adult↔pediatric transfer; modality-specific transfer; age-stratified transfer | Sleep, Pediatric Pulmonology, IEEE JBHI, Comput Biol Med |

---

## Strategic Guidance for Q1 Publication

**On novelty**: The field has moved past "we applied a CNN to ECG and got 95% accuracy." The literature now contains foundation models and benchmarks (SynthSleepNet, SleepFM, Stanford Sleep Bench), domain adaptation frameworks (SE-MSResNet, DUDE, Varghese et al.), and pediatric XAI models (García-Vicente et al.). Q1 journals now expect one of: (a) methodological novelty, meaning a new architecture, learning paradigm, or adaptation strategy that outperforms these baselines; (b) rigorous validation (multi-center, prospective, cross-population, cross-dataset) that reveals limitations of existing models; or (c) clinical relevance, meaning alignment with diagnostic workflows, treatment decisions, or health equity, ideally shown through a translation study with real-world impact. The directions above are designed with these expectations in mind.

**On feasibility with the datasets**: Directions 2, 4, 5, and 8 are immediately feasible with the datasets already vetted as "Live" with accessible data. Direction 1 requires BDSP credentialing for the Human Sleep Project (119,234 recordings) but is otherwise the most impactful. Direction 3 requires DREAMT access (PhysioNet credentialing + DUA). Direction 7 is the most resource-intensive but also the most citable.

**On execution sequence**: Start with a focused study, Direction 4 (Pediatric) or Direction 5 (Audio), which have clear datasets and manageable scope. The pediatric multi-modal Transformer (NCH + CHAT) and multi-task audio (Shenzhen + PSG-Audio + MPSSC + SSBPR) are both immediately actionable. Use that study to establish the methodological pipeline and preliminary results, then expand to Direction 2 (cross-dataset validation) and Direction 1 (foundation model), which require more data engineering but yield higher-impact publications. Direction 7 (benchmarking) is best positioned as a follow-up once results from one or two focused studies are available.

**On clinical co-authorship**: For Q1 clinical journals (Sleep, Sleep Medicine Reviews), including a clinical co-author (sleep physician or sleep technologist) strengthens the submission considerably. The dataset inventory already includes clinically annotated data (PSG-IPA with 12 scorers, CPS with questionnaires, OSASUD with physician annotations), which suggests that clinical collaborations exist or can be established.

**On reproducibility**: Q1 journals increasingly require code and data availability statements. Several datasets are open access (Apnea-ECG, UCDDB, ISRUC, PSG-Audio, Shenzhen Multimodal, SSBPR, ONEI, MPSSC, Kaggle Snoring), which makes code release straightforward. For credentialed datasets (SHHS, MESA, NCH, DREAMT, Human Sleep Project), code can be released while noting data access requirements. The SynthSleepNet source code is already available on GitHub, providing a reference implementation for foundation model pretraining.

---

## Reconciliation Notes

Points where the two source documents overlapped or disagreed, and how they were handled here:

1. **Duplicate content**: The second document was the same "Filling the Gaps" text that formed the second half of the first document, written in second person. It is included once, in a neutral voice, merged into each direction.
2. **Human Sleep Project size**: The first document's opening section gave "20,000+ subjects"; the later sections gave "119,234 recordings from 90,000+ patients across five US academic medical centers". The later, more specific figure is used throughout. Worth confirming against the BDSP page before citing.
3. **Direction 8 novelty claim**: The original text said no study had examined adult-to-pediatric transfer and that cross-age transfer "remains unexplored", while the expanded text cites Niu et al. (2025) doing exactly that for audio. Section 8.1 is reworded to match.
4. **Scientific Data**: Listed twice in Direction 7 as "Scientific Data" and "Nature Scientific Data". These are the same journal and are merged.
5. **ONEI and MPSSC access**: ONEI is described as "available by request" in Direction 5 but listed as open access under reproducibility. The access terms for ONEI and MPSSC should be checked before writing a data availability statement.
6. **"Immediately feasible" vs. credentialed access**: Directions 2, 4, and 8 are called immediately feasible, yet they rely on SHHS, MESA, MrOS, and NCH, which the reproducibility paragraph lists as credentialed. Feasibility depends on those approvals already being in place.
7. **PSG-Audio size**: Given as a range (212–287 patients) in both documents; left as is.
8. **Stanford Sleep Bench**: The source grouped it with foundation models; it is a dataset and benchmark, so the novelty paragraph now says "foundation models and benchmarks".
