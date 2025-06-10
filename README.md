# Handwriting OCR Script Description

This Python script extracts text from handwritten images using an API. It processes multiple images from a specified directory and saves the extracted text into both JSON and Excel files.

## Purpose

The script automates the process of extracting handwritten text from images, which can be useful for digitizing handwritten notes, forms, or documents.

## How to Use

1.  **Install Dependencies:**

    Before running the script, ensure you have the necessary libraries installed. You can install them using pip:

    ```bash
    pip install requests Pillow pandas openpyxl
    ```

2.  **API Key Setup:**

    Obtain an API key from the Bayer internal chat service and replace `"Your API"` with your actual API key in the script.

    ```python
    API_KEY = "Your API"
    ```

3.  **Prompt Configuration:**

    The script uses a prompt to guide the text extraction process. You can modify the `PROMPT` variable to suit your specific needs.

    ```python
    PROMPT = """
    # 手書き文字抽出・CSV化プロンプト（改良版）

    ## 背景・目的

    Workshopで「もっと職場をよくするには？」というテーマで参加者が書いた手書きの意見を、漏れなく正確に抽出してCSV形式で整理する。

    ## 実行手順

    ### 1. 画像解析の準備

    - 画像を明瞭に確認し、手書き文字の判読可能性を評価
    - 不鮮明な部分は「判読困難」として明記
    - 複数の意見が1枚に書かれている場合はすべて抽出

    ### 2. 文字読み取りの実行

    以下の順序で実行：
    1. **全体把握**：画像全体をスキャンし、書かれている項目数を把握
    2. **詳細読み取り**：各項目を個別に丁寧に読み取り
    3. **確認作業**：読み取り結果を再度画像と照合

    ### 3. カテゴリー分類基準

    以下の基準でカテゴリーを判定：
    - **コミュニケーション改善**：会話、情報共有、チームワーク関連
    - **業務効率化**：プロセス改善、ツール導入、時短関連
    - **職場環境**：物理環境、設備、レイアウト関連
    - **人事・制度**：評価制度、研修、福利厚生関連
    - **マネジメント**：リーダーシップ、意思決定、組織運営関連
    - **その他**：上記に該当しない項目

    ### 4. 出力要件

    #### CSV形式：

    ```
    ファイル名,カテゴリー,項目,補足情報
    ```

    #### 出力ルール：

    - **ファイル名**：画像ファイル名をそのまま記載
    - **カテゴリー**：上記6分類のいずれかを必ず選択
    - **項目**：読み取った手書き文字をそのまま記載（推測による補完は避ける）
    - **補足情報**：判読困難な文字、推測部分、特記事項を記載

    #### 品質確保のポイント：

    1. **完全性**：画像内のすべての文字を抽出（見落とし厳禁）
    2. **正確性**：推測ではなく読み取れる範囲で記載
    3. **一貫性**：カテゴリー分類基準を全画像で統一適用
    4. **透明性**：不明瞭な部分は「？」や「[判読困難]」で明記

    ## 処理完了後の確認事項

    - 抽出項目数が画像内の実際の項目数と一致しているか
    - カテゴリー分類に偏りや分類ミスがないか
    - 判読困難部分が適切にマークされているか

    ## エラー処理

    - 完全に判読不可能な画像：「画像不鮮明により抽出不可」と記載
    - 部分的に判読困難：読み取れる部分のみ抽出し、困難部分を明記
    """
    ```

4.  **Image Directory:**

    Specify the directory where your images are stored by updating the `image_directory` variable.

    ```python
    image_directory = "Directory where photos are saved."  # 画像が保存されているディレクトリ
    ```

5.  **Output File Path:**

    Define the output file path for the Excel file by updating the `output` variable.

    ```python
    output = "Output file path"
    ```

6.  **Run the Script:**

    Execute the script to process the images and extract the text.

    ```bash
    python your_script_name.py
    ```

## Dependencies

*   requests
*   Pillow (PIL)
*   pandas
*   openpyxl

You can install these dependencies using pip:

```bash
pip install requests Pillow pandas openpyxl
```

## API Key Information

The script requires an API key to access the handwriting recognition service. Ensure that you have a valid API key and that it is properly configured in the script.

## Input and Output File Formats

*   **Input:** The script accepts images in `.jpg`, `.jpeg`, `.png`, `.bmp`, and `.tiff` formats.
*   **Output:** The script produces two output files:
    *   `extracted_text.json`: A JSON file containing the extracted text and status for each image.
    *   `extracted_texts.xlsx`: An Excel file containing the extracted text for each image.

## Error Handling

The script includes error handling for API call failures, image encoding issues, and other potential problems. It prints error messages to the console and saves the status of each image in the JSON output file.
