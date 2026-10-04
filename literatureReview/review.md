# Deep Learning and Machine Learning in Sleep Apnea Research: A Literature Review (2020–2025)

## 1. Introduction

Sleep apnea, particularly obstructive sleep apnea (OSA), is a highly prevalent chronic disorder characterized by recurrent episodes of complete or partial upper airway obstruction during sleep, leading to intermittent hypoxemia, sleep fragmentation, and sympathetic activation. The condition affects an estimated 936 million adults globally, with prevalence of moderate-to-severe OSA in the general adult population ranging from 6% to 17%. Beyond its cardinal symptoms of excessive daytime sleepiness and fatigue, untreated OSA is associated with cardiovascular disease, cognitive decline, and increased mortality risk.

The diagnostic gold standard—attended in-laboratory polysomnography (PSG)—remains costly, labor-intensive, and uncomfortable for patients. Manual scoring of PSG data is time-consuming, requiring expert technicians to visually identify and classify respiratory events across hundreds of 30-second epochs per night. These limitations have created a pressing need for automated, accessible, and accurate diagnostic alternatives. Machine learning (ML) and deep learning (DL) have emerged as promising solutions, leveraging the increasing availability of physiological signal data and computational advances to automate OSA detection, severity grading, and even screening from minimal sensor inputs.

This review synthesizes recent research (2020–2025) on ML/DL applications in sleep apnea, with particular emphasis on five key studies that exemplify current methodological trends. It examines the evolution of sensing modalities, model architectures, and clinical translation efforts, while identifying persistent challenges and future directions.

---

## 2. Automated Scoring and Severity Assessment

One of the most clinically impactful applications of DL in sleep medicine is the automation of PSG scoring, which has the potential to reduce technician workload, eliminate inter-scorer variability, and enable scalable diagnostic workflows.

### 2.1 Deep Learning for Automated PSG Scoring

Park et al. (2024) developed a deep learning algorithm to automatically score and grade OSA in adult polysomnography. Using 1,000 PSG cases split into training (700), validation (200), and test (100) sets, the authors constructed a sequential model comprising an initial perceptron layer, three consecutive LSTM layers, and two additional perceptron layers. The algorithm achieved high sensitivity (95% CI: 98.06–98.51) and specificity (95% CI: 95.46–97.79) across all OSA severities in detecting apnea/hypopnea events, with AUC values of 0.9402, 0.9388, and 0.9442 for predicting OSA at AHI thresholds of ≥5, ≥15, and ≥30, respectively. Notably, the model's performance was consistent across severity groups, suggesting robust generalizability. This study exemplifies how DL can be integrated into existing clinical workflows to enhance efficiency without sacrificing diagnostic accuracy.

### 2.2 Event-Level Classification and Clinical Severity Determination

Yook et al. (2024) took a complementary approach, focusing on accurate classification of apnea-hypopnea events and subsequent determination of clinical severity. Their study employed an Xception network trained on nasal respiration flow (RF), peripheral oxygen saturation (SpO2), and ECG signals obtained during PSG, incorporating demographic data for enhanced performance. Using RF and SpO2 feature sets, the model achieved 94% accuracy in detecting apnea/hypopnea events. For OSA screening, it attained 99% accuracy with an AUC of 0.99, while severity categorization yielded 93% accuracy and an AUC of 0.91, with no misclassification between normal/mild versus moderate/severe OSA. Importantly, the authors identified that classification errors predominantly arose in cases with hypopnea-prevalent participants—a clinically relevant limitation given the inherent difficulty of detecting hypopneas, which involve partial airflow reduction rather than complete cessation.

### 2.3 Comparative Observations

Both studies demonstrate that DL models can match or exceed human expert performance in respiratory event scoring. Park et al.'s LSTM-based sequential model and Yook et al.'s Xception network represent different architectural philosophies: the former emphasizes temporal sequence modeling, while the latter leverages depthwise separable convolutions for efficient feature extraction. The consistent finding across both studies is that DL can reliably automate tasks that currently consume significant clinical resources.

---

## 3. Novel Sensing Modalities and Radar-Based Detection

A significant trend in recent research is the exploration of non-contact and minimally invasive sensing modalities that could enable home-based OSA screening without the burden of traditional PSG equipment.

### 3.1 Radar-Based Apnea-Hypopnea Detection

Choi et al. (2024) developed a novel deep learning model for detecting apnea-hypopnea events using radar data, addressing the need for cost-effective and accessible alternatives to PSG. In a single-center prospective cohort study, participants with suspected sleep-disordered breathing were divided into development (n=54) and temporally independent test (n=35) sets. The authors employed a hybrid CNN-Transformer architecture, performing fivefold cross-validation on the development set. In the test set, the model achieved an event detection sensitivity of 67.2% (95% CI: 65.8–68.5%) and demonstrated a mean absolute error (MAE) of 7.54 for AHI estimation, with good agreement (ICC = 0.889) and strong correlation (r = 0.892) with ground truth. OSA severity estimation showed substantial agreement (κ = 0.780).

While the event detection sensitivity is lower than ECG-based approaches, this study represents a pioneering proof-of-concept for radar-based OSA diagnosis. The hybrid CNN-Transformer architecture is particularly noteworthy: CNNs excel at extracting local spatial features from radar signal spectrograms, while transformers capture long-range temporal dependencies across the night's recording. The non-contact nature of radar sensing could dramatically improve patient comfort and enable longitudinal monitoring in home environments.

### 3.2 Wearable and Sensor-Based Approaches

Zovko et al. (2025) introduced a machine learning-based framework aimed at detecting apnea events through analysis of polysomnographic and oximetry data, representing an effort to develop a practical data framework for sleep medicine applications. This work reflects the broader movement toward standardized, reusable data pipelines that can accommodate heterogeneous sensor inputs—a critical infrastructure need as the field moves toward multi-center validation and real-world deployment.

---

## 4. Multimodal Fusion and Advanced Architectures

The integration of multiple physiological signals and the adoption of increasingly sophisticated neural architectures represent two of the most active research directions in the field.

### 4.1 Multimodal Signal Fusion with Transformers

Zhang et al. (2025) developed a multimodal signal fusion multiscale Transformer model for OSA detection and severity assessment, using ECG and SpO2 signals—chosen for their medical reliability and acquisition simplicity. The model comprises signal preprocessing, feature extraction, cross-modal interaction, and classification modules, with a total of 510 patients who underwent PSG included in the hospital dataset.

The results were impressive: per-segment and per-recording detection accuracy reached 91.38% and 96.08%, respectively, in the hospital dataset. Severity assessment accuracy for mild, moderate, and severe OSA was 90.20%, 88.24%, and 92.16%, respectively. Bland-Altman plots confirmed consistency between true and predicted AHI. On public datasets (Apnea-ECG and UCD), per-segment detection accuracy was 95.04% and 90.56%, respectively.

The multiscale Transformer architecture is particularly well-suited to physiological signals, which contain meaningful information across multiple temporal scales—from sub-second cardiac dynamics to minute-scale respiratory patterns. The cross-modal interaction module enables the model to learn complementary representations from ECG and SpO2, potentially capturing both cardiac autonomic responses to apneic events and the resulting oxygen desaturation.

### 4.2 Hybrid Architectures: CNNs, LSTMs, and Transformers

The studies reviewed here illustrate a clear architectural evolution. Early DL approaches in sleep apnea relied primarily on CNNs or LSTMs in isolation. The current generation of models increasingly employs hybrid designs:

- **CNN-Transformer hybrids** (Choi et al.) combine local feature extraction with global temporal attention.
- **Xception networks** (Yook et al.) leverage depthwise separable convolutions for efficient feature learning.
- **Multiscale Transformers** (Zhang et al.) process signals at multiple temporal resolutions simultaneously.
- **LSTM-based sequential models** (Park et al.) remain effective for structured time-series data.

This architectural diversification reflects a maturation of the field: rather than seeking a single "best" model, researchers are now tailoring architectures to specific signal characteristics, data availability, and clinical requirements.

---

## 5. Systematic Reviews and Meta-Analyses: Establishing the Evidence Base

The proliferation of individual studies has been accompanied by systematic reviews and meta-analyses that synthesize evidence across the field.

### 5.1 ECG-Based Detection

Kilic et al. (2025) conducted a systematic review and meta-analysis of ML and DL algorithms for ECG-based sleep apnea detection, analyzing 84 studies through November 2023. The pooled sensitivity and specificity exceeded 90% in per-segment analysis and approached 97% in per-record analysis. However, the authors noted significant variations in algorithm effectiveness and methodological biases across studies, highlighting the need for standardized evaluation protocols.

### 5.2 EEG-Based Detection

Fathima et al. (2025) systematically reviewed EEG-based SA detection, screening 402 papers and selecting 63 for in-depth analysis. Their review underscored the potential of EEG-based methods while identifying key areas requiring further exploration, including signal decomposition techniques, feature selection methodologies, and cross-population generalizability.

### 5.3 Wearable AI and Non-Invasive Approaches

Osa-Sanchez et al. (2025) reviewed 249 studies published between 2020 and 2024 on wearable sensors and AI for sleep apnea detection, ultimately including 28 studies. They observed a trend toward integrating patches, clocks, and rings with convolutional neural networks, producing particularly promising results when combined with transfer learning. The review concluded that employing multiple combinations of different neural networks with convolutional layers contributes to more precise systems for early diagnosis.

Abd-Alrazaq et al. (2024) conducted a systematic review and meta-analysis of wearable AI for sleep apnea detection. Their subgroup analysis revealed that machine learning algorithms achieved a pooled mean accuracy of 0.896 (95% CI: 0.87–0.92), while deep learning algorithms achieved 0.849 (95% CI: 0.76–0.92). Notably, studies with sample sizes exceeding 100 participants achieved higher pooled accuracy (0.905) compared to smaller studies (0.838), suggesting that data quantity remains a critical factor.

### 5.4 Earlier Meta-Analyses

Tyagi and Agarwal (2023) conducted a systematic review and meta-analysis of DL applied to physiological data including pulse oxygen saturation, ECG, airflow, and sound signals, reviewing 47 studies from 2012–2022. Their work categorized research by signal type and DL architecture, providing a foundational taxonomy for the field.

---

## 6. Methodological Trends and Clinical Translation

### 6.1 Data Sources and Signal Modalities

The research landscape reveals a clear hierarchy of signal preference:

| Signal Type | Advantages | Limitations | Representative Studies |
|---|---|---|---|
| **ECG** | Widely available, strong autonomic correlates | Requires contact sensors | Kilic et al. (2025), Zhang et al. (2025) |
| **SpO2** | Simple acquisition, direct measure of desaturation | Lag in response, motion artifacts | Yook et al. (2024), Zhang et al. (2025) |
| **EEG** | Rich sleep stage information | Requires expertise, uncomfortable | Fathima et al. (2025) |
| **Radar** | Non-contact, privacy-preserving | Lower sensitivity, emerging technology | Choi et al. (2024) |
| **Wearable sensors** | Ambulatory, longitudinal monitoring | Variable data quality | Osa-Sanchez et al. (2025), Abd-Alrazaq et al. (2024) |

### 6.2 Model Performance Benchmarks

Across studies, DL models consistently achieve high performance metrics:

- **Per-record detection**: 90–97% sensitivity/specificity (ECG-based)
- **Per-segment detection**: >90% accuracy (multimodal)
- **Event-level detection**: 94% accuracy (RF + SpO2)
- **Severity classification**: 88–93% accuracy
- **Radar-based detection**: 67.2% sensitivity (emerging technology)

### 6.3 Clinical Translation Challenges

Despite impressive technical performance, several barriers to clinical adoption persist:

**Interpretability**: Many DL models operate as "black boxes," making it difficult for clinicians to understand the basis for predictions. This is particularly problematic in medical applications where accountability and explainability are essential.

**Generalizability**: Most studies are single-center with relatively small sample sizes. The multi-center study by Park et al. (2024) is a notable exception, but broader validation across diverse populations, equipment, and clinical settings remains limited.

**Demographic bias**: Systematic reviews have highlighted demographic gaps in study cohorts, with underrepresentation of certain racial, ethnic, and socioeconomic groups.

**Regulatory and workflow integration**: Automated scoring systems must undergo regulatory approval and integrate seamlessly with existing clinical workflows—a process that is both time-consuming and resource-intensive.

---

## 7. Challenges and Future Directions

### 7.1 Technical Challenges

- **Hypopnea detection**: As noted by Yook et al., hypopnea-predominant cases remain the most challenging for automated systems, with classification errors predominantly arising in these scenarios. Improving hypopnea detection requires more sophisticated modeling of partial airflow reduction and its physiological correlates.
- **Inter-subject variability**: Physiological signals vary substantially across individuals due to age, sex, body composition, and comorbidities. Domain adaptation and transfer learning techniques are promising but remain under-explored in sleep apnea research.
- **Data scarcity**: Annotated PSG data is expensive to obtain. Self-supervised learning and data augmentation strategies could help address this limitation.

### 7.2 Clinical and Translational Priorities

- **Prospective validation**: Most studies are retrospective. Prospective, blinded validation against expert-scored PSG is needed before clinical deployment.
- **Home-based screening**: Radar, wearable, and smartphone-based approaches hold promise for scalable screening, but require validation in real-world home environments.
- **Integration with treatment pathways**: DL models should not only detect OSA but also inform treatment selection (e.g., CPAP titration, oral appliance therapy, or surgical intervention).
- **Patient-centered outcomes**: Beyond AHI correlation, future studies should evaluate whether DL-guided diagnosis improves patient-reported outcomes, treatment adherence, and long-term health outcomes.

### 7.3 Emerging Research Directions

- **Foundation models**: Large-scale pre-training on diverse physiological signals could yield generalizable representations that transfer across tasks and populations.
- **Explainable AI**: Attention visualization, saliency mapping, and other interpretability techniques are increasingly being applied to sleep apnea models, helping clinicians understand model decisions.
- **Edge computing**: Deploying DL models on wearable devices and smartphones enables real-time monitoring without cloud dependency, raising new challenges in model compression and energy efficiency.
- **Multi-omics integration**: Combining physiological signals with genomic, metabolomic, and clinical data could enable more precise phenotyping of OSA subtypes.

---

## 8. Conclusion

The past five years have witnessed remarkable progress in applying ML and DL to sleep apnea research. From automated PSG scoring to radar-based non-contact detection and multimodal Transformer models, the field has expanded both in methodological sophistication and clinical relevance. The five studies highlighted in this review exemplify key trends: the maturation of hybrid architectures (CNN-Transformer, Xception, multiscale Transformers), the exploration of novel sensing modalities (radar, wearables), and the growing emphasis on clinical translation and validation.

However, significant challenges remain. Hypopnea detection, inter-subject variability, demographic bias, and the gap between retrospective performance and prospective clinical utility must be addressed before these technologies can realize their full potential. Systematic reviews and meta-analyses consistently show high pooled accuracy but also highlight methodological heterogeneity and the need for standardized evaluation frameworks.

The future of the field lies in prospective validation studies, explainable and generalizable models, integration with clinical workflows, and ultimately, demonstration that AI-guided diagnosis improves patient outcomes. As the research community moves toward these goals, the integration of ML/DL into sleep medicine promises to transform a field historically constrained by resource-intensive diagnostics into one capable of scalable, accessible, and precise care.

---

## References

1. Choi, J. W., Koo, D. L., Kim, D. H., Nam, H., Lee, J. H., Hong, S.-N., & Kim, B. (2024). A novel deep learning model for obstructive sleep apnea diagnosis: hybrid CNN-Transformer approach for radar-based detection of apnea-hypopnea events. *Sleep*, 47(12), zsae184.

2. Park, M. J., Choi, J. H., Kim, S. Y., & Ha, T. K. (2024). A deep learning algorithm model to automatically score and grade obstructive sleep apnea in adult polysomnography. *DIGITAL HEALTH*, 10.

3. Yook, S., Kim, D., Gupte, C., Joo, E. Y., & Kim, H. (2024). Deep learning of sleep apnea-hypopnea events for accurate classification of obstructive sleep apnea and determination of clinical severity. *Sleep Medicine*, 114, 211–219.

4. Zhang, Y., Zhou, L., Zhu, S., et al. (2025). Deep Learning for Obstructive Sleep Apnea Detection and Severity Assessment: A Multimodal Signals Fusion Multiscale Transformer Model. *Nature and Science of Sleep*, 17, 1–15.

5. Zovko, K., Sadowski, Y., Perković, T., Šolić, P., Pavlinac Dodig, I., Pecotić, R., & Đogaš, Z. (2025). Advanced Data Framework for Sleep Medicine Applications: Machine Learning-Based Detection of Sleep Apnea Events. *Applied Sciences*, 15(1), 376.

6. Kilic, M. E., Arayici, M. E., Turan, O. E., Yilancioglu, Y. R., Ozcan, E. E., & Yilmaz, M. B. (2025). Diagnostic accuracy of machine learning algorithms in electrocardiogram-based sleep apnea detection: A systematic review and meta-analysis. *Sleep Medicine Reviews*, 81, 102097.

7. Osa-Sanchez, A., et al. (2025). Wearable Sensors and Artificial Intelligence for Sleep Apnea Detection: A Systematic Review. *Journal of Medical Systems*, 49(1), 66.

8. Fathima, S., et al. (2025). Sleep Apnea Detection Using EEG: A Systematic Review of Datasets, Methods, Challenges, and Future Directions. *Annals of Biomedical Engineering*, 53(5), 1043–1067.

9. Abd-Alrazaq, A., Aslam, H., AlSaad, R., Alsahli, M., Ahmed, A., Damseh, R., Aziz, S., & Sheikh, J. (2024). Detection of Sleep Apnea Using Wearable AI: Systematic Review and Meta-Analysis. *Journal of Medical Internet Research*, 26, e58187.

10. Tyagi, P. K., & Agarwal, D. (2023). Systematic review of automated sleep apnea detection based on physiological signal data using deep learning algorithm: a meta-analysis approach. *Biomedical Engineering Letters*, 13(3), 293–312.
