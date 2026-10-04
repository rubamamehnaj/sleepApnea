# Research Directions in Machine Learning and Deep Learning for Sleep Apnea

Date: 4 October 2026

## 1. Purpose and Basis

This document sets out eight research directions in the application of machine learning and deep learning to sleep apnea, ordered by how soon each can be undertaken. For each direction it states the rationale, the existing work that was identified, a specific research question, the data required and the principal limitations.

Statements about published studies and datasets are restricted to facts observed on publisher, repository or preprint pages. The literature was not searched systematically. No direction should therefore be regarded as novel until a dedicated literature search on its exact research question has been completed.

Two findings from the existing literature inform all eight directions:

- **Hypopneas are detected less reliably than apneas.** [Le et al. (2023)](https://doi.org/10.2196/44818) classified 51% of hypopnea epochs correctly from breathing sounds, compared with 84% of apnea epochs.
- **Scoring practice differs between cohorts.** The authors of [UT-OSANet](https://arxiv.org/abs/2511.16169v1) observe that the prevalence of hypopneas varies between cohorts in a manner that reflects scoring, and a [2021 study](https://arxiv.org/pdf/2101.04635) identifies the choice of scoring signal (nasal pressure or thermistor) as a source of distribution shift.

## 2. Data Resources and Access

The datasets relevant to these directions fall into seven access categories. Only those in the first category are available without an application.

| Access route | Datasets | Requirement |
| --- | --- | --- |
| Open download | Apnea-ECG, UCDDB, CinC 2018, PSG-Audio, Shenzhen multimodal, OSASUD, PSG-IPA, Kaggle snoring | None, or a free account |
| Form on the dataset website | ISRUC-Sleep | Acceptance of a data-use agreement |
| NSRR data request | SHHS, MESA, MrOS, WSC, CHAT, RASP | Registration and an approved request |
| Signed agreement on PhysioNet | DREAMT | Account and data use agreement |
| Credentialed PhysioNet access | NCH Sleep DataBank, CPS | Training certificate and agreement |
| Credentialed BDSP access | Human Sleep Project, Boston Children's Hospital Sleep Corpus | Training and agreement |
| Request to the authors | SSBPR, ONEI, MPSSC | Email request or research protocol |

Data use agreements for the large cohorts generally prohibit redistribution. Work based on them can release code and split definitions but not data, and each agreement should be consulted.

## 3. Direction 1: Transfer of Audio-Based Apnea Detection to Smartphone Recordings

**Rationale.** Breathing sounds offer a non-contact route to screening, but models are commonly developed on clinical microphones and their behaviour on consumer devices is uncertain.

**Existing work.** Apnea events scored from polysomnography are available in two open audio datasets: [PSG-Audio](https://www.scidb.cn/en/detail?dataSetId=778740145531650048), with 212 patients recorded by tracheal and ambient microphones, and the [Shenzhen dataset](https://www.nature.com/articles/s41597-025-05583-8), with 50 patients and more than 400 hours recorded by smartphone and digital recorder. A [2026 study](https://mobile-systems.cl.cam.ac.uk/papers/JBHI26.pdf) of 194 PSG-Audio subjects compares tracheal and ambient microphones.

**Research question.** Does an apnea-event model trained on PSG-Audio transfer to smartphone audio in the Shenzhen dataset, and what proportion of the loss in performance is attributable to hypopneas?

**Data and feasibility.** Both datasets are open, and the study can begin immediately. Storage and computation for several hundred hours of audio require planning.

**Limitations.** The Shenzhen dataset comprises 50 patients from a single hospital. Other snoring corpora cannot extend the study: MPSSC labels snore type, SSBPR labels body position, and neither contains apnea events.

## 4. Direction 2: Explaining the Cross-Cohort Decline in Performance

**Rationale.** Models that perform well on the cohort used for development frequently perform less well elsewhere. The existence of this decline is established; its causes are not.

**Existing work.** Cross-cohort evaluation has been reported on the large public cohorts. [DRIVEN](https://communities.springernature.com/amp/posts/towards-automatic-home-based-sleep-apnea-estimation-using-deep-learning) was trained on SHHS and tested on MESA and MrOS. UT-OSANet used 9,021 recordings from MrOS, SHHS, MESA and CFS, with HomePAP reserved as an independent test set. [ApneaTime](https://research.hub.ku.edu.tr/entities/publication/dc48682e-ee07-4f51-b8fa-d0cda763ccb9) reports transfer from SHHS to MESA using domain-adversarial training. [Holter-to-Sleep](https://arxiv.org/pdf/2603.18714) was trained on MESA, MrOS and SHHS and tested on CFS, with an area under the curve for respiratory-event detection of 0.787 internally and 0.785 externally.

**Research question.** What proportion of the cross-cohort decline in ECG-based and SpO2-based apnea detection is attributable to differences in hypopnea scoring rules, and what proportion persists after the labels have been harmonised?

**Data and feasibility.** A pilot study is possible immediately using Apnea-ECG, UCDDB and OSASUD. The full question requires NSRR approval for at least two cohorts.

**Limitations.** Scoring rules, recording devices and demographics vary together between cohorts, and their effects cannot be separated completely.

## 5. Direction 3: A Reproducible Evaluation Protocol on Open Data

**Rationale.** Reported results are difficult to compare because studies differ in how recordings are divided between training and testing and in the level at which performance is measured.

**Existing work.** Multi-cohort evaluation exists within individual papers, including those cited under Direction 2. A [federated multi-task study](https://cinc.org/2025/Program/accepted/7.html) treats SHHS, APPLES, Sleep-EDF-X, HMC and DREAMT as five clients. Whether a shared benchmark specific to apnea detection already exists was not determined.

**Research question.** Under subject-wise data splits and separate reporting for apneas and hypopneas, how do published open-source apnea detection models rank on the open datasets, and how do the results compare with those reported in the original papers?

**Data and feasibility.** The open datasets in Section 2 are sufficient, and the work can begin immediately. It also supplies the evaluation framework for Directions 1 and 2.

**Limitations.** The audio datasets and the signal datasets do not share subjects, so modalities cannot be compared on the same individuals.

## 6. Direction 4: Generalization of Pediatric Models

**Rationale.** Pediatric obstructive sleep apnea is scored with different event definitions and lower severity thresholds than adult disease, and models developed on adults cannot be assumed to apply.

**Existing work.** The [NCH Sleep DataBank](https://www.physionet.org/content/nch-sleep/3.1.0/) contains 3,984 pediatric sleep studies from 3,673 patients (2017–2019) with linked clinical data. [CHAT](https://sleepdata.org/datasets/chat) enrolled 464 children aged 5 to 9.9 years with mild to moderate obstructive sleep apnea. [RASP](https://www.sleepdata.org/datasets/rasp) compiles retrospective pediatric recordings from five sites, and a Boston Children's Hospital Sleep Corpus is [listed on BDSP](https://registry.opendata.aws/bdsp_credentialed_projects/). The published modelling literature on these datasets was not surveyed.

**Research question.** Does a model trained on NCH generalize to CHAT for the classification of pediatric obstructive sleep apnea severity, and do linked clinical variables improve accuracy beyond that achieved with the signals alone?

**Data and feasibility.** PhysioNet credentialing and NSRR approval are both required.

**Limitations.** The two cohorts differ by design. NCH is a clinical population aged 0 to 18 years, whereas CHAT is a trial population with a narrow range of age and severity. Any decline in performance between them confounds model weakness with that difference.

## 7. Direction 5: Apnea Detection from Wrist-Worn Sensors

**Rationale.** Wrist devices could extend screening to the home, but published validation studies of commercial watches, such as the [OPPO Watch study](https://doi.org/10.2147/NSS.S438065), rely on proprietary algorithms that cannot be reproduced.

**Existing work.** [DREAMT](https://physionet.org/content/dreamt/2.2.0/) pairs wearable recordings with polysomnography for 100 participants; the current version is 2.2.0 (June 2026). An [IEEE TBME study (2024)](https://doi.org/10.1109/TBME.2024.3378480) applied transfer learning to wrist PPG and accelerometry and reported slightly lower performance on wearable data than on clinical data. A [Computing in Cardiology paper (2024)](https://doi.org/10.22489/CinC.2024.307) evaluated convolutional networks on one-minute PPG segments from MESA.

**Research question.** Can an openly described model estimate moderate-to-severe obstructive sleep apnea from wrist PPG and accelerometry in DREAMT, and does pretraining on PPG from a large cohort such as MESA improve its performance?

**Data and feasibility.** The DREAMT agreement is required, as is NSRR approval if MESA is used. It should be confirmed that the release includes event-level apnea labels before the study is planned.

**Limitations.** A sample of 100 participants does not support conclusions about performance across demographic subgroups.

## 8. Direction 6: Transfer from Adult to Pediatric Cohorts

**Rationale.** Pediatric datasets are far smaller than adult cohorts. Pretraining on adult data is a natural means of compensating, provided that the differences in scoring are addressed.

**Existing work.** The pediatric datasets are those described under Direction 4, and the adult cohorts are the NSRR datasets listed in Section 2. The published literature on cross-age transfer was not surveyed.

**Research question.** Does pretraining on adult cohorts improve the classification of pediatric obstructive sleep apnea severity on NCH, relative to training on pediatric data alone?

**Data and feasibility.** Both NSRR approval and PhysioNet credentialing are required. The direction is a continuation of Direction 4 and should follow it.

**Limitations.** Adult and pediatric labels must be mapped to a common definition before any transfer result can be interpreted.

## 9. Direction 7: Attribution Shift as an Indicator of Generalization Failure

**Rationale.** A model whose reasoning changes when it is applied to a new population may be signalling that its predictions are no longer reliable. This can be examined without additional data collection.

**Existing work.** The literature on explainability in sleep apnea models was not surveyed. Among the available datasets, [PSG-IPA](https://physionet.org/content/psg-ipa/1.0.0/) contains 20 recordings scored by 12 technologists, of which five were scored for respiratory events; it supports the measurement of inter-scorer disagreement but is too small for model training.

**Research question.** When an apnea detection model is applied to a new cohort, do its feature attributions shift in a manner that corresponds to the loss in accuracy?

**Data and feasibility.** The question uses the models and cohorts of Direction 2 and is best conducted as part of that study.

**Limitations.** Attribution methods inherit the biases of the model they explain. Any study involving clinicians as evaluators would require ethics approval and recruitment.

## 10. Direction 8: Fine-Tuning Pretrained Sleep Models for Event Detection

**Rationale.** Large pretrained sleep models now exist, but their reported performance on apnea tasks is below that of task-specific models, which suggests that adaptation is worthwhile.

**Existing work.** [SleepFM](https://www.nature.com/articles/s41591-025-04133-4) (Nature Medicine, 2026) was pretrained on more than 585,000 hours of polysomnography from approximately 65,000 participants across several cohorts, with SHHS withheld for external evaluation. It reports an accuracy of 0.87 for the presence of apnea and 0.69 for severity class. [SleepFM-2](https://arxiv.org/pdf/2609.06849), a 2026 preprint, draws on approximately two million hours from 26 cohorts. A [2025 preprint](https://arxiv.org/pdf/2502.17481) applies hybrid self-supervised learning to EEG, EOG, EMG and ECG signals and evaluates apnea and hypopnea detection on SHHS.

**Research question.** Does fine-tuning an existing pretrained sleep encoder improve event-level detection of apneas and hypopneas on small clinical datasets, relative to training from scratch?

**Data and feasibility.** The direction is conditional on the public availability of model weights, which was not verified. Pretraining a new model at comparable scale is not attainable without credentialed access to many cohorts and substantial computation.

**Limitations.** Multi-cohort pretraining has already been carried out by well-resourced groups, and the scope for an original contribution lies in adaptation and evaluation only.

## 11. A Further Avenue: Privacy-Preserving Training Across Cohorts

The large cohorts are held under separate agreements, which makes them a natural setting for federated training. This avenue has already received attention: [federated multi-task training across five polysomnography datasets](https://www.mdpi.com/2076-3417/15/14/8077) and [federated ECG-based apnea detection](https://iris.unicampania.it/handle/11591/588366) have both been published. Whether formal differential-privacy guarantees and their effect on accuracy have been investigated for apnea detection was not examined, and a literature search on that point is required before the avenue is pursued.

## 12. Recommended Sequence

| Direction | Standing | Earliest start |
| --- | --- | --- |
| 1. Audio transfer to smartphone recordings | Feasible; novelty to be verified | Immediately |
| 2. Explaining the cross-cohort decline | Feasible; contribution lies in the explanation | Pilot immediately; full study after NSRR approval |
| 3. Evaluation protocol on open data | Feasible; supports Directions 1 and 2 | Immediately |
| 4. Generalization of pediatric models | Plausible; literature to be surveyed | After credentialing and NSRR approval |
| 5. Wrist-worn sensors | Valid; limited by sample size | After the DREAMT agreement |
| 6. Adult-to-pediatric transfer | Continuation of Direction 4 | After Direction 4 |
| 7. Attribution shift | Component of Direction 2 | Concurrently with Direction 2 |
| 8. Fine-tuning pretrained models | Conditional | If public model weights exist |

**Actions required**

- [ ] Select one research question.
- [ ] Conduct a dedicated literature search on that exact question.
- [ ] Submit the NSRR request, the PhysioNet credentialing application and the DREAMT agreement in parallel.
- [ ] Identify target journals and verify their quartiles in JCR or Scimago.
