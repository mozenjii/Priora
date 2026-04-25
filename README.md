Report for Denial Risk Prediction: 

Dataset Description: 
                   The dataset used for this project is 'denial_risk.csv'. This data was sourced from the American Health Association and synthetic records modeled after real-world healthcare administrations for machine learning purposes, focusing on variety, differentiation, and normality. It focuses on the Prior Authorization domain, which is the process healthcare providers use to obtain approval from insurance payers before a service is provided to ensure proper insurance provision. Ther dataset has nominal, ordinal, and numerical columns with many parameters.  

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
