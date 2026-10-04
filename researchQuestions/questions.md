# Research Directions in Sleep Apnea Machine Learning and Deep Learning: An Evidence-Checked Revision

Date: 4 October 2026

## 1. Nature of the Revision

All eight research directions proposed in the original document are retained as topics. Five categories of claim in that document could not be substantiated, however, and have been removed or corrected. Each direction below distinguishes between findings that were confirmed and claims that were not.

| Claim in the original document | Deficiency | Treatment in this revision |
| --- | --- | --- |
| Statements that "the researcher has access to" the datasets | Most datasets require approval, credentialing or a request to the authors | Replaced by the access table in Section 2 |
| Novelty claims of the form "no study has…" | Several are contradicted by published work | Replaced by narrower research questions |
| Description of Directions 2, 4, 5 and 8 as "immediately feasible" | Feasibility depends on access that has not yet been obtained | Feasibility restated for each direction |
| Performance figures and citations for approximately 25 papers | Not verified against the papers themselves | Omitted unless confirmed; retained only as leads for verification |
| Journal impact factors | Approximate and in part incorrect | Removed; quartiles should be verified in JCR or Scimago |

In this document, "confirmed" denotes a fact observed on a publisher, repository or preprint page during the course of this project. "Not confirmed" denotes a claim whose only source is the original document.

## 2. Data Access

Only the first group of datasets listed below is available for immediate use. All others require an application that must be approved before work can commence.

| Access route | Datasets | Requirement |
| --- | --- | --- |
| Open download | Apnea-ECG, UCDDB, CinC 2018, PSG-Audio, Shenzhen multimodal, OSASUD, PSG-IPA, Kaggle snoring | None, or a free account |
| Form on the dataset website | ISRUC-Sleep | Acceptance of a data-use agreement |
| NSRR data request | SHHS, MESA, MrOS, WSC, CHAT | Registration and an approved request |
| Signed agreement on PhysioNet | DREAMT | Account and data use agreement |
| Credentialed PhysioNet access | NCH Sleep DataBank, CPS | Training certificate and agreement |
| Credentialed BDSP access | Human Sleep Project, Boston Children's Hospital Sleep Corpus | Training and agreement |
| Request to the authors | SSBPR, ONEI, MPSSC | Email request or research protocol |
| Not verified | PATS, Stanford Sleep Bench | Existence and terms were not confirmed |

The original document described SSBPR, ONEI and MPSSC as open access. The pages maintained for these datasets state otherwise.

The size of the Human Sleep Project could not be confirmed. Its public listing describes a collection that began with 15,000 to 19,000 patients from a single hospital and continues to grow. The figure of 119,234 recordings given in the original document was not located.

## 3. Direction 1: Foundation Models and Self-Supervised Pretraining

The principal gap asserted in the original document, namely that no model has been pretrained across multiple cohorts, is incorrect. The direction is valid as a field of inquiry but does not constitute a realistic first project.

**Confirmed findings**

- [SleepFM](https://www.nature.com/articles/s41591-025-04133-4) (Nature Medicine, 2026) was pretrained on more than 585,000 hours of polysomnography from approximately 65,000 participants across several cohorts, with SHHS withheld for external evaluation.
- Its reported performance on apnea tasks is modest: an accuracy of 0.87 for the presence of apnea and 0.69 for severity class.
- [SleepFM-2](https://arxiv.org/pdf/2609.06849), a 2026 preprint, draws on approximately two million hours from 26 polysomnography cohorts, including twelve NSRR datasets and the Human Sleep Project.
- A [2025 preprint](https://arxiv.org/pdf/2502.17481) applies hybrid self-supervised learning to EEG, EOG, EMG and ECG signals and evaluates apnea and hypopnea detection on SHHS.

**Unconfirmed claims removed**

- The apnea detection accuracy of 99.75% attributed to SynthSleepNet, together with the research question premised on exceeding it.
- The details provided for Stanford Sleep Bench and for the "low-burden" foundation model.
- The assertion that the Boston Children's Hospital corpus has never been used for pretraining.

**Revised research question.** Does fine-tuning an existing pretrained sleep encoder improve event-level detection of apneas and hypopneas on small clinical datasets, relative to training from scratch?

**Feasibility.** Fine-tuning a released model is achievable with modest computational resources, provided that the model weights are publicly available; this remains to be verified. Pretraining a new model is not achievable within the resources of this project.

## 4. Direction 2: Cross-Dataset Generalization

Cross-cohort evaluation of apnea detection models has already been conducted on the large public cohorts. The assertion in the original document that such evaluation "has not been performed" is therefore false. The question that remains open concerns the explanation of the observed decline in performance, not the demonstration that it occurs.

**Confirmed findings**

- [DRIVEN](https://communities.springernature.com/amp/posts/towards-automatic-home-based-sleep-apnea-estimation-using-deep-learning) was trained on SHHS and tested on MESA and MrOS.
- [UT-OSANet](https://arxiv.org/abs/2511.16169v1) used 9,021 recordings from MrOS, SHHS, MESA and CFS, with HomePAP reserved as an independent test set. Its authors observe that the prevalence of hypopneas differs between cohorts in a manner that reflects scoring practice.
- A [2021 study](https://arxiv.org/pdf/2101.04635) trained a model on 9,656 hospital polysomnograms and validated it externally on SHHS. It identifies a specific source of distribution shift: the use of nasal pressure versus thermistor as the primary scoring signal.
- [ApneaTime](https://research.hub.ku.edu.tr/entities/publication/dc48682e-ee07-4f51-b8fa-d0cda763ccb9) reports transfer from SHHS to MESA using domain-adversarial training.
- [Holter-to-Sleep](https://arxiv.org/pdf/2603.18714) was trained on MESA, MrOS and SHHS and tested on CFS, with an area under the curve for respiratory-event detection of 0.787 internally and 0.785 externally.

**Unconfirmed claims removed**

- The details provided for SE-MSResNet, DUDE, Varghese et al. and the AHI harmonisation framework.
- The sentences quoted from Sleep Medicine Reviews and other reviews.

**Revised research question.** What proportion of the cross-cohort decline in ECG-based and SpO2-based apnea detection is attributable to differences in hypopnea scoring rules, and what proportion persists after the labels have been harmonised?

**Feasibility.** A pilot study is possible at present using Apnea-ECG, UCDDB and OSASUD. The full question requires NSRR approval for at least two cohorts.

## 5. Direction 3: Wearable PPG Detection

This direction is valid but more limited than the original document suggests, because the only paired wearable dataset in the inventory comprises 100 participants. Claims regarding performance "across demographics" cannot be supported at that sample size.

**Confirmed findings**

- [DREAMT](https://physionet.org/content/dreamt/2.2.0/) pairs wearable recordings with polysomnography for 100 participants. The current version is 2.2.0 (June 2026), and access requires a signed agreement. The dataset was first released in 2024, not in April 2025 as stated in the original document.
- BIDMC consists of 53 eight-minute intensive-care recordings without apnea labels. It has been removed as a dataset for this direction.
- An [IEEE TBME study (2024)](https://doi.org/10.1109/TBME.2024.3378480) applied transfer learning to wrist PPG and accelerometry and reported slightly lower performance on wearable data than on clinical data.
- A [Computing in Cardiology paper (2024)](https://doi.org/10.22489/CinC.2024.307) evaluated convolutional networks on one-minute PPG segments from MESA.
- Published smartwatch validation studies, such as the [OPPO Watch study](https://doi.org/10.2147/NSS.S438065), rely on proprietary algorithms.

**Unconfirmed claims removed**

- The balanced accuracy of 62% attributed to Silva et al., together with the five-class formulation derived from it.
- The reference to "ECE12: Team Sleep", which appears to be a listing for a student project and not a publication.
- The sensitivity of 72.4% and the accuracy of 80.8% cited from other studies.
- The statement concerning FDA clearance, which was not independently verified.

**Revised research question.** Can an openly described model estimate moderate-to-severe obstructive sleep apnea from wrist PPG and accelerometry in DREAMT, and does pretraining on PPG from a large cohort such as MESA improve its performance?

**Feasibility.** The DREAMT agreement is required, as is NSRR approval if MESA is used. It should be confirmed that the release includes event-level apnea labels before the study is planned.

## 6. Direction 4: Pediatric Sleep Apnea

The datasets proposed for this direction were confirmed. None of the claims concerning the literature were confirmed, and the novelty of the direction is therefore unestablished. It is a reasonable candidate that requires a dedicated literature search before any commitment is made.

**Confirmed findings**

- The [NCH Sleep DataBank](https://www.physionet.org/content/nch-sleep/3.1.0/) contains 3,984 pediatric sleep studies from 3,673 patients (2017–2019) with linked clinical data. Access is credentialed.
- [CHAT](https://sleepdata.org/datasets/chat) enrolled 464 children aged 5 to 9.9 years with mild to moderate obstructive sleep apnea. Access is obtained by NSRR request.
- A Boston Children's Hospital Sleep Corpus is [listed on BDSP](https://registry.opendata.aws/bdsp_credentialed_projects/). Its size was not confirmed.
- [RASP](https://www.sleepdata.org/datasets/rasp), hosted on NSRR, compiles retrospective pediatric recordings from five sites. It was not included in the original document.

**Unconfirmed claims removed**

- All figures attributed to García-Vicente et al. (2026) and the quotation from that paper.
- The F1 and AUROC figures reported for the multi-modal Transformer on NCH and CHAT. That paper also appears to date from 2023, not 2025.
- The statements that no study has evaluated transfer from NCH to CHAT or the contribution of electronic health record variables.

**Revised research question.** Does a model trained on NCH generalize to CHAT for the classification of pediatric obstructive sleep apnea severity, and do linked clinical variables improve accuracy beyond that achieved with the signals alone?

**Limitation.** The two cohorts differ by design. NCH is a clinical population aged 0 to 18 years, whereas CHAT is a trial population with a narrow range of age and severity. Any decline in performance between them confounds model weakness with that difference.

**Feasibility.** PhysioNet credentialing and NSRR approval are both required. The study cannot begin immediately.

## 7. Direction 5: Audio and Smartphone Screening

The multi-task question posed in the original document cannot be executed as written, because no dataset contains all three types of label that it requires. A narrower audio question is one of the few in this document that can begin at present on open data.

**Confirmed findings**

- Apnea events scored from polysomnography are available in two open audio datasets: [PSG-Audio](https://www.scidb.cn/en/detail?dataSetId=778740145531650048) (212 patients according to its dataset page) and the [Shenzhen dataset](https://www.nature.com/articles/s41597-025-05583-8) (50 patients, more than 400 hours, recorded by smartphone and digital recorder).
- Snore-type labels are available only in MPSSC, and body-position labels only in SSBPR. Both datasets are released on request, and neither contains apnea event labels.
- The Kaggle snoring dataset comprises 1,000 one-second clips, of which 500 contain snoring. It is too small to serve as a pretraining corpus.
- [Le et al. (2023)](https://doi.org/10.2196/44818) classified 51% of hypopnea epochs correctly from breathing sounds, compared with 84% of apnea epochs.
- A [2026 study](https://mobile-systems.cl.cam.ac.uk/papers/JBHI26.pdf) of 194 PSG-Audio subjects compares tracheal and ambient microphones.

**Unconfirmed claims removed**

- The figures reported for the multi-task study of 157 nights, for the hybrid CNN-ResNet18 model, and the recall of 67.1% on MPSSC.
- The references to the Zenodo pipeline and the coordinate-attention paper.
- The assertion that cross-dataset validation of audio models has never been performed.

**Revised research question.** Does an apnea-event model trained on PSG-Audio transfer to smartphone audio in the Shenzhen dataset, and what proportion of the loss in performance is attributable to hypopneas?

**Feasibility.** Both datasets are open, and the study can therefore begin at present. Storage and computation for several hundred hours of audio require planning.

## 8. Direction 6: Explainable Artificial Intelligence

None of the literature cited for this direction was confirmed, and the datasets proposed are too small for the studies described. The direction is better treated as an analysis incorporated into another direction than as an independent project.

**Confirmed findings**

- [PSG-IPA](https://physionet.org/content/psg-ipa/1.0.0/) contains 20 recordings scored by 12 technologists; however, only five recordings were scored for respiratory events. This supports the measurement of inter-scorer disagreement but not training with label noise.
- OSASUD comprises 30 patients. CPS requires credentialed access and is centred on arousals.

**Unconfirmed claims removed**

- The chin-EMG study, the SHHS phenotyping study and POxi-SleepNet, together with all associated figures.
- The quotations attributed to reviews in Sleep and Breathing and Sleep Medicine Reviews.
- The assertions that no study has examined the stability of SHAP explanations or used it for out-of-distribution detection.

**Component withdrawn.** The clinician user study has been withdrawn. It requires ethics approval and the recruitment of sleep physicians, both of which would need to be arranged beforehand.

**Revised research question.** When an apnea detection model is applied to a new cohort, do its feature attributions shift in a manner that corresponds to the loss in accuracy? This question belongs within Direction 2.

## 9. Direction 7: Multi-Dataset Benchmarking

The statement that no multi-dataset benchmark exists is not established, and parts of the proposal cannot be constructed from the dataset inventory. A more limited evaluation protocol on open data is defensible.

**Confirmed findings**

- Multi-cohort evaluation of apnea models already exists in individual papers, including UT-OSANet and DRIVEN, as described under Direction 2.
- A [federated multi-task study](https://cinc.org/2025/Program/accepted/7.html) treats SHHS, APPLES, Sleep-EDF-X, HMC and DREAMT as five clients.
- The [Human Sleep Project listing](https://registry.opendata.aws/bdsp-hsp/) describes CAISR as covering sleep stages, arousals, apnea and hypopnea events, and limb movements. The original document stated that CAISR did not address apnea.
- The inventory contains no radar dataset; "radar" has accordingly been removed from the scope.

**Unconfirmed claims removed**

- The statement that "no comprehensive, multi-dataset benchmark currently exists".
- The description of Stanford Sleep Bench as a ready-made evaluation protocol.
- The proposal to compare ECG, SpO2, PPG and audio on the same subjects. The audio datasets and the large cohorts do not share subjects.

**Constraint.** Data use agreements for the large cohorts generally prohibit redistribution. A benchmark could therefore release code and split definitions but not data; each agreement should be consulted.

**Revised research question.** Under subject-wise data splits and separate reporting for apneas and hypopneas, how do published open-source apnea detection models rank on the open datasets, and how do the results compare with those reported in the original papers?

## 10. Direction 8: Adult-to-Pediatric Transfer

This direction is a combination of Directions 2 and 4 and does not constitute a separate project. The original document is also inconsistent regarding its novelty: it states that no study has examined adult-to-pediatric transfer and subsequently cites a study that does so.

**Confirmed findings**

- The pediatric datasets are those described under Direction 4. The adult cohorts are the NSRR datasets listed in the access table.

**Unconfirmed claims removed**

- The details of the two transfer-learning papers cited (Niu et al. and Haimov et al.), including the figures of 157 adult nights and 15 pediatric nights.
- The statement that "cross-age transfer remains unexplored".
- The question of pediatric-to-adult transfer, for which no rationale was provided.

**Revised research question.** Does pretraining on adult cohorts improve the classification of pediatric obstructive sleep apnea severity on NCH, relative to training on pediatric data alone?

**Limitation.** Pediatric scoring employs different event definitions and lower severity thresholds than adult scoring. The labels must be mapped before any transfer result can be interpreted.

**Feasibility.** Both NSRR approval and PhysioNet credentialing are required. The direction should be treated as a continuation of Direction 4.

## 11. Recommended Order of Work

Three of the revised questions can begin at present on open data, one of them only as a pilot; the remainder depend on access that has yet to be obtained. No direction should be adopted until a literature search on its exact revised question has been completed.

| Direction | Standing after revision | Earliest start |
| --- | --- | --- |
| 5. Audio transfer from PSG-Audio to the Shenzhen dataset | Feasible; novelty not yet verified | Immediately |
| 2. Cause of the cross-cohort decline | Feasible; the novelty lies in the explanation, not in the test | Pilot immediately; full study after NSRR approval |
| 7. Evaluation protocol on open data | Feasible; supports Directions 2 and 5 | Immediately |
| 4. Pediatric generalization from NCH to CHAT | Plausible; literature unverified | After credentialing and NSRR approval |
| 3. Wearable PPG on DREAMT | Valid; limited by a sample of 100 participants | After the DREAMT agreement |
| 8. Adult-to-pediatric transfer | Continuation of Direction 4 | After Direction 4 |
| 6. Explainability | Analysis within Direction 2 | Concurrently with Direction 2 |
| 1. Foundation models | Fine-tuning only; pretraining is not attainable | Conditional on public model weights |

The sequence proposed in the original document, which began with the pediatric and multi-task audio studies on the grounds that they were "immediately actionable", has been replaced. Neither study was actionable as described.

**An additional consideration.** Privacy-preserving training across cohorts was proposed earlier in this project as an unexplored avenue. That characterisation was incorrect: [federated multi-task training across five polysomnography datasets](https://www.mdpi.com/2076-3417/15/14/8077) and [federated ECG-based apnea detection](https://iris.unicampania.it/handle/11591/588366) have both been published. Whether formal differential-privacy guarantees have been investigated for apnea detection was not examined.

**Actions required**

- [ ] Select one revised research question.
- [ ] Conduct a dedicated literature search on that exact question.
- [ ] Submit the NSRR request, the PhysioNet credentialing application and the DREAMT agreement in parallel.
- [ ] Verify the removed citations before any of them is reused.
- [ ] Verify journal quartiles in JCR or Scimago before target journals are named.
