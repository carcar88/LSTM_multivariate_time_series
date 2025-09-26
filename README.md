# LSTM Multivariate Time Series Model

**Tujuan:**  
Membangun model prediksi temperatur/kualitas udara berdasarkan data 5 hari terakhir mengenai 33 variabel kualitas udara dan meteorologis seperti PM10, NO, CO2, Wind Direction, dll.  

**Metodologi:**  
Model prediksi yang digunakan adalah model LSTM (Long Short-Term Memory). Pemilihan model LSTM dilatarbelakangi oleh kemampuannya untuk secara efektif menangkap _depencency_ jangka panjang dan pendek (pola fluktuatif _target variable_) pada _time series dataset_. Selain itu, model LSTM dapat menangkap hubungan kompleks antara 33 variabel _input_ yang dimiliki.

**Fitur-fitur _Dataset_:**  
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

**Langkah Analisis dan Pemodelan:**  
1.	_Exploratory Data Analysis_ (EDA)  
EDA dimulai dengan visualisasi line chart untuk _target variable_ AT seiring berjalannya waktu. Hal ini dilakukan untuk menentukan apakah ada pola tertentu yang dapat digunakan dalam membuat model. Tanpa adanya pola tersebut, maka model yang dibuat tidak mungkin memprediksi AT dengan akurat.
2.	Pembersihan dan _preprocessing_ data  
Dilakukan pengecekan _missing value_. Variabel ‘eth_benzene’ yang memiliki jumlah _missing value_ 50,85% dihapuskan dari _dataset_ karena dapat merusak akurasi model. Setelah itu, dilakukan pengecekan _outlier_ menggunakan boxplot. Informasi ini digunakan di tahap selanjutnya, yaitu imputasi _missing values_. Kemudian, _dataset_ dibagi menjadi _dataset_ x dan y menggunakan _sliding window_ dengan ukuran lima. Terakhir, _dataset_ dipisah menjadi _training_ dan _testing dataset_. 
3.	Pemodelan  
_Base model_ dibangun dengan satu LSTM _layer_ dan satu _regressor layer_. Setelah itu, model dilatih sebanyak sepuluh _epoch_ saja. Setelah memvisualisasi _loss_ dan MAE model, _base model_ dimodifikasi dengan menambahkan dua LSTM _layer_. Model kedua pun dilatih menggunakan sepuluh _epoch_. Terakhir, dilakukan visualisasi _loss_ dan MAE model.  
4.	Evaluasi model  
Selain menggunakan visualisasi MAE dan _loss_ model, evaluasi juga dilakukan menggunakan skor MAE, MSE, dan R2 yang dilakukan pada _testing dataset_.  

**Hasil dan Kesimpulan:**  
Setelah membandingkan kinerja kedua model, ditemukan bahwa model kedua memiliki akurasi yang jauh lebih tinggi daripada model pertama. Berikut adalah skor masing-masing model.  
_Base model MAE score_: 28.658918180622038  
_Base model MSE score_: 1464.3793530144183  
_Base model R2 score_: -0.1957010917268791  

_Modified model MAE score_: 9.92235530888448  
_Modified model MSE score_: 241.13943737034398  
_Modified model R2 score_: 0.8031038283020051  

**Teknologi dan _Libraries_ yang Digunakan:**  
•	LSTM Model  
•	pandas  
•	numpy  
•	matplotlib.pyplot   
•	scikit-learn  
•	numpy sliding window  
•	tensorflow  
