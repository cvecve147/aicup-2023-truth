# AICUP-2023-Truth

## 環境安裝
使用 docker 安裝相關環境
```
sudo docker run --gpus all --shm-size=1G  -v "${PWD}:/workspace"  -it -p 8888:8888 autogluon/autogluon:0.7.0-cuda11.7-jupyter-ubuntu20.04-py3.9 /bin/bash
```
啟動 jupyter lab
```
jupyter lab --port=8888 --ip=0.0.0.0 --allow-root
```

## 資料
- `private_test_data.jsonl` 原始 private_test 資料
- `public_test.jsonl` 原始 public_test 資料
- `public_train_0316.jsonl`  原始 public_train_0316 資料
- `public_train_0522.jsonl` 原始 public_train_0522 資料
- `merged.jsonl` 刪除 claim 中的空白訓練資料
- `public_train.jsonl` 刪除空白、處理衝突 label、利用 claim 合併證據的資料
- `public_test_data.jsonl` 刪除 claim 中的空白資料

處理程式碼
- `preprocess.ipynb` 在資料的後三筆是由此程式碼產生而來

## 訓練程式碼
`main.ipynb` 由比賽 baseline 程式碼修改而來，主要使用 hanlp +  chinese-lert-base，模型訓練皆使用 autogluon 來輔助訓練過程
- 執行前需要先將wiki-pages放入Data中

## 預測
`test.ipynb` 由比賽 baseline 程式碼修改而來，主要使用 hanlp +  chinese-lert-base
- 設定載入模型，修改這兩變數將權重下載下來後載入模型路徑
    - `step2_model = 'step2_new_upload'` 
    - `step3_model = 'step3_new_upload'`


## 模型權重

|                  Model Type                   | Public Score | Private Score |                                               URL                                                |
| :-------------------------------------------: | :----------: | :-----------: | :----------------------------------------------------------------------------------------------: |
| hanlp + chinese-lert-base * 2 |   0.592518   |   0.678255    | [Download](https://drive.google.com/drive/folders/1-4sLL-tQtZC1QEXegeoR3c6Qi3GRvkjM?usp=sharing) |

- 因為實驗室電腦被攻擊資料被刪除，這是在比賽最後一周訓練的權重，並且只保留最佳模型
- 所有權重的訓練參數與設定都在此資料夾中 assets.json、config.yaml 檔案，大多數參數都使用Autogluon預設參數
