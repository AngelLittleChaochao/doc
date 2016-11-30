# Chinese FAQ Extraction

1. Label Data
	
   Label data by starting project 'TrainingDataLabeler' in Visual Studio 2015. The project in solution QAExtractionV7.
	
   Merge all labeled data to one file.
	
2. Copy labeled data to CAAP-HealthCare/faq/label_datas/faq.chinese.v2.label.txt

3. Train model   
   Training model by running model trainer in CAAP-HealthCare/faq/faq/
	
	```
	$ python3 model_trainer.py -l ../label_datas/faq.chinese.v2.label.txt
	```
	The model will ouput to CAAP-HealthCare/faq/faq/model_outputs.
	Running the model multiple times, when the precision is > 92%, it can be used.
	
4. Copy trained model to CAAP-HealthCare/faq/models/faq.chinese.v2.label.pkl
5. Run tests   
   Add your tests in CAAP-HealthCare/faq/tests/question_predictor_test.py.  
   **Attention**: change model path to the new chinese model.
   Run tests, you can running all tests or specific one:  
   
   ```
   $ python3 -m unittest question_predictor_test.py
   $ python3 -m unittest question_predictor_test.TestQuestionPredictor.test_isquestion
   ```
6. Test html
   Use file in CAAP-HealthCare/faq/faq/qa_extractor_factory.py
   
   Specific language and uri to extract qa.
   
   ```
   $ python3 qa_extractor_factory.py -u fileOrUrl -l cn_v2
   ```

7. Try extract faq by server side
   
   Install all related packages in CAAP-HealthCare/faq/
   
   ```
   $ gulp install
   ```
   
   Go to CAAP-HealthCare/faq/faqserver, and start server
   
   ```
   $ python3 index.py
   ```
   
   And access [http://localhost:3333](http://localhost:3333/) in your browser

