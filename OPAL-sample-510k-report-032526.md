Medical Device Review Report: uMI Panvivo PET/CT System
Section I: Product Description and Specifications
The uMI Panvivo series consists of high-performance Positron Emission Tomography (PET) and Computed Tomography (CT) systems. The following table summarizes the physical and system specifications based on the scalable detector ring architecture.

Table 1: System Physical and Functional Specifications
Feature	uMI Panvivo	uMI Panvivo S	uMI Panvivo ES	uMI Panvivo EX
Number of PET Rings	100	80	180	240
Axial Field of View (aFOV)	295 mm	235 mm	534 mm	712 mm
Scintillator Material	LYSO	LYSO	LYSO	LYSO
CT Slice Count	160-slice	160-slice	160-slice	160-slice
Maximum Table Load	280 kg	280 kg	280 kg	280 kg
Coincidence Window	4.6 ns	4.6 ns	4.9 ns	4.9 ns
Section II: Safety and Performance Data
The device has been evaluated against international standards for electrical safety, radiation protection, and electromagnetic compatibility.

Table 2: Safety Standards and Regulatory Compliance
Category	Requirement / Standard	Review Outcome	Remarks
Electrical Safety	ANSI/AAMI ES60601-1	[X] Compliant	Covers basic safety and essential performance.
Electromagnetic Compatibility	IEC 60601-1-2	[X] Compliant	Verified immunity to electromagnetic disturbances.
Radiation Safety	IEC 60601-1-3 / 60601-2-44	[X] Compliant	Specific requirements for CT and radiation protection.
Laser Safety	IEC 60825-1	[X] Compliant	Classification of laser products for patient positioning.
Software Lifecycle	IEC 62304	[X] Compliant	Software development and maintenance processes verified.
Biocompatibility	ISO 10993-1 / -5 / -10	[X] Compliant	Evaluated for patient-contacting parts (headrest/table).
Section III: Machine Learning and Algorithm Performance
The uMI Panvivo integrates several AI-driven algorithms to enhance image quality and mitigate artifacts.

Table 3: Machine Learning Algorithm Verification Summary
Algorithm	Purpose	Performance Metric	Result
DeepMAC	Metal Artifact Reduction	HU Difference (Affected vs. Control)	< 10 HU
uExcel DPR	Deep Progressive Reconstruction	Maximum Noise Reduction	47% reduction
OncoFocus	Respiratory Motion Correction	SUVmax Change (ΔSUVmax)	> 0% (Improvement)
NeuroFocus.Brain	Head Motion Management	High-uptake region recovery (ΔSUVmean)	< 10% deviation
AI EFOV	Extended FOV Attenuation	SUV Deviation	< 5% deviation
Section IV: Substantial Equivalence Comparison
The proposed device is compared against the primary predicate (K251839) to ensure safety and effectiveness.

Table 4: Technological Comparison with Predicate Device
Parameter	Proposed Device (uMI Panvivo)	Predicate (K251839)	Comparison Result
Indications for Use	PET/CT Imaging, Oncology, Cardiology	Identical	Equivalent
Spatial Resolution	< 3.5 mm (Axial FWHM @ 1cm)	< 3.5 mm	Same
Sensitivity	Up to 85 cps/kBq (EX Model)	Up to 16 cps/kBq	Improved (Note 3)
Time-of-Flight (TOF)	< 245 ps	< 245 ps	Same
Coregistration Accuracy	< 3.0 mm	< 3.0 mm	Same
Section V: Clinical and Non-Clinical Testing
Validation included phantom studies and clinical volunteer datasets to confirm diagnostic quality.

Table 5: Validation Dataset Demographics (Clinical)
Algorithm Validation	Subjects (N)	Primary Ethnicity	BMI Groups	Diagnostic Confidence
DeepMAC	20	Asian/Caucasian/Negroid	Various	Pass (Board Certified Review)
uExcel DPR	8	Asian	Healthy to Obese	Pass (Improved Sharpness)
OncoFocus	13	Asian	Healthy/Overweight	Pass (Reduced Artifacts)
NeuroFocus.Brain	7	Asian	Healthy/Overweight	Pass (Improved Alignment)
AI EFOV	4	Asian	Overweight	Pass (Homogeneity verified)
Associated Entities and Context
uMI Panvivo: The primary medical device system under review, comprising multiple PET/CT models.
Shanghai United Imaging Healthcare Co., Ltd.: The sponsor and manufacturer responsible for the 510(k) submission.
K253564: The 510(k) premarket notification number assigned to the proposed device.
K251839: The 510(k) number of the predicate device used for substantial equivalence.
LYSO (Lutetium-yttrium oxyorthosilicate): The scintillator material used in the PET detector rings.
Axial Field of View (aFOV): The longitudinal coverage of the PET detectors, ranging from 235 mm to 712 mm.
DeepMAC: A machine learning post-processing technology for metal artifact reduction.
uExcel DPR: A deep learning-based PET reconstruction algorithm (Deep Progressive Reconstruction).
OncoFocus: A motion correction technique for respiratory signal generation and attenuation map synthesis.
NeuroFocus.Brain: A head-motion management solution utilizing AI for brain PET imaging.
AI EFOV: An algorithm used to improve CT value accuracy when objects exceed the standard field of view.
SUV (Standardized Uptake Value): A quantitative metric in PET used to assess radiopharmaceutical concentration.
SNR (Signal-to-Noise Ratio): A performance metric used to evaluate image quality and noise levels.
NEMA NU 2-2018: The industry-standard performance measurement protocol for PET systems.
IEC 60601-2-44: The particular safety standard for X-ray equipment for computed tomography.
ISO 14971: The international standard for the application of risk management to medical devices.
DICOM: The standard for Digital Imaging and Communications in Medicine, ensuring interoperability.
PMMA Phantom: A polymethyl methacrylate object used for quantitative evaluation in CT testing.
FDG (18F-FDG): The primary radiopharmaceutical (fluorodeoxyglucose) supported by the reconstruction algorithms.
Intelligent Assistant: A local auxiliary query tool provided for operational support and troubleshooting.
Comprehensive Follow-up Questions for Review
Does the increase in the coincidence window to 4.9 ns for the ES and EX models adversely affect the random coincidence rate?
Can the manufacturer provide the specific validation report for the 280 kg table load, specifically regarding motor durability?
What are the specific inclusion criteria for the 20 volunteers used in the DeepMAC validation study?
How does the system maintain PET/CT coregistration accuracy across the extended 712 mm aFOV in the EX model?
Is the Intelligent Assistant tool capable of modifying any scanning parameters, or is it strictly read-only?
What is the specific software version number for the reconstruction engine used in this submission?
Provide the risk analysis for the NeuroFocus.Brain algorithm when used with non-FDG tracers.
Are there any specific cleaning or disinfection restrictions for the patient-contacting parts tested under ISO 10993?
How is the "ground truth" established for the AI EFOV algorithm training in the absence of manual annotation?
Does the 160-slice CT system utilize any specific dose-reduction technologies like iterative reconstruction?
Provide a detailed breakdown of the "other accessories" included in the system description.
What is the expected lifetime of the LYSO scintillators under typical clinical workloads?
Can the system perform simultaneous PET/CT acquisition, or are they exclusively sequential?
How does the system handle power fluctuations, as defined in the IEC 60601-1-2 EMC testing?
Are there any cybersecurity measures in place to protect the training datasets used for the AI algorithms?
What are the specific thermal environment limits for the storage of the detector modules?
Provide the specific spatial resolution results for the ES and EX models at the edge of the 712 mm FOV.
Does the uExcel DPR algorithm support tracers other than 18F-FDG for the Panvivo and Panvivo S models?
What is the reconstruction time for a full-body scan using the 240-ring EX model compared to the 100-ring base model?
Are there any identified residual risks following the implementation of the AI-driven motion correction features?
