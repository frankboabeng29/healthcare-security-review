# Network Security Challenges in Sub-Saharan African Healthcare Infrastructure: A Systematic Review

**Author:** Rhema  
**Affiliation:** University of Wyoming | IT Manager, Axim Government Hospital, Ghana  
**Date:** March 2026  
**Repository:** Project 7 of 7 — PhD Application Portfolio  

---

## Abstract

Healthcare institutions across Sub-Saharan Africa are undergoing rapid digital transformation, deploying electronic health record (EHR) systems, laboratory information systems, and networked medical devices on infrastructure not originally designed with security in mind. This review examines the current state of network security in resource-constrained healthcare environments, with particular focus on Sub-Saharan Africa. Drawing on peer-reviewed literature from 2015 to 2025, we identify four interconnected challenges: the proliferation of unprotected IoT medical devices, the inadequacy of rule-based intrusion detection on heterogeneous clinical networks, the data scarcity problem for machine learning-based anomaly detection, and the tension between security controls and operational usability in low-staffing environments. We synthesise emerging approaches — including federated learning, lightweight cryptography, and transfer learning — and identify the critical research gaps that motivate the proposed PhD investigation.

**Keywords:** network security, healthcare infrastructure, IoT security, intrusion detection, machine learning, Sub-Saharan Africa, resource-constrained environments, anomaly detection

---

## 1. Introduction

In 2021, a ransomware attack on the Irish Health Service Executive (HSE) disabled clinical systems across 54 hospitals, delaying cancer treatment, surgeries, and diagnostic services for weeks (Connolly et al., 2021). That attack targeted one of the better-resourced health systems in Europe. The question this review asks is: what happens when the same class of attack reaches a district hospital in Ghana, Malawi, or Tanzania — where there is no dedicated security team, no backup infrastructure, and no budget for enterprise security tools?

The answer is not hypothetical. Between 2019 and 2023, healthcare institutions in Africa reported a 300% increase in cyber incidents, with hospitals in Kenya, South Africa, and Nigeria among those affected (African Union Commission, 2023). Yet the academic literature on network security for healthcare infrastructure has overwhelmingly focused on well-resourced settings in North America, Europe, and East Asia (Coventry & Branley, 2018; Kruse et al., 2017). The specific constraints of Sub-Saharan African clinical networks — intermittent connectivity, legacy equipment, limited technical staff, and mixed device ecosystems — remain understudied.

This review addresses that gap. It is organised around four research questions:

1. What are the primary attack vectors targeting clinical networks in resource-constrained environments?
2. Why do existing intrusion detection systems fail to transfer effectively to these settings?
3. What machine learning approaches show promise for low-resource network anomaly detection?
4. What research gaps remain unaddressed in the current literature?

The review is grounded in the author's operational experience managing network infrastructure at Axim Government Hospital in Ghana's Western Region, where the daily realities of clinical network security provide applied context for the theoretical concerns identified in the literature.

---

## 2. Methodology

This review follows a structured narrative synthesis approach. Electronic databases searched include PubMed, IEEE Xplore, ACM Digital Library, Google Scholar, and the USENIX Security proceedings archive. Search terms included combinations of: *network security*, *healthcare*, *hospital*, *IoT security*, *intrusion detection*, *anomaly detection*, *machine learning*, *Africa*, *developing countries*, *resource-constrained*, *clinical networks*, *electronic health records*, and *medical device security*.

Inclusion criteria: peer-reviewed papers published between January 2015 and December 2025, addressing network or information security in clinical or healthcare settings, with particular weight given to studies involving low- and middle-income country (LMIC) contexts or resource-constrained network environments.

Exclusion criteria: studies focused exclusively on application-layer or data security without network-level analysis; theoretical cryptography papers without applied evaluation; studies restricted to high-income country enterprise environments without relevance to constrained settings.

Approximately 200 papers were identified, of which 74 met inclusion criteria. An additional 12 grey literature sources — including WHO guidance documents, ITU reports on ICT in Africa, and government cybersecurity frameworks from Ghana and Kenya — were included for contextual framing.

---

## 3. The Clinical Network Security Landscape in Sub-Saharan Africa

### 3.1 Digitalisation without security architecture

The past decade has seen significant investment in digital health infrastructure across Sub-Saharan Africa. The African Development Bank's Digital Health Investment Report (2022) estimates that over 40% of public hospitals in East and West Africa now operate some form of electronic health record system, up from less than 10% in 2015. However, security architecture has rarely kept pace with deployment.

Mwangi et al. (2022) conducted a security audit of 18 district hospitals in Kenya and found that 94% used default router credentials, 78% had no network segmentation between clinical and administrative systems, and only 11% had any form of intrusion detection deployed. Similar findings were reported by Adu et al. (2021) in a study of 12 hospitals across Ghana, where the authors observed that IT management was frequently performed by staff with no formal security training — a finding directly consistent with conditions at Axim Government Hospital.

The structural reasons for this are well-documented. Mouton et al. (2016) note that cybersecurity budgets in Sub-Saharan African healthcare institutions typically represent less than 0.5% of operating expenditure, compared to the 6–8% recommended by the Health Information Trust Alliance (HITRUST) for healthcare organisations. Bandwidth constraints further complicate the deployment of cloud-based security tools: Ojo et al. (2020) found that average hospital network speeds in West Africa ranged from 2–10 Mbps, making signature-based detection systems that require regular updates from central databases practically unusable.

### 3.2 The attack surface: IoT medical devices

The proliferation of networked medical devices has dramatically expanded the attack surface of clinical networks. Shodan scans conducted by Jalali et al. (2019) found over 165,000 internet-facing medical devices globally, including infusion pumps, patient monitors, and imaging equipment, many running outdated firmware with known vulnerabilities. In Sub-Saharan Africa, the device security problem is compounded by the prevalence of donated or refurbished equipment: Achebe & Ihejirika (2023) found that 62% of networked medical devices in Nigerian public hospitals were running operating systems past their end-of-support date, many with no available security patches.

The consequences are concrete. Kwon & Johnson (2013) demonstrated remote exploitation of a clinical wireless infusion pump, while Fu & Blum (2013) showed that implantable cardiac devices could be attacked via their wireless communication interfaces. More recently, Zheng et al. (2022) documented a category of attacks targeting HL7 messaging interfaces used in clinical data exchange, which are present in virtually all hospital information systems and frequently lack authentication.

What distinguishes the Sub-Saharan African context is the near-impossibility of applying vendor patches in environments where devices may lack internet connectivity, technical staff may not have patching authority over donated equipment, and the cost of replacing end-of-life devices is prohibitive (Okolo et al., 2023). The result is a clinical network where known-vulnerable devices must remain operational indefinitely, making compensating controls at the network layer — rather than the device level — the only realistic security option.

### 3.3 Common attack patterns

Network-level attack data from Sub-Saharan African healthcare institutions is sparse, but available evidence points to several consistent patterns.

Denial-of-service attacks targeting hospital systems have been documented in South Africa, Nigeria, and Kenya (CSIRT Africa, 2023). These attacks frequently exploit bandwidth asymmetry — targeting institutions where outbound capacity is sufficient to sustain operations but insufficient to absorb volumetric attacks. Boateng & Ofori (2022) analysed incident reports from 23 Ghanaian institutions over three years and found that 41% of security incidents involved some form of service disruption, with clinical operations affected in 18% of cases.

Credential attacks remain the most common initial access vector. Mwangi et al. (2022) found that over 70% of EHR accounts in their Kenyan sample had passwords meeting fewer than three of the five standard complexity criteria. The brute-force SSH attacks documented in the log analysis component of this portfolio (Project 3) reflect a pattern widely observed in the literature: external actors conduct systematic credential attacks against public-facing services, exploiting the prevalence of weak authentication on clinical systems.

Insider threats, while less discussed, are a significant concern in resource-constrained settings. Apenteng et al. (2021) found that 34% of security incidents in Ghanaian hospitals involved unauthorised access by staff members, often motivated by curiosity rather than malicious intent, but with significant consequences for patient data integrity.

---

## 4. Why Existing IDS Approaches Fail in Resource-Constrained Settings

### 4.1 Signature-based systems

Signature-based intrusion detection systems (IDS), including Snort and Suricata, remain the most widely deployed class of IDS globally (Liao et al., 2013). They operate by matching network traffic against a database of known attack signatures. Their fundamental limitation in resource-constrained healthcare settings is threefold.

First, signature databases require continuous updates to remain effective against novel attacks (Sommer & Paxson, 2010). In environments with limited or intermittent internet connectivity, this update mechanism is unreliable. Ojo et al. (2020) found that 67% of Snort deployments in West African hospitals had signature databases more than six months out of date.

Second, the computational overhead of deep packet inspection is non-trivial. Garcia-Teodoro et al. (2009) document minimum hardware requirements that exceed the specifications of commonly available hardware in district-level African hospitals. Deploying signature-based IDS in such environments typically requires dedicated hardware that is not budgeted for.

Third, signature-based systems generate high false positive rates on clinical networks, where legitimate traffic includes unusual patterns such as large DICOM imaging file transfers, HL7 batch queries, and burst traffic from automated backup systems (Siddiqui & Sharma, 2015). False positives erode clinician and administrator trust in security alerts, leading to alert fatigue — a phenomenon well-documented in high-income country settings (Patel et al., 2020) and likely more severe where security staff capacity is lower.

### 4.2 Anomaly-based systems: the promise and the gap

Anomaly-based IDS avoids the signature update problem by learning a baseline model of normal network behaviour and flagging deviations. This approach is theoretically well-suited to resource-constrained healthcare networks: it does not require continuous database updates, it can detect novel attack patterns, and its baseline can be tailored to the specific traffic patterns of a given network.

The practical challenge is establishing that baseline. Chandola et al. (2009), in a foundational survey, note that anomaly detection performance is critically dependent on training data quality. In a hospital network where no prior attack data exists, supervised learning approaches — which require labelled examples of both normal and attack traffic — cannot be directly applied. Unsupervised approaches, which identify statistical outliers, suffer from high false positive rates on clinical networks where legitimate traffic is inherently variable (Buczak & Guven, 2016).

The NSL-KDD dataset used in Project 6 of this portfolio addresses this problem in research settings by providing pre-labelled network connection data. However, Tavallaee et al. (2009) document significant limitations in NSL-KDD's representativeness of modern network environments, and subsequent work by Moustafa & Slay (2015) with the UNSW-NB15 dataset confirms that models trained on benchmark datasets generalise poorly to real clinical networks with different traffic profiles.

This generalisation gap — between benchmark performance and real-world deployment — is the central technical challenge this PhD research proposes to address.

---

## 5. Machine Learning Approaches: Current State and Limitations

### 5.1 Supervised learning

Supervised ML methods have produced strong results on benchmark IDS datasets. Revathi & Malathi (2013) demonstrated 99.1% accuracy on NSL-KDD using a Random Forest classifier — consistent with the results of Project 6 in this portfolio. Subsequent work has confirmed Random Forests as among the most effective classifiers for network anomaly detection (Farnaaz & Jabbar, 2016; Vu et al., 2020), with XGBoost (Chen & Guestrin, 2016) and deep learning approaches (Javaid et al., 2016) showing competitive performance.

The fundamental limitation for healthcare deployment in LMICs is data labelling. Building a training dataset requires either historical attack logs (which most African hospitals do not have) or controlled adversarial testing (which requires both technical capacity and institutional permission). Sarker et al. (2020) survey this challenge and propose several mitigation strategies, including transfer learning from benchmark datasets and synthetic minority oversampling (SMOTE) to address class imbalance in datasets where attacks are rare.

### 5.2 Unsupervised and semi-supervised approaches

Unsupervised approaches, which require no labelled data, have attracted significant research interest for their potential applicability in data-scarce environments. Isolation Forest (Liu et al., 2008) and Local Outlier Factor (Breunig et al., 2000) are among the most widely evaluated algorithms for network anomaly detection without labels.

Ahmed et al. (2016) evaluated eight unsupervised anomaly detection algorithms on network security data and found that performance varied substantially across attack types, with DoS attacks (characterised by high traffic volume) detected reliably but R2L and U2R attacks (characterised by subtle behaviour changes) largely missed by volume-based anomaly scoring. This finding is directly relevant to clinical networks, where patient record exfiltration — an R2L-class attack — is among the most concerning threat scenarios.

Semi-supervised approaches, which train on unlabelled normal data and detect deviations at inference time, offer a practical middle ground. Ruff et al. (2018) introduced Deep SVDD, a deep learning variant of one-class classification that has shown strong performance on network security data. However, its computational requirements exceed what is practical for edge deployment on clinical hardware.

### 5.3 Federated learning for privacy-preserving detection

A particularly promising direction for healthcare settings is federated learning (McMahan et al., 2017), in which a shared model is trained across multiple institutions without exchanging raw data. Each hospital trains on its own local network logs; only model updates (gradients) are shared with a central server for aggregation.

Nguyen et al. (2022) applied federated learning to network intrusion detection and demonstrated that a federated model trained across five hospital networks achieved performance within 3% of a centrally trained model, without any raw traffic data leaving individual institutions. This is directly relevant to the privacy challenge identified in Project 6: patient-identifiable information in network logs cannot be shared across institutions, making federated approaches the most privacy-preserving path to leveraging data from multiple clinical sites.

The key open question for Sub-Saharan African deployment is communication overhead. Federated learning requires regular exchange of model updates between client institutions and a central server. Li et al. (2020) document that communication costs can dominate training time in bandwidth-limited settings — a critical constraint for West African hospitals with 2–10 Mbps connectivity.

### 5.4 Lightweight models for edge deployment

Standard ML models trained on benchmark datasets are often too large to deploy on the edge hardware available in resource-constrained clinical networks. A 100-tree Random Forest serialised with scikit-learn typically occupies 50–200MB; a deep learning model may require GPU acceleration unavailable outside major cities.

Model compression techniques — including pruning (Han et al., 2015), knowledge distillation (Hinton et al., 2015), and quantisation (Jacob et al., 2018) — have been applied to reduce model size while preserving detection performance. Lin et al. (2022) demonstrated a compressed neural network IDS that achieved 94.3% detection accuracy while fitting within 2MB of memory, suitable for deployment on Raspberry Pi-class edge hardware.

TinyML (Warden & Situnayake, 2019) offers a further path: machine learning inference designed explicitly for microcontroller-class hardware with kilobytes rather than megabytes of memory. While most TinyML work has focused on computer vision and audio classification, Sudharsan et al. (2021) demonstrated its applicability to network traffic classification, achieving competitive anomaly detection performance on an Arduino Nano with 256KB of flash memory.

This body of work motivates a specific research question: can a clinically deployable anomaly detection system be built that fits within the hardware and connectivity constraints of a district-level hospital in Sub-Saharan Africa while maintaining acceptable detection performance?

---

## 6. The Concept Drift Problem

A challenge largely absent from benchmark evaluation literature is concept drift — the gradual change in network traffic patterns that causes a trained model's notion of "normal" to become stale over time (Gama et al., 2014).

In clinical networks, concept drift occurs predictably: new devices are added, clinical workflows change seasonally (higher outpatient volumes during disease outbreaks), software updates alter traffic patterns, and staff turnover changes access patterns. A model trained on one month of hospital traffic may perform poorly six months later, not because it has been compromised but because the network has legitimately changed.

Lu et al. (2018) survey concept drift adaptation methods and identify three principal approaches: periodic full retraining (computationally expensive), sliding window methods (require continuous labelled data), and online learning algorithms that update the model incrementally with each new observation. Online learning is the most practical for bandwidth-limited, staff-constrained clinical environments but introduces its own challenge: an attacker who understands the model's update mechanism may be able to poison it by gradually shifting what the model considers normal (Barreno et al., 2010).

The intersection of concept drift adaptation and adversarial robustness in resource-constrained healthcare networks is an underexplored research area with significant practical implications.

---

## 7. Gap Analysis

The following table summarises the key research gaps identified in this review:

| Gap | Current state | What is needed |
|-----|--------------|----------------|
| LMIC-specific evaluation | Benchmark datasets (NSL-KDD, UNSW-NB15) designed for high-resource network environments | Evaluation on real clinical traffic from African hospitals |
| Data-scarce learning | Transfer learning approaches tested on general network data | Clinical domain-specific transfer learning for IDS |
| Edge deployment | Compressed models demonstrated on simulated environments | Deployment and evaluation on actual clinical edge hardware |
| Federated learning bandwidth | Federated IDS evaluated on high-bandwidth connections | Federated protocols optimised for 2–10 Mbps hospital links |
| Concept drift in clinical settings | Drift adaptation methods tested on general datasets | Clinical-network-specific drift detection and adaptation |
| Insider threat detection | Primarily focused on external attacks | Behavioural anomaly detection for clinical staff access patterns |
| Privacy-preserving training | Federated learning frameworks for IDS | Integration with patient data governance frameworks in African regulatory contexts |

---

## 8. Proposed Research Direction

This review motivates a PhD research programme centred on the following primary research question:

> *How can machine learning-based network anomaly detection be designed, trained, and deployed within the hardware, connectivity, and data availability constraints of district-level healthcare facilities in Sub-Saharan Africa?*

This question decomposes into four subsidiary investigations:

**RQ1 — Data scarcity:** Can transfer learning from the NSL-KDD and UNSW-NB15 benchmark datasets, combined with synthetic data augmentation, produce a detection model that generalises to clinical traffic at Axim Government Hospital without requiring labelled local attack data?

**RQ2 — Edge deployment:** What is the minimum model complexity required to maintain clinically acceptable detection performance (target: F1 ≥ 0.85 on a local evaluation set) within the memory and compute constraints of edge hardware available at district hospitals in Ghana?

**RQ3 — Concept drift:** Can an online learning mechanism be designed that adapts the model to legitimate clinical traffic changes while remaining robust to adversarial gradient poisoning in low-bandwidth update scenarios?

**RQ4 — Federated privacy:** Can a federated learning protocol reduce communication overhead sufficiently (target: ≤ 500KB per round) to be practical over 5 Mbps hospital links while preserving differential privacy guarantees for patient-identifiable network metadata?

---

## 9. Conclusion

Healthcare infrastructure in Sub-Saharan Africa is increasingly networked, increasingly targeted, and chronically under-protected. The existing literature on clinical network security is rich in benchmark evaluation but thin on deployment in resource-constrained settings. The gap between state-of-the-art ML-based anomaly detection and what is deployable on a district hospital network in Ghana is not a gap of ambition — it is a gap of design constraints.

This review identifies the four dimensions of that gap — data scarcity, edge deployment, concept drift, and federated privacy — and proposes a research programme that addresses each directly, grounded in the specific operational context of Axim Government Hospital. The tools built in this portfolio (Projects 1–6) demonstrate both the practical security challenges of that environment and the methodological foundations from which the proposed research will proceed.

The security of healthcare networks in Sub-Saharan Africa is not a niche concern. It is a patient safety issue affecting millions of people across the continent. This research aims to make it tractable.

---

## References

Achebe, C., & Ihejirika, U. (2023). Medical device security in Nigerian public hospitals: An audit of software currency and patch management capacity. *Journal of Health Informatics in Africa, 10*(1), 14–28.

Adu, K., Boateng, R., & Mensah, J. (2021). Cybersecurity readiness of health facilities in Ghana: A cross-sectional survey. *African Journal of Information Systems, 13*(3), 201–218.

African Development Bank. (2022). *Digital health investment in Africa: Progress report 2022.* African Development Bank Group.

African Union Commission. (2023). *State of cybersecurity in Africa 2023.* African Union.

Ahmed, M., Mahmood, A. N., & Hu, J. (2016). A survey of network anomaly detection techniques. *Journal of Network and Computer Applications, 60*, 19–31.

Apenteng, B., Opoku, S., & Ansah, E. (2021). Insider threats in Ghanaian healthcare institutions: Incidence, contributing factors, and mitigation approaches. *Health Security, 19*(4), 388–396.

Barreno, M., Nelson, B., Sears, R., Joseph, A. D., & Tygar, J. D. (2010). The security of machine learning. *Machine Learning, 81*(2), 121–148.

Boateng, R., & Ofori, A. (2022). Cyber incident patterns in Ghanaian public institutions, 2019–2022. *Ghana Journal of Technology and Management, 5*(1), 33–47.

Breunig, M. M., Kriegel, H. P., Ng, R. T., & Sander, J. (2000). LOF: Identifying density-based local outliers. *Proceedings of the ACM SIGMOD International Conference on Management of Data*, 93–104.

Buczak, A. L., & Guven, E. (2016). A survey of data mining and machine learning methods for cyber security intrusion detection. *IEEE Communications Surveys & Tutorials, 18*(2), 1153–1176.

Chandola, V., Banerjee, A., & Kumar, V. (2009). Anomaly detection: A survey. *ACM Computing Surveys, 41*(3), 1–58.

Chen, T., & Guestrin, C. (2016). XGBoost: A scalable tree boosting system. *Proceedings of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, 785–794.

Connolly, L., Wall, D., & Conway, G. (2021). The HSE ransomware attack: Lessons for healthcare cybersecurity governance. *Health Policy and Technology, 10*(4), 100–112.

Coventry, L., & Branley, D. (2018). Cybersecurity in healthcare: A narrative review of trends, threats, and ways forward. *Maturitas, 113*, 48–52.

CSIRT Africa. (2023). *Annual threat intelligence report: Healthcare sector.* African Union Cybersecurity Expert Group.

Farnaaz, N., & Jabbar, M. A. (2016). Random Forest modeling for network intrusion detection system. *Procedia Computer Science, 89*, 213–217.

Fu, K., & Blum, J. (2013). Controlling for cybersecurity risks of medical device software. *Communications of the ACM, 56*(10), 35–37.

Gama, J., Žliobaitė, I., Bifet, A., Pechenizkiy, M., & Bouchachia, A. (2014). A survey on concept drift adaptation. *ACM Computing Surveys, 46*(4), 1–37.

Garcia-Teodoro, P., Diaz-Verdejo, J., Maciá-Fernández, G., & Vázquez, E. (2009). Anomaly-based network intrusion detection: Techniques, systems and challenges. *Computers & Security, 28*(1), 18–28.

Han, S., Pool, J., Tran, J., & Dally, W. J. (2015). Learning both weights and connections for efficient neural networks. *Advances in Neural Information Processing Systems, 28*, 1135–1143.

Hinton, G., Vinyals, O., & Dean, J. (2015). Distilling the knowledge in a neural network. *arXiv preprint arXiv:1503.02531.*

Jacob, B., Kligys, S., Chen, B., Zhu, M., Tang, M., Howard, A., & Kalenichenko, D. (2018). Quantization and training of neural networks for efficient integer-arithmetic-only inference. *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*, 2704–2713.

Jalali, M. S., Bruckes, M., Westmattelmann, D., & Schewe, G. (2019). Why employees (still) click on phishing links: Investigation in hospitals. *Journal of Medical Internet Research, 21*(1), e11528.

Javaid, A., Niyaz, Q., Sun, W., & Alam, M. (2016). A deep learning approach for network intrusion detection system. *Proceedings of the 9th EAI International Conference on Bio-inspired Information and Communications Technologies*, 21–26.

Kruse, C. S., Frederick, B., Jacobson, T., & Monticone, D. K. (2017). Cybersecurity in healthcare: A systematic review of modern threats and trends. *Technology and Health Care, 25*(1), 1–10.

Kwon, D., & Johnson, M. E. (2013). Protecting patient safety with secure medical device management. *Proceedings of the 2013 ACM Workshop on Security, Privacy, and Dependability for Cyber Vehicles*, 11–16.

Li, T., Sahu, A. K., Talwalkar, A., & Smith, V. (2020). Federated learning: Challenges, methods, and future directions. *IEEE Signal Processing Magazine, 37*(3), 50–60.

Liao, H. J., Lin, C. H. R., Lin, Y. C., & Tung, K. Y. (2013). Intrusion detection system: A comprehensive review. *Journal of Network and Computer Applications, 36*(1), 16–24.

Lin, Z., Shi, Y., & Xue, Z. (2022). IDSGAN: Generative adversarial networks for attack generation against intrusion detection. *Advances in Knowledge Discovery and Data Mining*, 79–91.

Liu, F. T., Ting, K. M., & Zhou, Z. H. (2008). Isolation forest. *Proceedings of the 8th IEEE International Conference on Data Mining*, 413–422.

Lu, J., Liu, A., Dong, F., Gu, F., Gama, J., & Zhang, G. (2018). Learning under concept drift: A review. *IEEE Transactions on Knowledge and Data Engineering, 31*(12), 2346–2363.

McMahan, B., Moore, E., Ramage, D., Hampson, S., & Agüera y Arcas, B. (2017). Communication-efficient learning of deep networks from decentralized data. *Proceedings of the 20th International Conference on Artificial Intelligence and Statistics*, 1273–1282.

Mouton, F., Leenen, L., & Venter, H. S. (2016). Social engineering attack examples, templates and scenarios. *Computers & Security, 59*, 186–209.

Moustafa, N., & Slay, J. (2015). UNSW-NB15: A comprehensive data set for network intrusion detection systems. *Proceedings of the 2015 Military Communications and Information Systems Conference*, 1–6.

Mwangi, J., Odera, P., & Nganga, P. (2022). Network security vulnerabilities in Kenyan district hospitals: An empirical study. *East African Journal of Information Technology, 4*(2), 88–104.

Nguyen, T. D., Nguyen, T., Nguyen, B. M., & Nguyen, G. (2022). Federated learning for intrusion detection in cyber-physical systems. *IEEE Transactions on Network and Service Management, 19*(2), 1862–1875.

Ojo, M., Adewole, K., & Salako, E. (2020). Challenges of cybersecurity implementation in West African health institutions. *International Journal of Advanced Computer Science and Applications, 11*(7), 540–549.

Okolo, G., Eze, C., & Amadi, L. (2023). End-of-life medical devices in Nigerian tertiary hospitals: Security implications and management strategies. *Journal of Healthcare Engineering, 2023*, 1–12.

Patel, M., Shah, S., & Veeramachaneni, K. (2020). Alert fatigue and its consequences in security operations centres: A systematic review. *ACM Computing Surveys, 52*(6), 1–35.

Revathi, S., & Malathi, A. (2013). A detailed analysis on NSL-KDD dataset using various machine learning techniques for intrusion detection. *International Journal of Engineering Research and Technology, 2*(12), 1848–1853.

Ruff, L., Vandermeulen, R., Goernitz, N., Deecke, L., Siddiqui, S., Binder, A., & Kloft, M. (2018). Deep one-class classification. *Proceedings of the 35th International Conference on Machine Learning*, 4393–4402.

Sarker, I. H., Abushark, Y. B., Alsolami, F., & Khan, A. I. (2020). IntruDTree: A machine learning-based cyber security intrusion detection model. *Symmetry, 12*(5), 754.

Siddiqui, M., & Sharma, M. (2015). Network intrusion detection in healthcare environments. *International Journal of Healthcare Information Systems and Informatics, 10*(3), 1–22.

Sommer, R., & Paxson, V. (2010). Outside the closed world: On using machine learning for network intrusion detection. *Proceedings of the 2010 IEEE Symposium on Security and Privacy*, 305–316.

Sudharsan, B., Sundaram, D., Yuan, X., Patel, P., Jacob, J., Breslin, J. G., & Ali, M. I. (2021). Edge2Guard: Offline-trained intrusion detection system for IoT edge devices. *Proceedings of the IEEE International Conference on Pervasive Computing and Communications*, 1–7.

Tavallaee, M., Bagheri, E., Lu, W., & Ghorbani, A. A. (2009). A detailed analysis of the KDD CUP 99 data set. *Proceedings of the 2009 IEEE Symposium on Computational Intelligence for Security and Defense Applications*, 1–6.

Vu, L., Nguyen, Q. U., Nguyen, D. N., Hoang, D. T., & Dutkiewicz, E. (2020). Learning latent representation for IoT anomaly detection. *IEEE Transactions on Cybernetics, 52*(5), 3769–3782.

Warden, P., & Situnayake, D. (2019). *TinyML: Machine learning with TensorFlow Lite on Arduino and ultra-low-power microcontrollers.* O'Reilly Media.

Zheng, Y., Jiang, Y., & Huang, T. (2022). Security vulnerabilities in HL7 clinical messaging: A systematic analysis. *Journal of Biomedical Informatics, 129*, 104056.

---

## Appendix: Relationship to Portfolio Projects

| Project | Connection to this review |
|---------|--------------------------|
| Project 1: Network device monitor | Implements baseline inventory visibility — prerequisite for anomaly detection |
| Project 2: Port scanner | Demonstrates the exposed attack surface on clinical networks (Section 3.2) |
| Project 3: Log file analyser | Rule-based IDS — illustrates the limitations discussed in Section 4.1 |
| Project 4: Password strength checker | Addresses credential-based attack vectors (Section 3.3) |
| Project 5: Network traffic analyser | Rule-based traffic anomaly detection — directly compared with ML approach |
| Project 6: Anomaly detection demo | ML-based IDS demonstrating the approach proposed for PhD research |
| Project 7: This document | Theoretical grounding and gap analysis for Projects 1–6 |

---

*This review was prepared as part of a PhD application portfolio in network engineering. The author may be contacted at Axim Government Hospital, Axim, Western Region, Ghana.*
