# Machine Learning and Deep Learning in Sleep Apnea Research: A Literature Review (2021–2026)

As of 4 October 2026

## Summary

Machine learning can now score apnea and hypopnea events from polysomnography (PSG) at accuracies above 90% within a single dataset, but that performance rarely holds when a model is tested on a different cohort, device or scoring protocol. This is the central finding across the 60 sources reviewed here.

- **Automated PSG scoring** is the most mature line of work. Hospital-scale studies report 93–94% accuracy for event detection and severity grading.
- **Reduced-signal detection** from single-lead ECG, oximetry or both dominates the benchmark literature. Reported per-segment accuracy sits between 86% and 96% on the Apnea-ECG and UCD databases.
- **Audio, radar and wearables** aim at home screening. They estimate severity well for moderate-to-severe disease, while event-level sensitivity is lower: 67% for radar and 51% for hypopneas from breathing sounds.
- **Foundation models** trained on hundreds of thousands of hours of PSG appeared in 2025–2026. Apnea detection is one downstream task among many for these models.
- **Persistent weaknesses** are hypopnea detection, cross-cohort generalization, inconsistent evaluation, demographic bias and a near-total absence of prospective validation.

Several headline numbers come from sources that were not re-checked against the original papers. The Scope section and the reference table say which.

## Scope and sources

This review covers 60 sources published between 2021 and October 2026 that apply machine learning or deep learning to sleep apnea. It merges two inputs: the 56-entry paper list compiled for this project and a draft review that contributed four further systematic reviews.

The set is a curated sample, not a systematic search. Papers were gathered through general web search and the reference lists of dataset papers, so coverage is weighted toward the datasets in the project inventory. No PRISMA-style screening or quality appraisal was applied.

One paper sits outside the window by request: the INTERSPEECH 2017 challenge paper that introduced the Munich-Passau Snore Sound Corpus.

**How far each source was checked**

| Status | Sources | What it means |
| --- | --- | --- |
| Checked | 39 | Title, venue and key facts confirmed on a publisher, index or preprint page |
| Supplied, not re-checked | 18 | Citation and reported figures taken from the draft review or earlier lists |
| Reference lists only | 3 | Seen cited in other papers; bibliographic details confirmed, content not read |

Full texts were not read for most papers. Performance figures are quoted as the authors or abstracts report them and should be confirmed in the original before being cited. Twelve sources are preprints or arXiv-only papers that have not been peer reviewed.

## Background

Obstructive sleep apnea (OSA) is common and underdiagnosed because its reference test is expensive. Widely cited estimates put the number of affected adults near 936 million worldwide, with moderate-to-severe disease in 6–17% of the general adult population.

Diagnosis rests on attended polysomnography. A technician scores each night by hand, marking apneas (airflow stops for at least 10 seconds) and hypopneas (airflow falls, with a desaturation or arousal). The count per hour of sleep is the apnea-hypopnea index (AHI), and severity is graded at AHI thresholds of 5, 15 and 30.

This creates two distinct problems for machine learning:

- **Scoring automation.** Replace or assist the technician on full PSG.
- **Signal reduction.** Reach a usable diagnosis from fewer or cheaper signals, such as one ECG lead, a finger oximeter, a microphone, a radar or a watch.

Most of the literature addresses the second problem. Three evaluation levels recur and are not interchangeable: per-segment (is this 30- or 60-second window apneic), per-event (was this event found) and per-recording (is this patient's AHI above a threshold).

## Data resources

The field's results are shaped by a small number of public datasets, and the two most used are also the smallest. [Apnea-ECG](https://physionet.org/content/apnea-ecg/1.0.0/) has 70 single-lead recordings with per-minute labels, and the [UCD database](https://physionet.org/content/ucddb/1.0.0/) has 25 patients. Large cohorts such as [SHHS](https://sleepdata.org/datasets/shhs) and [MESA](https://sleepdata.org/datasets/mesa) need an approved data request and appear less often.

Nine sources in this review are dataset papers. They matter because each one opened a line of work that did not exist before it.

| Dataset paper | Year | Signal | Size | What it enabled |
| --- | --- | --- | --- | --- |
| [PSG-Audio](https://doi.org/10.1038/s41597-021-00977-w) (Korompili et al.) | 2021 | PSG with tracheal and ambient microphones | 212 patients | Audio apnea detection scored against full PSG |
| [OSASUD](https://doi.org/10.1038/s41597-022-01272-y) (Bernardini et al.) | 2022 | ECG, PPG, SpO2, vital signs | 30 stroke-unit patients | Per-second event labels on noisy real-world monitoring |
| [Shenzhen multimodal dataset](https://www.nature.com/articles/s41597-025-05583-8) | 2025 | Smartphone and recorder audio with PSG | 50 patients, 400+ hours | Bedside smartphone audio in a clinical setting |
| [SSBPR](https://arxiv.org/abs/2307.13346) (Xiao et al.) | 2023 | Snoring audio | 7,570 recordings, 6 body positions | Sleep position from snoring |
| [ONEI](https://link.springer.com/chapter/10.1007/978-981-99-8138-0_39) | 2023 | Snoring audio from OSAHS patients | Not checked | Breathing route and phase from snoring |
| [SimuSOE](https://arxiv.org/pdf/2407.07397) | 2024 | Snoring simulated while awake | Not checked | Severity screening without an overnight recording |
| [ICSD](https://arxiv.org/abs/2408.10561v3) (Liu et al.) | 2024 | Snoring and infant-cry audio | 3.3 hours strongly labelled | Snore event detection, no apnea labels |
| [Speech dataset for snoring detection](https://ieeexplore.ieee.org/document/10924987) | 2024 | Audio, 4 classes | Not checked | Normal versus abnormal snoring classification |
| [MPSSC](https://www.isca-archive.org/interspeech_2017/schuller17_interspeech.html) (Schuller et al.) | 2017 | Snore audio | 828 snore events, 4 classes | Snore excitation-site classification |

The audio datasets differ in what they label. Only PSG-Audio and the Shenzhen set carry apnea events scored from PSG. The others label snoring itself and support screening only indirectly.

## Automated PSG scoring and severity grading

Models given the respiratory channels of a full PSG now grade OSA severity with over 90% accuracy on held-out patients from the same hospital. The remaining errors concentrate in hypopneas.

| Study | Input | Model | Data | Reported result |
| --- | --- | --- | --- | --- |
| [Park et al. 2024](https://doi.org/10.1177/20552076241291707) | PSG channels | Perceptron layers around three LSTM layers | 1,000 PSGs (700 / 200 / 100 split) | AUC 0.94 at AHI thresholds of 5, 15 and 30 |
| [Yook et al. 2024](https://doi.org/10.1016/j.sleep.2024.01.015) | Nasal flow, SpO2, ECG, demographics | Xception CNN | Clinical PSG | 94% event accuracy; 93% severity accuracy |
| [Zovko et al. 2025](https://doi.org/10.3390/app15010376) | SpO2, heart rate, airflow | LSTM | Clinical PSG and oximetry, Split | Framework paper; figures not checked |
| Multi-centre study, 2023 | EEG and oral-nasal airflow | Deep network | Several sleep centres | 87.7% mean accuracy, varying by centre and device |
| [Two-tier framework, 2023](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10557519/) | PSG | Two-stage deep and classical models | Not checked | Not checked |

Park et al. and Yook et al. take different routes to the same task. The first models the night as a sequence with recurrent layers. The second treats short windows as images for a convolutional network and adds demographics.

Yook et al. report that misclassified patients were mostly those whose events were predominantly hypopneas. A hypopnea is a partial airflow reduction defined partly by its consequence, so it has a weaker signature than an apnea. The same weakness recurs in every modality reviewed below.

The 2023 multi-centre study is the most informative result in this group. Accuracy differed significantly between centres and recording devices, which single-centre studies cannot detect.

Newer preprints widen the task from apnea alone to the full scoring workload. [UT-OSANet](https://arxiv.org/abs/2511.16169v1) detects apneas, hypopneas, desaturations and arousals at event level. A [multi-task model](https://arxiv.org/pdf/2501.09519) scores sleep stages and events jointly, and [another](https://arxiv.org/pdf/2402.17788) is designed to keep working when a channel is missing or noisy.

Two neighbouring lines use other inputs. EEG-only classification is covered by a [2026 preprint](https://arxiv.org/pdf/2607.15477) and by the review of Fathima et al. (2025). Çil et al. (2025) predict severity from clinical variables alone in 750 inpatients, reporting an AUC of 0.966 with the Epworth score and lowest overnight saturation as leading predictors.

## Single-lead ECG detection

Single-lead ECG is the most studied reduced signal, with reported per-segment accuracy between 86% and about 93%. Almost all of those figures come from one 70-recording benchmark.

The physiological basis is that apneas produce cyclic changes in heart rate and R-wave amplitude. Models therefore take RR intervals, R-peak amplitudes or the raw trace as input.

| Study | Architecture | Data | Reported result |
| --- | --- | --- | --- |
| [Fang et al. 2022](https://doi.org/10.3390/life12010119) | Multi-scale residual network with focal loss | Apnea-ECG; UCD for generalization | 86.0% accuracy, 84.1% sensitivity, 87.1% specificity |
| [Chen et al. 2022 (SE-MSCNN)](https://github.com/Bettycxh/Toward-Sleep-Apnea-Detection-with-Lightweight-Multi-scaled-Fusion-Network) | Multi-scale CNN with channel attention | Apnea-ECG | Lightweight; code released |
| Liu et al. 2023 | CNN-Transformer | Not checked | Not checked |
| Chen et al. 2023 (RAFNet) | Restricted attention fusion | Not checked | Not checked |
| Srivastava et al. 2023 (ApneaNet) | 1D CNN with LSTM | Digitized ECG | Not checked |
| Hemrajani et al. 2023 | MobileNet V1 with GRU | Single-lead ECG | 90.29% accuracy; wearable prototype |
| Multi-scale CNN, 2025 | Multi-scale CNN with residual and channel attention | Two public datasets | 92.82% and 90.73% accuracy |
| SE-MSResNet, 2025 | Squeeze-and-excitation ResNet with adversarial domain generalization | Single-lead ECG | Not checked |
| [SApneaNet 2026](https://doi.org/10.3390/s26185936) | Wavelet scalograms into a CNN-Transformer with gated fusion | Single-lead ECG | Not checked |

Three design ideas account for most of the gains.

1. **Multiple time scales.** Feeding the labelled minute together with its neighbours lets the model see the slow cyclic pattern, as in Fang et al. and SE-MSCNN.
2. **Attention.** Channel attention and later Transformer layers weight the informative scales and time steps.
3. **Domain generalization.** SE-MSResNet treats each training subject as a domain and trains adversarially so features do not encode who the subject is.

The meta-analysis by Kilic et al. (2025) pooled 84 studies and found sensitivity and specificity above 90% per segment and near 97% per recording. It also found large variation between algorithms and frequent methodological bias.

The benchmark itself is a limitation. Apnea-ECG has 35 training recordings and labels each minute as a whole. A gain of one or two points on it says little about performance in a clinic population, and where a model is also tested on UCD, as in Zhang et al. (2025), accuracy is lower.

## Oximetry and multimodal fusion

Adding oxygen saturation to ECG gives the best reduced-signal results in this review, and SpO2 alone performs nearly as well on small benchmarks. Saturation is the most direct signal available outside a sleep laboratory, because desaturation is part of how hypopneas are defined.

[Zhang et al. (2025)](https://doi.org/10.2147/nss.s492806) fuse ECG and SpO2 in a multiscale Transformer with a cross-modal interaction module. On a hospital set of 510 patients they report 91.38% per-segment and 96.08% per-recording accuracy. Severity accuracy was 90.20%, 88.24% and 92.16% for mild, moderate and severe OSA.

The same model reached 95.04% per-segment accuracy on Apnea-ECG and 90.56% on UCD. The ordering is typical: the hospital cohort and UCD are harder than Apnea-ECG, so a benchmark figure overstates clinical performance.

[Liang et al. (2026)](https://doi.org/10.2174/0126662558475621260611103146) use single-channel SpO2 with a pruned CNN-Transformer. They report 95.77% accuracy, 95.02% sensitivity and 96.18% specificity on UCD. That database has 25 patients, so the result needs confirmation on a larger cohort.

Yook et al. (2024), discussed above, also found that nasal flow with SpO2 was the strongest feature set. An [out-of-distribution study](https://arxiv.org/pdf/2608.12229) of PPG and SpO2 models tested on the OSASUD stroke-unit data addresses the opposite question: how much is lost when the population changes.

## Audio and breathing-sound screening

Breathing sounds recorded by a phone or bedside microphone can separate moderate-to-severe OSA from normal sleep, but they detect individual hypopneas poorly. This line of work grew quickly after PSG-Audio made PSG-scored audio public in 2021.

| Study | Audio source | Model | Data | Reported result |
| --- | --- | --- | --- | --- |
| [JAMA Otolaryngology study, 2022](https://pmc.ncbi.nlm.nih.gov/articles/PMC9011176/) | Smartphone, about 1 m from the head, during in-lab PSG | Classical models on 508 acoustic features | 423 patients | Severity prediction at standard AHI thresholds |
| [Le et al. 2023](https://doi.org/10.2196/44818) | PSG microphone and smartphone | Deep network trained with added home noise | 1,018 PSG audio sets, 297 smartphone sets, 22,500 noise clips | Epoch accuracy 92% no-event, 84% apnea, 51% hypopnea |
| [ASMM-OSA 2024](https://doi.org/10.3389/fnins.2024.1336307) | Snoring audio | Audio and text-embedding features into XGBoost | Hospital cohort | Four-class severity classification |
| [PSG-Audio screening study, 2025](https://www.sciencedirect.com/science/article/abs/pii/S1746809424015301) | PSG-Audio | ConvNeXt with LSTM on 9-second windows | 50-subject independent test set | Estimated versus PSG AHI, r = 0.804 |
| [Cambridge study, 2026](https://mobile-systems.cl.cam.ac.uk/papers/JBHI26.pdf) | PSG-Audio, tracheal and ambient | Event detection pipeline | 194 subjects, 850+ hours | Severe OSA screening: sensitivity 0.84, specificity 0.97 |
| Sleep Medicine study, 2025 | Tracheal sounds | Transfer learning on six pretrained CNNs | Not checked | 83.66% accuracy separating obstructive from central events |
| Neck-sensor pilot, 2025 | Piezoelectric vibration sensor | 1D CNN and GRU | Pilot cohort | 92% accuracy for silence, snoring and noise |

Le et al. give the clearest picture of where audio fails. Of true hypopnea epochs, 15% were called apnea and 34% were called no-event. A partial obstruction often sounds like ordinary breathing.

Two design choices stand out. Le et al. train with injected household noise so the model survives outside the laboratory. And evaluation moves from event accuracy to AHI correlation and severity screening, where audio performs acceptably.

The Sleep Medicine study addresses a question the others skip: whether an event is obstructive or central. That distinction changes treatment and is rarely attempted from reduced signals.

Smaller contributions include a [comparison of deep models on PSG-Audio](https://www.jicce.org/journal/view.html?uid=1321&vmd=Full) and a [recall-first CNN preprint](https://arxiv.org/pdf/2510.00052) for snoring-based screening. The snoring corpora in the Data resources section support a parallel literature on snore type and body position, which informs treatment choice more than diagnosis.

## Contactless and wearable sensing

Radar and wrist devices estimate AHI closely enough to grade severity, though the one study reporting event-level sensitivity missed a third of events. They are the least mature modalities and the ones closest to consumer products.

| Study | Sensor | Model | Data | Reported result |
| --- | --- | --- | --- | --- |
| [Choi et al. 2024](https://doi.org/10.1093/sleep/zsae184) | Radar | CNN-Transformer | 54 development, 35 temporally separate test patients | Event sensitivity 67.2%; AHI correlation r = 0.892; severity agreement κ = 0.780 |
| [OPPO Watch study, 2024](https://doi.org/10.2147/NSS.S438065) | Watch PPG, accelerometer, snoring audio | Proprietary machine learning model | Compared with PSG | Screening performance; figures not checked |
| [Kim et al. 2025](https://pure.skku.edu/en/publications/aienhanced-smartwatch-ahi-estimation-and-aiscored-polysomnography/) | Smartwatch | Proprietary AHI estimator | 90 Korean adults with simultaneous PSG | High concordance, best for moderate-to-severe OSA |
| [IEEE TBME study, 2024](https://doi.org/10.1109/TBME.2024.3378480) | Wrist PPG and accelerometer | Deep CNN with transfer learning | Clinical and wearable recordings | Slightly worse on wearable than clinical data |
| [Computing in Cardiology, 2024](https://doi.org/10.22489/CinC.2024.307) | Finger PPG from MESA | AlexNet, ZF-Net, custom CNN | One-minute segments | Feasibility study |
| [AcceleRest, 2026 preprint](https://www.medrxiv.org/content/10.64898/2026.01.28.26345056v1) | Wrist accelerometer | Masked autoencoder | Several cohorts including DREAMT | Not checked |

Choi et al. show the pattern for the whole group. The model found 67.2% of events, yet its AHI estimate had a mean absolute error of 7.54 events per hour and an intraclass correlation of 0.889 with PSG. Missed and spurious events partly cancel over a night, so severity grading is more forgiving than event detection.

Kim et al. is notable for its validation design. The algorithm was trained on South American cohorts and tested on Korean adults, a real cross-population test that most studies lack.

Two systematic reviews cover this area. Osa-Sanchez et al. (2025) screened 249 studies from 2020–2024 and included 28. They found a trend toward patches, watches and rings paired with CNNs and transfer learning.

Abd-Alrazaq et al. (2024) pooled wearable studies and found classical machine learning at 0.896 mean accuracy against 0.849 for deep learning. Studies with more than 100 participants reached 0.905 against 0.838 for smaller ones. Both gaps suggest that sample size, not architecture, limits wearable performance.

## Foundation models and self-supervised learning

The largest shift since 2025 is pretraining on unlabelled sleep recordings at a scale no labelled apnea dataset approaches. Apnea detection is a secondary result in these papers, and their apnea figures are below those of specialised models.

[SleepFM (Thapa et al. 2026)](https://www.nature.com/articles/s41591-025-04133-4) was trained by contrastive learning on more than 585,000 hours of PSG from about 65,000 participants across several cohorts. Its main claim is prediction of future disease risk from one night of sleep.

On standard tasks SleepFM reached mean F1 scores of 0.70–0.78 for sleep staging. Accuracy was 0.87 for apnea presence and 0.69 for severity class. SHHS was held out of pretraining and used to test transfer.

[SleepFM-2](https://arxiv.org/pdf/2609.06849), a 2026 preprint, extends pretraining to about two million hours from 26 PSG cohorts plus wrist accelerometry. Its cohort list includes twelve NSRR datasets and the Human Sleep Project.

A [2025 preprint](https://arxiv.org/pdf/2502.17481) proposes a hybrid self-supervised framework over EEG, EOG, EMG and ECG. It evaluates apnea and hypopnea detection on SHHS as separate downstream tasks. AcceleRest applies the same idea to wrist accelerometry with a masked autoencoder.

Three points follow for apnea research.

- **Label efficiency is the benefit.** A pretrained encoder needs fewer scored nights to reach a given accuracy, which matters most for small clinical datasets.
- **Generic pretraining does not solve event scoring.** A severity accuracy of 0.69 is well below the 93% reported by task-specific PSG models, although the datasets differ.
- **Entry cost is high.** These models depend on credentialed access to many cohorts and on compute beyond most academic groups.

## What the evidence syntheses conclude

The eleven reviews in this set agree on two things: pooled accuracy is high, and the methods behind it are inconsistent.

| Review | Scope | Studies included | Main conclusion |
| --- | --- | --- | --- |
| [Tyagi and Agarwal 2023](https://doi.org/10.1007/s13534-023-00297-5) | Deep learning on SpO2, ECG, airflow and sound | 47 (2012–2022) | Taxonomy by signal type and architecture |
| Kilic et al. 2025 | ECG-based detection, meta-analysis | 84 (to November 2023) | Pooled sensitivity and specificity above 90% per segment; high heterogeneity and bias |
| Fathima et al. 2025 | EEG-based detection | 63 of 402 screened | Promising; signal decomposition, feature selection and cross-population testing need work |
| Osa-Sanchez et al. 2025 | Wearable sensors with AI | 28 of 249 screened | Trend to patches, watches and rings with CNNs and transfer learning |
| Abd-Alrazaq et al. 2024 | Wearable AI, meta-analysis | Not checked | Pooled accuracy 0.896 for classical models, 0.849 for deep learning |
| [Systematic review, 2026](https://www.sciencedirect.com/science/article/pii/S2667305326000670) | Machine learning techniques overall | Not checked | Deep models exceed 85% accuracy in many studies; multimodal designs are scarce |
| Narrative review preprint, 2025 | Machine learning in OSA, 2018–2023 | 254 | Deep learning most used, then SVM; cohorts skew toward particular demographics |
| IEEE Access study, 2024 | Deep versus shallow models | Not checked | CNN, SVM and ANN generally lead |

Two IEEE conference reviews from 2024 and a [2026 book chapter](https://link.springer.com/chapter/10.1007/978-3-032-06777-7_9) cover similar ground. Their citations in the source list are incomplete or unchecked, so they are not summarised here.

The reviews converge on four criticisms.

- **Heterogeneous evaluation.** Studies differ in window length, split strategy and metric, so pooled figures mix unlike quantities.
- **Small samples.** Larger studies report higher accuracy in the wearable meta-analysis, which suggests many models are data-limited.
- **Narrow cohorts.** The 2025 narrative review found demographic gaps in the populations studied.
- **Single-signal designs.** Few studies combine modalities or test what happens when one fails.

## Cross-cutting limitations

Six weaknesses appear across modalities, and each one makes the published accuracy figures an upper bound on real-world performance.

1. **Hypopneas are the common failure.** Yook et al. traced their errors to hypopnea-dominant patients. Le et al. classified only 51% of hypopnea epochs correctly from audio. Papers that report a single apnea-plus-hypopnea figure hide this.
2. **Performance drops across datasets.** The 2023 multi-centre study found significant differences between centres and devices. Zhang et al. lost about 4.5 points moving from Apnea-ECG to UCD. The IEEE TBME study did worse on wearable than clinical data.
3. **Evaluation levels are mixed.** Per-segment, per-event and per-recording results are reported interchangeably. Choi et al. show how far they diverge: 67% event sensitivity alongside 0.89 AHI correlation.
4. **Benchmarks are small and old.** Apnea-ECG dates from 2000 and has 70 recordings. UCD has 25 patients. Results on them are sensitive to how recordings are split.
5. **Labels are not uniform.** Cohorts were scored under different hypopnea rules, so the same night can yield different AHI values. Cross-cohort comparisons inherit that difference.
6. **Validation is retrospective.** Nearly every study tests on archived recordings. The commercial watch algorithms are proprietary, so their results cannot be reproduced.

Two topics are thin in this set. Only one study separates obstructive from central events. Interpretability is raised in the reviews but is not the focus of any primary study here.

Pediatric OSA is absent from the primary studies reviewed, although public pediatric cohorts exist.

## Research gaps

The gaps below follow directly from the limitations above and are the questions this body of work leaves open.

| Gap | Evidence in this review | What a study would need |
| --- | --- | --- |
| Hypopnea-specific performance | 51% hypopnea accuracy from audio; errors cluster in hypopnea-dominant patients | Separate apnea and hypopnea metrics; models that use desaturation and arousal context |
| Cross-cohort generalization | Accuracy falls between datasets, centres and devices | Train on one cohort, test on others, with harmonised scoring rules |
| Standard evaluation | Reviews report heterogeneous splits and metrics | Subject-independent splits and all three evaluation levels on shared data |
| Home-recorded audio | Most audio is recorded in a sleep laboratory | PSG-scored recordings from bedrooms, across several nights |
| Open wearable algorithms | Watch studies use proprietary models; paired public data is small | Open models on paired wearable and PSG data, tested across populations |
| Fine-tuning foundation models for event scoring | SleepFM reaches 0.69 severity accuracy without task-specific design | Event-level fine-tuning and label-efficiency tests on small clinical sets |
| Obstructive versus central events | One study in this set | Event-type labels in reduced-signal datasets |
| Pediatric populations | No primary study in this set | Models trained or adapted on pediatric cohorts |
| Training across restricted cohorts | Large cohorts sit under separate data agreements; no source here pools them without centralising data | Federated or privacy-preserving training across cohorts |
| Prospective and outcome studies | Nearly all validation is retrospective | Blinded prospective comparison with PSG; effect on diagnosis and treatment |

The first three gaps can be studied with data that is already public. The others depend on new data collection or on credentialed access.

## References

All 60 sources, newest first. Status follows the definitions in Scope and sources. Entries without a link had no confirmed URL.

| # | Reference | Year | Type | Status |
| --- | --- | --- | --- | --- |
| 1 | Liang Y, Zhang C, Hu H, Bai X. [A Lightweight CNN-Transformer Model for Obstructive Sleep Apnea Detection Using Single-Channel SpO2 Signals](https://doi.org/10.2174/0126662558475621260611103146). Journal with ISSN 2666-2558 | 2026 | Original study | Checked |
| 2 | Thapa R, Kjaer MR, He B, Covert I, Moore H, Hanif U, et al. [A multimodal sleep foundation model for disease prediction (SleepFM)](https://www.nature.com/articles/s41591-025-04133-4). Nature Medicine 32(2):752-762 | 2026 | Original study | Checked |
| 3 | [AcceleRest: A Physiology-Aware Masked Autoencoder for Wrist Accelerometer-based Sleep Staging and Apnea Evaluation](https://www.medrxiv.org/content/10.64898/2026.01.28.26345056v1). medRxiv | 2026 | Preprint | Checked |
| 4 | [Apnea Burden-Guided Framework: Enhancing Out-of-Distribution Generalization in PPG-Based Sleep Apnea Characterization](https://arxiv.org/pdf/2608.12229). arXiv 2608.12229 | 2026 | Preprint | Checked |
| 5 | [Artificial Intelligence in Sleep Apnea Detection: A Review](https://link.springer.com/chapter/10.1007/978-3-032-06777-7_9). Springer book chapter | 2026 | Review | Checked |
| 6 | University of Cambridge Mobile Systems group. [Continuous Mobile Audio Monitoring for Sleep Apnea Detection](https://mobile-systems.cl.cam.ac.uk/papers/JBHI26.pdf). IEEE JBHI, per author PDF | 2026 | Original study | Checked |
| 7 | [Deep Learning Approaches for Sleep Apnea Classification from Polysomnographic EEG Signals](https://arxiv.org/pdf/2607.15477). arXiv 2607.15477 | 2026 | Preprint | Checked |
| 8 | [Learning transferable human physiology from two million hours of sleep with SleepFM-2](https://arxiv.org/pdf/2609.06849). arXiv 2609.06849 | 2026 | Preprint | Checked |
| 9 | [Machine learning techniques in sleep apnea detection: A systematic review](https://www.sciencedirect.com/science/article/pii/S2667305326000670). Elsevier journal | 2026 | Review | Checked |
| 10 | [SApneaNet: Adaptive Squeeze-and-Excitation-Based CNN-Transformer Network with AGFF for Sleep Apnea Event Detection Using ECG Images Under IoMT](https://doi.org/10.3390/s26185936). Sensors 26(18):5936 | 2026 | Original study | Checked |
| 11 | [A multimodal dataset for training deep learning models aimed at detecting and analyzing sleep apnea](https://www.nature.com/articles/s41597-025-05583-8). Scientific Data 12:1263 | 2025 | Dataset paper | Checked |
| 12 | A novel obstructive sleep apnea detection model based on multi-scale convolutional neural networks. Expert Systems with Applications, as supplied | 2025 | Original study | Supplied, not re-checked |
| 13 | [A Recall-First CNN for Sleep Apnea Screening from Snoring Audio](https://arxiv.org/pdf/2510.00052). arXiv 2510.00052 | 2025 | Preprint | Checked |
| 14 | Zovko K, Sadowski Y, Perkovic T, Solic P, Pavlinac Dodig I, Pecotic R, Dogas Z. [Advanced Data Framework for Sleep Medicine Applications: Machine Learning-Based Detection of Sleep Apnea Events](https://doi.org/10.3390/app15010376). Applied Sciences 15(1):376 | 2025 | Original study | Checked |
| 15 | Kim et al. [AI-Enhanced Smartwatch AHI Estimation and AI-Scored Polysomnography for Obstructive Sleep Apnea: Real-World Validation](https://pure.skku.edu/en/publications/aienhanced-smartwatch-ahi-estimation-and-aiscored-polysomnography/). Nature and Science of Sleep | 2025 | Original study | Checked |
| 16 | Zhang Y, Zhou L, Zhu S, et al. [Deep Learning for Obstructive Sleep Apnea Detection and Severity Assessment: A Multimodal Signals Fusion Multiscale Transformer Model](https://doi.org/10.2147/nss.s492806). Nature and Science of Sleep 17:1-15 | 2025 | Original study | Checked |
| 17 | Kilic ME, Arayici ME, Turan OE, Yilancioglu YR, Ozcan EE, Yilmaz MB. Diagnostic accuracy of machine learning algorithms in electrocardiogram-based sleep apnea detection: A systematic review and meta-analysis. Sleep Medicine Reviews 81:102097 | 2025 | Review | Supplied, not re-checked |
| 18 | Distinguishing severe sleep apnea from habitual snoring using a neck-wearable piezoelectric sensor and deep learning: A pilot study. Computers in Biology and Medicine | 2025 | Original study | Supplied, not re-checked |
| 19 | [Multi-task deep-learning for sleep event detection and stage classification](https://arxiv.org/pdf/2501.09519). arXiv 2501.09519 | 2025 | Preprint | Checked |
| 20 | Cil B, Irmak H, Kabak M. Predicting the severity of obstructive sleep apnea using artificial intelligence tools. Annals of Thoracic Medicine 20(4):254-261 | 2025 | Original study | Supplied, not re-checked |
| 21 | [Screening for obstructive sleep apnea hypopnea using sleep breathing sounds based on the PSG-audio dataset](https://www.sciencedirect.com/science/article/abs/pii/S1746809424015301). Biomedical Signal Processing and Control | 2025 | Original study | Checked |
| 22 | SE-MSResNet: A lightweight squeeze-and-excitation multi-scaled ResNet with domain generalization for sleep apnea detection. Neurocomputing 620:129201 | 2025 | Original study | Supplied, not re-checked |
| 23 | Separating obstructive and central respiratory events during sleep using breathing sounds: Utilizing transfer learning on deep convolutional networks. Sleep Medicine 131:106485 | 2025 | Original study | Supplied, not re-checked |
| 24 | Fathima S, et al. Sleep Apnea Detection Using EEG: A Systematic Review of Datasets, Methods, Challenges, and Future Directions. Annals of Biomedical Engineering 53(5):1043-1067 | 2025 | Review | Supplied, not re-checked |
| 25 | [Sleep Apnea Detection Using Respiratory Sound Data Based on Deep Learning Models](https://www.jicce.org/journal/view.html?uid=1321&vmd=Full). Journal of Information and Communication Convergence Engineering | 2025 | Original study | Checked |
| 26 | Status and Opportunities of Machine Learning Applications in Obstructive Sleep Apnea: A Narrative Review. Preprint, March 2025 | 2025 | Review | Supplied, not re-checked |
| 27 | [Toward Foundational Model for Sleep Analysis Using a Multimodal Hybrid Self-Supervised Learning Framework](https://arxiv.org/pdf/2502.17481). arXiv 2502.17481 | 2025 | Preprint | Checked |
| 28 | Wang Z, Bao X, Zhao C, Zhang J, Ai S, Li Y. [UT-OSANet: A Multimodal Deep Learning model for Evaluating and Classifying Obstructive Sleep Apnea](https://arxiv.org/abs/2511.16169v1). arXiv 2511.16169 | 2025 | Preprint | Checked |
| 29 | Osa-Sanchez A, et al. Wearable Sensors and Artificial Intelligence for Sleep Apnea Detection: A Systematic Review. Journal of Medical Systems 49(1):66 | 2025 | Review | Supplied, not re-checked |
| 30 | Park MJ, Choi JH, Kim SY, Ha TK. [A deep learning algorithm model to automatically score and grade obstructive sleep apnea in adult polysomnography](https://doi.org/10.1177/20552076241291707). Digital Health 10 | 2024 | Original study | Supplied, not re-checked |
| 31 | [A deep transfer learning approach for sleep stage classification and sleep apnea detection using wrist-worn consumer sleep technologies](https://doi.org/10.1109/TBME.2024.3378480). IEEE Transactions on Biomedical Engineering | 2024 | Original study | Checked |
| 32 | Choi JW, Koo DL, Kim DH, et al. [A novel deep learning model for obstructive sleep apnea diagnosis: hybrid CNN-Transformer approach for radar-based detection of apnea-hypopnea events](https://doi.org/10.1093/sleep/zsae184). SLEEP 47(12):zsae184 | 2024 | Original study | Supplied, not re-checked |
| 33 | [A Speech Dataset for Snoring Detection in Sleep Based on Deep Learning](https://ieeexplore.ieee.org/document/10924987). IEEE conference, Xplore 10924987 | 2024 | Dataset paper | Checked |
| 34 | A Systematic Literature on Recent Advancement in Deep Learning to Diagnose Obstructive Sleep Apnea. IEEE conference, 14-15 March 2024 | 2024 | Review | Supplied, not re-checked |
| 35 | [An audio-semantic multimodal model for automatic obstructive sleep Apnea-Hypopnea Syndrome classification via multi-feature analysis of snoring sounds (ASMM-OSA)](https://doi.org/10.3389/fnins.2024.1336307). Frontiers in Neuroscience | 2024 | Original study | Checked |
| 36 | [Comparison of OPPO Watch Sleep Analyzer and Polysomnography for Obstructive Sleep Apnea Screening](https://doi.org/10.2147/NSS.S438065). Nature and Science of Sleep 16:125-141 | 2024 | Original study | Checked |
| 37 | Deep and Shallow Learning Model-Based Sleep Apnea Diagnosis Systems: A Comprehensive Study. IEEE Access | 2024 | Review | Supplied, not re-checked |
| 38 | Yook S, Kim D, Gupte C, Joo EY, Kim H. [Deep learning of sleep apnea-hypopnea events for accurate classification of obstructive sleep apnea and determination of clinical severity](https://doi.org/10.1016/j.sleep.2024.01.015). Sleep Medicine 114:211-219 | 2024 | Original study | Supplied, not re-checked |
| 39 | Abd-Alrazaq A, Aslam H, AlSaad R, Alsahli M, Ahmed A, Damseh R, Aziz S, Sheikh J. Detection of Sleep Apnea Using Wearable AI: Systematic Review and Meta-Analysis. Journal of Medical Internet Research 26:e58187 | 2024 | Review | Supplied, not re-checked |
| 40 | Detection of Sleep Apnea: A Comparative Analysis of Advanced Machine Learning and Deep Learning Approaches. IEEE conference, 6-8 November 2024 | 2024 | Review | Supplied, not re-checked |
| 41 | Liu Q, et al. [ICSD: An Open-source Dataset for Infant Cry and Snoring Detection](https://arxiv.org/abs/2408.10561v3). arXiv 2408.10561 | 2024 | Dataset paper | Checked |
| 42 | [Multimodal Sleep Apnea Detection with Missing or Noisy Modalities](https://arxiv.org/pdf/2402.17788). arXiv 2402.17788 | 2024 | Preprint | Checked |
| 43 | [SimuSOE: A Simulated Snoring Dataset for Obstructive Sleep Apnea-Hypopnea Syndrome Evaluation during Wakefulness](https://arxiv.org/pdf/2407.07397). arXiv 2407.07397 | 2024 | Dataset paper | Checked |
| 44 | [Sleep Apnea Detection - Towards Wearables](https://doi.org/10.22489/CinC.2024.307). Computing in Cardiology 2024, vol. 51 | 2024 | Conference paper | Checked |
| 45 | A deep learning model developed for sleep apnea detection: A multi-center study. Biomedical Signal Processing and Control | 2023 | Original study | Supplied, not re-checked |
| 46 | Xiao L, Yang X, Li X, Tu W, Chen X, Yi W, Lin J, et al. [A Snoring Sound Dataset for Body Position Recognition: Collection, Annotation, and Analysis (SSBPR)](https://arxiv.org/abs/2307.13346). INTERSPEECH 2023 | 2023 | Dataset paper | Checked |
| 47 | Srivastava G, et al. ApneaNet: A hybrid 1DCNN-LSTM architecture for detection of Obstructive Sleep Apnea using digitized ECG signals. Biomedical Signal Processing and Control 84:104754 | 2023 | Original study | Reference lists only |
| 48 | Liu H, et al. Detection of obstructive sleep apnea from single-channel ECG signals using a CNN-transformer architecture. Biomedical Signal Processing and Control 82 | 2023 | Original study | Reference lists only |
| 49 | Hemrajani P, et al. Efficient Deep Learning Based Hybrid Model to Detect Obstructive Sleep Apnea. Sensors 23(10):4692 | 2023 | Original study | Supplied, not re-checked |
| 50 | [ONEI: Unveiling Route and Phase of Breathing from Snoring Sounds](https://link.springer.com/chapter/10.1007/978-981-99-8138-0_39). Springer conference chapter | 2023 | Dataset paper | Checked |
| 51 | Chen Y, et al. RAFNet: Restricted attention fusion network for sleep apnea detection. Neural Networks 162 | 2023 | Original study | Reference lists only |
| 52 | Le VL, Kim D, Cho E, Jang H, Reyes RD, Kim H, Lee D, Yoon IY, Hong J, Kim JW. [Real-Time Detection of Sleep Apnea Based on Breathing Sounds and Prediction Reinforcement Using Home Noises: Algorithm Development and Validation](https://doi.org/10.2196/44818). Journal of Medical Internet Research 25:e44818 | 2023 | Original study | Checked |
| 53 | [Sleep disorder and apnea events detection framework with high performance using two-tier learning model design](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10557519/). PeerJ Computer Science | 2023 | Original study | Checked |
| 54 | Tyagi PK, Agarwal D. [Systematic review of automated sleep apnea detection based on physiological signal data using deep learning algorithm: a meta-analysis approach](https://doi.org/10.1007/s13534-023-00297-5). Biomedical Engineering Letters 13(3):293-312 | 2023 | Review | Checked |
| 55 | [Evaluating Prediction Models of Sleep Apnea From Smartphone-Recorded Sleep Breathing Sounds](https://pmc.ncbi.nlm.nih.gov/articles/PMC9011176/). JAMA Otolaryngology-Head and Neck Surgery | 2022 | Original study | Checked |
| 56 | Bernardini A, et al. [OSASUD: A dataset of stroke unit recordings for the detection of Obstructive Sleep Apnea Syndrome](https://doi.org/10.1038/s41597-022-01272-y). Scientific Data | 2022 | Dataset paper | Checked |
| 57 | Fang H, Lu C, Hong F, Jiang W, Wang T. [Sleep Apnea Detection Based on Multi-Scale Residual Network](https://doi.org/10.3390/life12010119). Life 12(1):119 | 2022 | Original study | Checked |
| 58 | Chen X, et al. [Toward sleep apnea detection with lightweight multi-scaled fusion network (SE-MSCNN)](https://github.com/Bettycxh/Toward-Sleep-Apnea-Detection-with-Lightweight-Multi-scaled-Fusion-Network). Knowledge-Based Systems 247 | 2022 | Original study | Checked |
| 59 | Korompili G, et al. [PSG-Audio, a scored polysomnography dataset with simultaneous audio recordings for sleep apnea studies](https://doi.org/10.1038/s41597-021-00977-w). Scientific Data | 2021 | Dataset paper | Checked |
| 60 | Schuller B, Steidl S, Batliner A, Bergelson E, Krajewski J, Janott C, et al. [The INTERSPEECH 2017 Computational Paralinguistics Challenge: Addressee, Cold and Snoring](https://www.isca-archive.org/interspeech_2017/schuller17_interspeech.html). INTERSPEECH 2017 | 2017 | Dataset paper | Checked |
