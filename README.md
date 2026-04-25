## 1. Dataset Description

The dataset used for this project is a **synthetic healthcare prior authorization dataset** created for the project **Priora: AI-Based Denial Risk and Denial Reason Prediction for Prior Authorization Workflows**. The domain of the dataset is **healthcare administration**, specifically the prior authorization process where healthcare providers submit treatment, procedure, drug, imaging, or device requests to insurance payers for approval.

The dataset was created because real prior authorization data is difficult to access due to healthcare privacy restrictions. Therefore, the project uses **synthetic case records, manually created structured samples, simulated denial letters, publicly inspired policy categories, and de-identified text templates**, which matches the data collection plan of the project. 

The dataset supports three machine learning tasks:

1. **Denial Risk Prediction**
   Predicts whether a prior authorization case will be approved or denied.

2. **Denial Reason Classification**
   Classifies the reason for denial from denial letter text or case explanation text.

3. **Document Completeness Prediction**
   Predicts whether the submitted prior authorization file is complete or incomplete.

The main topic is to help healthcare administrative staff identify risky prior authorization cases before submission and understand the likely reason if a case is denied. The reduced project scope focuses on supervised classification, NLP, feature engineering, model evaluation, and explainability, while excluding full PDF parsing, OCR, LLM fine-tuning, automatic appeal generation, and real insurer submission workflows. 

---

# 2. Features / Columns in the Dataset

Since Priora uses three classifiers, the dataset is divided into three related files.

---

# A. Denial Risk Prediction Dataset

This dataset is used to predict whether a prior authorization request is likely to be **Approved** or **Denied**. The project document states that this module uses structured features such as procedure type, diagnosis category, number of supporting documents, missing required conditions, referral status, lab report status, treatment history, policy match score, and note completeness score. 

| Feature / Column                      | Data Type                  | Description                                                                                         |
| ------------------------------------- | -------------------------- | --------------------------------------------------------------------------------------------------- |
| `case_id`                             | Text / Identifier          | Unique ID for each prior authorization case.                                                        |
| `patient_age`                         | Numerical                  | Age of the patient. Used to understand patient risk group.                                          |
| `age_group`                           | Categorical                | Age category such as child, adult, or senior.                                                       |
| `gender`                              | Categorical                | Patient gender category.                                                                            |
| `payer_type`                          | Categorical                | Type of insurance payer, such as Medicare, Medicaid, commercial, or self-pay.                       |
| `procedure_type`                      | Categorical                | Type of requested service, such as drug, imaging, procedure, DME, therapy, or surgery.              |
| `diagnosis_category`                  | Categorical                | Broad medical category of the diagnosis, such as cardiology, oncology, orthopedics, neurology, etc. |
| `urgency_level`                       | Categorical                | Priority of request, such as routine, urgent, or expedited.                                         |
| `service_setting`                     | Categorical                | Setting of care, such as inpatient, outpatient, emergency, or home health.                          |
| `num_supporting_documents`            | Numerical                  | Total number of documents attached with the request.                                                |
| `num_missing_required_conditions`     | Numerical                  | Number of payer-required conditions that are missing from the case.                                 |
| `referral_attached`                   | Categorical / Boolean      | Shows whether referral document is attached.                                                        |
| `lab_report_attached`                 | Categorical / Boolean      | Shows whether lab report is attached.                                                               |
| `clinical_note_attached`              | Categorical / Boolean      | Shows whether clinical note is attached.                                                            |
| `previous_treatment_history_included` | Categorical / Boolean      | Shows whether previous treatment history is included.                                               |
| `policy_match_score`                  | Numerical                  | Score showing how well the case matches payer policy requirements.                                  |
| `note_completeness_score`             | Numerical                  | Score showing how complete the clinical note is.                                                    |
| `prior_auth_required`                 | Categorical / Boolean      | Shows whether prior authorization is required for the request.                                      |
| `previous_denials_count`              | Numerical                  | Number of previous denials for similar requests or patient history.                                 |
| `estimated_cost`                      | Numerical                  | Estimated cost of requested treatment or service.                                                   |
| `decision`                            | Categorical / Target       | Final class label: Approved or Denied.                                                              |
| `denial_probability`                  | Numerical / Target Support | Probability score showing risk of denial.                                                           |

---

# B. Denial Reason Classification Dataset

This dataset is used for the NLP module. Its purpose is to classify the likely reason for denial from denial letter text or short case summaries. The project document defines this module as text-based and lists the possible denial reason classes: missing documentation, medical necessity not established, prior authorization not obtained, non-covered service, coding or billing issue, and duplicate/miscellaneous. 

| Feature / Column        | Data Type                  | Description                                                                            |
| ----------------------- | -------------------------- | -------------------------------------------------------------------------------------- |
| `case_id`               | Text / Identifier          | Unique ID for each denied case.                                                        |
| `denial_letter_text`    | Text                       | Main denial letter or denial paragraph written in natural language.                    |
| `short_denial_summary`  | Text                       | Short summary of the denial reason.                                                    |
| `case_explanation_text` | Text                       | Extra case explanation text describing why the request may have been denied.           |
| `procedure_type`        | Categorical                | Type of requested service, such as drug, imaging, procedure, DME, therapy, or surgery. |
| `diagnosis_category`    | Categorical                | Medical category related to the case.                                                  |
| `payer_type`            | Categorical                | Type of payer involved in the denial.                                                  |
| `reason_class`          | Categorical / Target       | The target class showing the denial reason category.                                   |
| `confidence_score`      | Numerical / Target Support | Confidence score associated with the predicted reason class.                           |

## Denial Reason Classes

| Reason Class                        | Meaning                                                                               |
| ----------------------------------- | ------------------------------------------------------------------------------------- |
| `missing_documentation`             | Required documents or evidence were missing.                                          |
| `medical_necessity_not_established` | The submitted information did not prove that the service was medically necessary.     |
| `prior_authorization_not_obtained`  | Authorization was required but was not obtained before the service.                   |
| `non_covered_service`               | The requested service is not covered under the patient’s plan.                        |
| `coding_or_billing_issue`           | There was an issue with diagnosis code, procedure code, modifier, or billing details. |
| `duplicate_or_miscellaneous`        | The request was duplicate or denied for another administrative reason.                |

---

## Short Version for Direct Submission

You can paste this if you want a smaller answer:

The dataset used in this project is a synthetic healthcare prior authorization dataset created for **Priora: AI-Based Denial Risk and Denial Reason Prediction for Prior Authorization Workflows**. The domain is healthcare administration, specifically prior authorization requests, denial prediction, denial reason classification, and document completeness checking. Real prior authorization data is difficult to access because of privacy restrictions, so the dataset was created using synthetic case records, manually created structured samples, simulated denial letters, publicly inspired policy categories, and de-identified text templates. This follows the project methodology, which states that the system will use structured and text-based datasets for supervised classification and NLP tasks. 

The main features include patient and case information, such as age, age group, gender, payer type, procedure type, diagnosis category, urgency level, number of supporting documents, missing required conditions, referral status, lab report status, previous treatment history, policy match score, and note completeness score. These are mainly numerical and categorical features used for the Denial Risk Predictor. The text-based dataset includes denial letter text, short denial summary, and case explanation text, which are used by the Denial Reason Classifier. The target class for this model is the denial reason category, such as missing documentation, medical necessity not established, prior authorization not obtained, non-covered service, coding or billing issue, and duplicate or miscellaneous. The optional Document Completeness Predictor uses features such as clinical note presence, diagnosis code presence, procedure code presence, lab report attached, referral attached, number of required fields missing, and total documents attached to predict whether the file is complete or incomplete.


## Report for Denial Risk Prediction:

Dataset Description:
The dataset used for this project is `denial_risk.csv`. This data was sourced from the American Health Association and synthetic records modeled after real-world healthcare administrations for machine learning purposes, focusing on variety, differentiation, and normality. It focuses on the Prior Authorization domain, which is the process healthcare providers use to obtain approval from insurance payers before a service is provided to ensure proper insurance provision. The dataset has nominal, ordinal, and numerical columns with many parameters.

Machine Learning Models Used:
For this project, we will be implementing two distinct models:

Logistic Regression:
Our initial model is used to establish an understanding of the linear relationships between costs, policy match scores, and outcomes, for the output of provision as a binary result.

Random Forest Classifier:
Our second model, which will utilize a group of decision trees for the complex, non-linear logic in medical claim denials, for better outcomes and accuracy.

Why These Models are Suitable:

Logistic Regression:
This is chosen for the first phase because it is simple, and generally good and reliable. In healthcare, understanding that a model thinks a claim might be denied is just as important as the prediction itself. It provides a clear mathematical floor.

Random Forest:
This model is suitable because insurance denials often follow "Decision Tree" logic, for if this then that analogy. The Random Forest mirrors human decision-making process but at a scale of thousands of data points, allowing for a significant jump in accuracy and consistency.

## Report for Denial Reason Classification:

Dataset Description:
The dataset used for this phase is `denial_reason.csv`. It contains synthetic prior-authorization denial records focused on denial-reason prediction. The data includes structured categorical and numeric fields such as `payer_name`, `request_type`, `diagnosis_category`, `supporting_doc_count`, and `missing_required_conditions`, along with text fields such as `denial_text`, `short_denial_summary`, and `policy_excerpt`. The target label for the main task is `detailed_denial_reason`, which makes this a multiclass classification problem.

Methodology:
The initial exploration in `notebooks/denial_reason.ipynb` shows that the dataset contains both structured features and useful denial-text content. The next step is to preprocess the data by handling missing values, encoding categorical variables, and converting the text fields into machine-learning features using TF-IDF. After preprocessing, the dataset can be split into training and testing sets to evaluate model performance using accuracy, precision, recall, and F1-score. Since the class distribution is uneven, weighted F1-score should be treated as one of the main evaluation metrics.

Machine Learning Models Used:
Two models are proposed for this task:

Logistic Regression:
This will be the first working model for the phase one submission. Logistic Regression is a strong baseline for multiclass classification, especially when paired with TF-IDF text features. It is efficient, interpretable, and works well for identifying how denial language and structured inputs relate to the final denial reason class.

Random Forest Classifier:
This will be the second model in the project. Random Forest is suitable for capturing non-linear relationships among the structured variables such as payer, diagnosis category, request type, and documentation counts. It can model rule-like behavior in denial decisions and serves as a useful comparison against the linear baseline.

Why These Models Are Suitable:

Logistic Regression:
This model is suitable because the denial-reason task is a supervised multiclass classification problem, and the text-heavy dataset can be represented effectively with TF-IDF features. Logistic Regression provides a clean baseline that is easy to train, explain, and compare.

Random Forest Classifier:
This model is suitable because denial outcomes are often influenced by combinations of categorical and numeric conditions rather than a single linear pattern. Random Forest can capture more complex interactions across the structured features and may improve performance where tree-style decision logic matters.
