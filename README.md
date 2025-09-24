# LSTM Multivariate Time Series Model

**Tujuan:**  
Membangun model prediksi temperatur udara berdasarkan data 5 hari terakhir mengenai 33 variabel kualitas udara dan meteorologis seperti PM10, NO, CO2, Wind Direction, dll.  

**Metodologi:**  
Model prediksi yang digunakan adalah model LSTM (Long Short-Term Memory). Pemilihan model LSTM dilatarbelakangi oleh kemampuannya untuk secara efektif menangkap depencency jangka panjang dan pendek (pola fluktuatif target variable) pada time series dataset. Selain itu, model LSTM dapat menangkap hubungan kompleks antara 33 variabel input yang dimiliki.

**Fitur-fitur dataset:**  
| Variabel | Deskripsi | Satuan |
| :--- | :--- | :--- |
| From Date | Starting date of data collection | - |
| To Date | Ending date of data collection | - |
| PM10 | Particulate Matter 10 | ug/m3 |
| PM2.5 | Particulate Matter 2.5 | ug/m3 |
| CO | Carbon Monoxide | mg/Nm3, mg/m3, ng/m3, ug/m3 |
| CO2 | Carbon Dioxide | mg/m3 |
| NO | Nitric Oxide | mg/m3, ppb, ppm, ug/m3 |
| NO2 | Nitrogen Dioxide | ug/m3 |
| NOx | Nitrogen Oxides | ppb, ppm, ug/m3 |
| NH3 | Ammonia | ppb, ug/m3 |
| SO2 | Sulfur Dioxide | ug/m3 |
| Temp | Temperature | degrees Celsius or ug/m3 |
| AT | Air Temperature | degrees Celsius or ug/m3 |
| BP | Barometric Pressure | W/mt2, mg/m3, mmHg |
| Benzene | Concentration of Benzene in the air | mg/m3 or ug/m3 |
| Toluene | Concentration of Toluene in the air | ug/m3 |
| VWS | Wind Speed | degree, m/s |
| Variance | Variance | n |
| WD | Wind Direction | deg, degree C, degree |
| WS | Wind Speed | m/s, ug/m3 |
| Xylene | Concentration of Xylene in the air | ug/m3 |
| CH4 | Methane | ug/m3 |
| Eth-Benzene | Concentration of Ethylbenzene in the air | ug/m3 |
| Gust | Wind Gust | kl/h, km/hr, m/s |
| HCHO | Formaldehyde | ug/m3 |
| Hg | Mercury | ug/m3 |
| MH | Mixing Height | meters (m) |
| MP-Xylene | Concentration of Meta-Para Xylene in the air | ug/m3 |
| NMHC | Non-Methane Hydrocarbons | ug/m3 |
| O Xylene | Concentration of Ortho-Xylene in the air | ug/m3 |
| Ozone | Ozone Concentration | ppb, ug/m3 |
| Power | Power Consumption | Watts (W) |
| RF | Rainfall | m/s, mm |
| RH | Relative Humidity | %, W/mt2, degree |
| SPM | Suspended Particulate Matter | ug/m3 |
| SR | Solar Radiation | W/mt2, ug/m3 |
| THC | Total Hydrocarbons | ug/m3 |

**Langkah analisis dan pemodelan:**  
1.	Exploratory Data Analysis (EDA)  
EDA dimulai dengan visualisasi line chart untuk target variable AT seiring berjalannya waktu. Hal ini dilakukan untuk menentukan apakah ada pola tertentu yang dapat digunakan dalam membuat model. Tanpa adanya pola tersebut, maka model yang dibuat tidak mungkin memprediksi AT dengan akurat.
2.	Pembersihan dan preprocessing data  
Dilakukan pengecekan missing value. Variabel ‘eth_benzene’ yang memiliki jumlah missing value 50,85% dihapuskan dari dataset karena dapat merusak akurasi model. Setelah itu, dilakukan pengecekan outlier menggunakan boxplot. Informasi ini digunakan di tahap selanjutnya, yaitu imputasi missing values. Kemudian, dataset dibagi menjadi dataset x dan y berdasarkan sliding window dengan ukuran lima. Terakhir, dataset dipisah menjadi training dan testing dataset  
3.	Pemodelan  
Base model dibangun dengan satu LSTM layer dan satu regressor layer. Setelah itu, model dilatih sebanyak sepuluh epoch saja. Setelah memvisualisasi loss dan MAE model, base model dimodifikasi dengan menambahkan dua LSTM layer. Model kedua pun dilatih menggunakan sepuluh epoch. Terakhir, dilakukan visualisasi loss dan MAE model.  
4.	Evaluasi model  
Selain menggunakan visualisasi MAE dan loss model, evaluasi juga dilakukan menggunakan skor MAE, MSE, dan R2 yang dilakukan pada testing dataset.  

**Hasil dan Kesimpulan:**  
Setelah membandingkan kinerja kedua model, ditemukan bahwa model kedua memiliki akurasi yang jauh lebih tinggi daripada model pertama. Berikut adalah skor masing-masing model.  
Base model MAE score: 28.658918180622038  
Base model MSE score: 1464.3793530144183  
Base model R2 score: -0.1957010917268791  

Modified model MAE score: 9.92235530888448  
Modified model MSE score: 241.13943737034398  
Modified model R2 score: 0.8031038283020051  

**Teknologi dan libraries yang digunakan:**  
•	LSTM Model  
•	pandas  
•	numpy  
•	matplotlib.pyplot   
•	scikit-learn  
•	numpy sliding window  
•	tensorflow  
