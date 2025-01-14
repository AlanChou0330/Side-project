資料來源:
==
>數據資料來源為美國加利福尼亞大學爾灣分校UCI的開源資料 <https://archive.ics.uci.edu/> 裡的
<https://archive.ics.uci.edu/dataset/161/mammographic+mass> 乳房X光數值

研究動機與目標:
==
>長年以來，癌症一直是台灣死因中最主要的原因之一，與第二名相比，其發生率高出了2倍。全球科學家一直在努力研究，希望能夠減少癌症所造成的悲劇。
根據台灣衛福部國健署的統計數據，女性乳癌的發病率逐年上升，從110年的2913人佔比17.1%，提升至111年的24.1%。這樣的增長速度非常令人擔憂。
乳癌檢測的主要方法之一是X光攝影檢查，其優點在於對早期乳癌的鈣化點具有敏感檢測能力，可以在疾病早期進行預防和治療。
然而，這種檢查需要對乳房進行緊壓，可能會引起疼痛和低劑量輻射，因此通常建議每1到2年進行一次檢查。
由於檢測的準確性無法達到100%，因此我們希望通過應用AI機器學習技術來提高檢測準確率，並準確判斷腫瘤的性質，是良性還是惡性。

大致步驟:
==
 ### 一. 資料預處理
> * 匯入所需的模組，包括 sklearn 的各種機器學習模型和評估工具，以及 matplotlib 用於繪圖。
> * 對資料進行預處理，包括標準化和正規化。
 ### 二. 建立模型評估準確度
> * 使用決策樹模型進行訓練，並使用交叉驗證評估模型的準確度。
> * 使用隨機森林模型進行訓練，並使用交叉驗證評估模型的準確度。
> * 使用支持向量機模型進行訓練，並使用交叉驗證評估模型的準確度。
> * 使用 K 最近鄰模型進行訓練，並使用交叉驗證評估模型的準確度。
> * 使用多項式貝葉斯模型進行訓練，並使用交叉驗證評估模型的準確度。
> * 使用邏輯回歸模型進行訓練，並使用交叉驗證評估模型的準確度。
 ### 三. 結果視覺化
> * 繪製各模型的準確度折線圖和直方圖，以便比較各模型的性能。每一步驟都會計算模型的平均準確度並將其印出。

技術:
==
### 標準化 : 特徵資料按比例縮放，讓資料落在某一特定的區間
* #### 優點:
##### 一、消除特徵間的尺度差異 : 
>不同特徵的尺度可能不同，如果不對特徵進行標準化，尺度較大的特徵可能會主導模型的訓練，從而導致模型訓練不穩定或性能下降。
##### 二、加速模型收斂 : 
>某些機器學習算法需要計算特徵之間的距離或相似度，例如 K 近鄰和支持向量機。如果特徵未標準化，則這些計算可能會受到尺度不匹配的影響，從而導致模型收斂速度變慢。
##### 三、降低數值範圍對權重的影響 : 
>特徵的數值範圍可能會影響權重的估計，從而對模型產生偏差。通過標準化，可以降低這種影響，使得模型更加公平地估計權重。
##### 四、減少模型過擬合的風險 : 
>適當的標準化可以減少模型對離群值的敏感度，從而降低過擬合的風險。這是因為標準化可以將特徵的數值範圍調整到較小的範圍，使得模型更加穩健。
* #### 缺點 :
##### 一、資訊損失 :
>在進行標準化的過程中，會將原始數據轉換為具有均值為0和標準差為1的新數據。這樣的轉換可能會導致部分數據的原始資訊丟失。
##### 二、對離群值的敏感性 :
>標準化過程中使用的均值和標準差是受離群值影響的。如果數據集中存在離群值，則這些極端值可能會對均值和標準差產生影響，進而對標準化後的結果產生影響。
##### 三、不適用於所有分佈 :
>標準化假設數據服從正態分佈，但在實際情況中，數據不一定符合這種分佈。因此，對於非正態分佈的數據，標準化可能不適用或效果不佳。
##### 四、可能導致過度擬合 :
>標準化後的數據可能會增加模型的複雜性，進而增加過度擬合的風險。特別是在樣本量較小的情況下，這種風險更加顯著。

-----------------------------------------------------------------------------------------------------------
### K-fold 交叉驗證 : 主要目的是評估模型的性能和泛化能力
##### 優點:
##### 一、模型性能評估 :
>交叉驗證提供了一種客觀的方法來評估機器學習模型的性能，並測試其對未見數據的泛化能力。
##### 二、降低過擬合風險 :
>通過將數據集分為訓練和測試集，K-fold 交叉驗證可以幫助減少模型對訓練數據的過度擬合。
##### 三、最大化數據利用率 :
>K-fold 交叉驗證允許使用每個樣本的數據進行訓練和測試，從而最大化了數據的利用率。
##### 缺點 :
##### 一、計算成本高 :
>交叉驗證需要訓練和測試模型 K 次，因此計算成本相對較高，特別是對於大型數據集和複雜的模型。
##### 二、時間消耗大 :
>需要 K 次訓練和測試模型，因此需要更多的時間來執行 K-fold 交叉驗證。
##### 三、不適用於時間序列數據 :
>交叉驗證對於時間序列數據不太適用，因為它破壞了數據的時間順序。





# 詳細流程:
## 1.對資料進行基本的前處理、標準化: 
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/data1.png" width="550"/>
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/data2.png" width="400"/>

### 再繪製出直方圖和箱線圖來更直觀的看到資料前處理以及標準化帶來的變化: (紅色數值為明顯變化數值)
##### 直方圖
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/DataPreprocessing_1.png" width="600"/>
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/DataPreprocessing_2.png" width="600"/>

##### 箱線圖
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/DataPreprocessing_3.png" width="600"/>
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/DataPreprocessing_4.png" width="600"/>

## 2.用決策樹來訓練測試數據集:
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/Decision Trees.png" width="900"/>
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/cv_DecisionTrees.png" width="900"/>

## 3.用隨機森林來訓練測試數據集:
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/cv_RandomForest.png" width="900"/>

## 4.用SVM支撐向量機來訓練測試數據集:
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/cv_SVM.png" width="900"/>

## 5.用KNN來訓練測試數據集:
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/cv_KNN.png" width="900"/>

## 6.用Naive Bayes貝氏分類器來訓練測試數據集:
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/cv_NaiveBayes.png" width="900"/>

## 7.用Logistic Regression邏輯迴歸來訓練測試數據集:
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/cv_LogisticRegression.png" width="900"/>

## 8.總結比較各模型準確率:
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/cv_All.png" width="900"/>
<img src="https://github.com/AlanChou0330/Breast-Cancer---machine-learning/blob/main/picture/cv_AllMean.png" width="900"/>

# 總結
### 經過實際測試，KNN模型對於這類型的X光片數據展現出較高的準確性和可靠性，這一發現對於改善乳癌檢測流程，提高準確性，並減少誤診率具有重要意義，有望對提高乳癌患者的生存率和生活品質產生積極正面影響。
### 由於數據集資料數不夠多，無法有效的解決過擬合問題，日後蒐集到更多數據繼續研究減緩此現象
