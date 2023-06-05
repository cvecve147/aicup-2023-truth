# AICUP-2023-Truth
## 語言
[![中文](https://img.shields.io/badge/language-%E4%B8%AD%E6%96%87-blue)](README.md)
[![English](https://img.shields.io/badge/language-English-blue)](README_EN.md)

## 環境設置
**硬體要求：**
- CPU: Intel i7-8700 (12) @ 4.600GHz 
- GPU: NVIDIA GeForce GTX 1080 Ti 
- 內存: 62.66GiB 
- 顯卡內存: 至少需要10GB
- RAM: 至少需要16GB

使用 Docker 安裝環境：
```
sudo docker run --gpus all --shm-size=1G -v "${PWD}:/workspace" -it -p 8888:8888 autogluon/autogluon:0.7.0-cuda11.7-jupyter-ubuntu20.04-py3.9 /bin/bash
```
啟動 Jupyter lab：
```
jupyter lab --port=8888 --ip=0.0.0.0 --allow-root
```
安裝依賴：
```
pip install -r requirements.txt
```


## 資料
- `private_test_data.jsonl`: 原始 private_test 資料
- `public_test.jsonl`: 原始 public_test 資料
- `public_train_0316.jsonl`: 原始 public_train_0316 資料
- `public_train_0522.jsonl`: 原始 public_train_0522 資料
- `merged.jsonl`: 移除 claim 中空白的訓練資料
- `public_train.jsonl`: 移除空白、處理衝突標籤、根據 claim 合併證據的資料
- `public_test_data.jsonl`: 移除 claim 中空白的資料

資料處理程式碼：
- `preprocess.ipynb`: 最後三筆資料由此程式碼生成，主要處理資料清理、資料整合和資料一致性檢查。

## 訓練程式碼
`main.ipynb`: 基於比賽基線程式碼修改，主要使用 hanlp + chinese-lert-base。模型訓練過程由 autogluon 協助，並使用 AdamW 作為優化器。所有訓練參數和設定都在權重目錄的 assets.json 和 config.yaml 檔案中。訓練結束後直接進行預測。
- 執行前需要先將 wiki-pages 放入 Data 文件夾

## 預測
`test.ipynb`: 基於比賽基線程式碼修改，主要使用 hanlp + chinese-lert-base。執行 test.ipynb 中的所有程式碼即可產生最佳提交結果。
- 載入模型設定，下載權重後修改以下兩個變數以載入模型路徑：
  - `step2_model = 'step2_new_upload'`
  - `step3_model = 'step3_new_upload'`

## 模型權重
| Model Type | Public Score | Private Score | URL |
|---|---|---|---|
| hanlp + chinese-lert-base * 2 | 0.592518 | 0.678255 | [Download](https://drive.google.com/drive/folders/1-4sLL-tQtZC1QEXegeoR3c6Qi3GRvkjM?usp=sharing) |

- 由於實驗室電腦被攻擊，資料被刪除，這是在比賽最後一週訓練的權重，且僅保留最佳模型。
- 所有權重的訓練參數和設定都在該權重目錄的 assets.json 和 config.yaml 檔案中，大部分參數使用 Autogluon 預設參數。
