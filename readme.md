# Wczesna Detekcja Ryzyka Udarowego: Modelowanie ML z Wykorzystaniem Explainable AI (XAI), XGBoost
 * Autor: Aleksander Śmiałowski 
 * Cel: Projekt Portfolio (Data Science / Machine Learning)
 * Zbiór danych: Stroke Prediction Dataset (fedesoriano)

* Wprowadzenie 
- Udar mózgu jest jedną z głównych przyczyn zgonów i niepełnosprawności na świecie. Z perspektywy medycznej i farmaceutycznej, kluczowym wyzwaniem nie jest tylko leczenie skutków, ale przede wszystkim wczesna identyfikacja pacjentów wysokiego ryzyka. Pozwala to na wdrożenie działań prewencyjnych (leczenie nadciśnienia, zmiana stylu życia, farmakoterapia przeciwzakrzepowa).

 * Główne wyzwania projektu:
 - Niezbalansowane dane (Imbalanced Data): Przypadki udaru stanowią zaledwie ok. 4.8% zbioru.
 - Konsekwencje błędów (Cost of Error): W medycynie koszt False Negative (niezdiagnozowanie chorego) jest znacznie wyższy niż koszt False Positive (niepotrzebne badania kontrolne).
 - Interpretowalność (Black Box Problem): Model w medycynie musi być wyjaśnialny zdrowotnie/biologicznie. 
 - Wyniki: Priorytetem dla mnie będzie Recall oraz ROC AUC

* Na czym się skupię ? 
- Advanced Feature Engineering : Zamiast polegać wyłącznie na surowych danych, mam w planach stworzyć  nowe zmienne oparte na wiedzy medycznej (np. interakcje wieku z glukozą, wskaźniki chorób współistniejących)
- Strategia dla Danych Niezbalansowanych : Zamiast sztucznego generowania danych przez(SMOTE) użyje mechanizmu ważenia klas (scale_pos_weight)
- OPTUNA: zastąpie klasycznego Grid Searcha Optuna w celu efektywnego dostrojenia hiperparametrów modelu XGBoost.
- Explainable AI (SHAP): Wykorzystam SHAP w celu sprawdzenia czy model podejmuję decyzję na podstawię logicznych przesłanek medycznych. 

* Lista rzeczy znajdujących się w projekcie 
- Importy
- Pobranie oraz przegląd danych 
- EDA na brudnych danych 
-  Data Cleaning, Preprocesing, Feature Enginering
- Tuning Hiperparametrów (OPTUNA)
-  Model XGBoost
- Wyniki 
- XAI (SHAP)
- Symulacja diagnozy jednego pacjenta (Waterfall PLOT)
- Raport Końcowy 




# RAPORT KOŃCOWY 
* Uwaga dodałem poprawę wyświetlania błędów i uruchomiłem skrypt jeszcze raz. Wyniki mogą się lekko różnić
 * Skuteczność Diagnostyczna (Performance Summary)
 - Zbudowany model XGBoost osiągnął ROC AUC na poziomie 0.84
 - Wysoki Priorytet Czułości (Recall = 80%): Dzięki zastosowaniu techniki ważenia klas (scale_pos_weight), optymalizacji za pomocą Optuna oraz dzięki inżynierii cech model skutecznie identyfikuje 4 na 5 pacjentów zagrożonych udarem
 - Niska precyzja (15%) jest świadomą decyzją projektową. W kontekście klinicznym oznacza że system generuję duża ilość alarmów dla pacjentów którzy nie są zagrożeni udarem. Aczkolwiek koszt badań profilaktycznych/prewencyjnych jest nieporównywalnie niższy, niż koszt leczenia osoby po udarzę. 

 * Wartość inżynierii Cech 
- Analiza SHAP (Explainable AI) jednoznacznie potwierdziła hipotezę, że ryzyko udaru nie jest sumą prostych czynników, lecz wynikiem ich nieliniowych interakcji.
 - Zmienne stworzone w procesie Feature Engineeringu – age_bmi_interaction ,  age_glucose_interaction praz comorbidity score znalazły się wysoko w analizie SHAP. Dowodzi to temu iż otyłość , wysoki poziom cukru, choroby krązenia lub serca połączone z zaawansowanym wiekiem stają się krytyczne dla powstania udaru 

* Interpretowalność i Zaufanie
- Model nie działa jako "czarna skrzynka". Dzięki implementacji SHAP Waterfall Plots, system jest w stanie wygenerować raport wyjaśniający, dlaczego dany pacjent został zakwalifikowany do grupy ryzyka
- Jest to kluczowy wymóg przy wdrażaniu systemów AI w podmiotach leczniczych (zgodnie z wytycznymi EU AI Act).
