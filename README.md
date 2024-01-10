# 文案抄襲檢查工具

這是一個使用 Streamlit 和 BERT 模型來檢查文案抄襲的簡單應用。

## 功能

- 切割輸入的文案成為多個段落。
- 使用 Google Custom Search API 來尋找每個段落可能的抄襲來源。
- 計算輸入段落與搜尋結果的相似度。
- 顯示相似度高於95%的段落，並提供相關資訊。

## 安裝指南

首先，複製此倉庫到本地：
bash
git clone https://your-repository-url.git
cd your-repository-directory

然後，安裝所需的依賴項：
bash
pip install -r requirements.txt

bash
streamlit run plagiarism-check.py


在瀏覽器中打開顯示的 URL，按照指示輸入文案並檢查抄襲。
