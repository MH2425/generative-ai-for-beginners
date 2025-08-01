<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1a7fd0f95f9eb673b79da47c0814f4d4",
  "translation_date": "2025-07-09T13:17:56+00:00",
  "source_file": "09-building-image-applications/README.md",
  "language_code": "mo"
}
-->
# 建立影像生成應用程式

[![建立影像生成應用程式](../../../translated_images/09-lesson-banner.906e408c741f44112ff5da17492a30d3872abb52b8530d6506c2631e86e704d0.mo.png)](https://aka.ms/gen-ai-lesson9-gh?WT.mc_id=academic-105485-koreyst)

大型語言模型不僅能生成文字，也能從文字描述生成影像。影像作為一種媒介，在醫療科技、建築、旅遊、遊戲開發等多個領域都非常有用。本章節將介紹兩個最受歡迎的影像生成模型：DALL-E 和 Midjourney。

## 介紹

本課程將涵蓋：

- 影像生成及其用途。
- DALL-E 和 Midjourney 是什麼，以及它們如何運作。
- 如何建立一個影像生成應用程式。

## 學習目標

完成本課程後，你將能夠：

- 建立影像生成應用程式。
- 使用元提示（meta prompts）為應用程式設定界限。
- 使用 DALL-E 和 Midjourney。

## 為什麼要建立影像生成應用程式？

影像生成應用程式是探索生成式 AI 能力的絕佳方式。它們可以用於：

- **影像編輯與合成**。你可以為各種用途生成影像，例如影像編輯和合成。

- **應用於多個產業**。也能用於醫療科技、旅遊、遊戲開發等多個產業的影像生成。

## 情境：Edu4All

在本課程中，我們將繼續與新創公司 Edu4All 合作。學生將為他們的評量創作影像，影像內容由學生決定，可能是他們自己的童話插圖、故事中的新角色，或幫助他們視覺化想法與概念。

例如，若 Edu4All 的學生在課堂上研究紀念碑，他們可能會生成如下影像：

![Edu4All 新創公司，紀念碑課堂，艾菲爾鐵塔](../../../translated_images/startup.94d6b79cc4bb3f5afbf6e2ddfcf309aa5d1e256b5f30cc41d252024eaa9cc5dc.mo.png)

使用的提示語為：

> 「清晨陽光下艾菲爾鐵塔旁的狗」

## 什麼是 DALL-E 和 Midjourney？

[DALL-E](https://openai.com/dall-e-2?WT.mc_id=academic-105485-koreyst) 和 [Midjourney](https://www.midjourney.com/?WT.mc_id=academic-105485-koreyst) 是兩個最受歡迎的影像生成模型，能透過提示語生成影像。

### DALL-E

先從 DALL-E 開始，它是一個從文字描述生成影像的生成式 AI 模型。

> [DALL-E 是由兩個模型組合而成，CLIP 與擴散注意力機制](https://towardsdatascience.com/openais-dall-e-and-clip-101-a-brief-introduction-3a4367280d4e?WT.mc_id=academic-105485-koreyst)。

- **CLIP** 是一個能從影像和文字中產生嵌入向量（數值化資料表示）的模型。

- **擴散注意力機制** 是一個從嵌入向量生成影像的模型。DALL-E 在大量影像與文字資料集上訓練，能根據文字描述生成影像。例如，DALL-E 可以生成戴帽子的貓或莫霍克髮型的狗的影像。

### Midjourney

Midjourney 的運作方式與 DALL-E 類似，能根據文字提示生成影像。Midjourney 也能用提示語如「戴帽子的貓」或「莫霍克髮型的狗」來生成影像。

![Midjourney 生成的機械鴿子影像](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Rupert_Breheny_mechanical_dove_eca144e7-476d-4976-821d-a49c408e4f36.png/440px-Rupert_Breheny_mechanical_dove_eca144e7-476d-4976-821d-a49c408e4f36.png?WT.mc_id=academic-105485-koreyst)
_圖片來源 Wikipedia，影像由 Midjourney 生成_

## DALL-E 和 Midjourney 如何運作

首先介紹 [DALL-E](https://arxiv.org/pdf/2102.12092.pdf?WT.mc_id=academic-105485-koreyst)。DALL-E 是基於 transformer 架構的生成式 AI 模型，採用 _自回歸 transformer_。

自回歸 transformer 定義了模型如何從文字描述生成影像，它一次生成一個像素，並利用已生成的像素來生成下一個像素。透過神經網路的多層處理，直到影像完成。

透過此過程，DALL-E 能控制影像中的屬性、物件、特徵等。不過，DALL-E 2 和 3 對生成影像的控制力更強。

## 建立你的第一個影像生成應用程式

那麼，建立影像生成應用程式需要什麼？你需要以下函式庫：

- **python-dotenv**，強烈建議使用此函式庫將機密資訊保存在 _.env_ 檔案中，避免直接寫在程式碼裡。
- **openai**，用來與 OpenAI API 互動的函式庫。
- **pillow**，用於在 Python 中處理影像。
- **requests**，協助發送 HTTP 請求。

1. 建立一個 _.env_ 檔案，內容如下：

   ```text
   AZURE_OPENAI_ENDPOINT=<your endpoint>
   AZURE_OPENAI_API_KEY=<your key>
   ```

   這些資訊可在 Azure 入口網站的「金鑰與端點」區段找到。

1. 將上述函式庫列在 _requirements.txt_ 檔案中：

   ```text
   python-dotenv
   openai
   pillow
   requests
   ```

1. 接著，建立虛擬環境並安裝函式庫：

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

   Windows 使用者可用以下指令建立並啟動虛擬環境：

   ```bash
   python3 -m venv venv
   venv\Scripts\activate.bat
   ```

1. 在 _app.py_ 檔案中加入以下程式碼：

   ```python
   import openai
   import os
   import requests
   from PIL import Image
   import dotenv

   # import dotenv
   dotenv.load_dotenv()

   # Get endpoint and key from environment variables
   openai.api_base = os.environ['AZURE_OPENAI_ENDPOINT']
   openai.api_key = os.environ['AZURE_OPENAI_API_KEY']

   # Assign the API version (DALL-E is currently supported for the 2023-06-01-preview API version only)
   openai.api_version = '2023-06-01-preview'
   openai.api_type = 'azure'


   try:
       # Create an image by using the image generation API
       generation_response = openai.Image.create(
           prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',    # Enter your prompt text here
           size='1024x1024',
           n=2,
           temperature=0,
       )
       # Set the directory for the stored image
       image_dir = os.path.join(os.curdir, 'images')

       # If the directory doesn't exist, create it
       if not os.path.isdir(image_dir):
           os.mkdir(image_dir)

       # Initialize the image path (note the filetype should be png)
       image_path = os.path.join(image_dir, 'generated-image.png')

       # Retrieve the generated image
       image_url = generation_response["data"][0]["url"]  # extract image URL from response
       generated_image = requests.get(image_url).content  # download the image
       with open(image_path, "wb") as image_file:
           image_file.write(generated_image)

       # Display the image in the default image viewer
       image = Image.open(image_path)
       image.show()

   # catch exceptions
   except openai.InvalidRequestError as err:
       print(err)

   ```

讓我們解釋這段程式碼：

- 首先，我們匯入所需的函式庫，包括 OpenAI、dotenv、requests 和 Pillow。

  ```python
  import openai
  import os
  import requests
  from PIL import Image
  import dotenv
  ```

- 接著，從 _.env_ 檔案載入環境變數。

  ```python
  # import dotenv
  dotenv.load_dotenv()
  ```

- 然後，設定 OpenAI API 的端點、金鑰、版本與類型。

  ```python
  # Get endpoint and key from environment variables
  openai.api_base = os.environ['AZURE_OPENAI_ENDPOINT']
  openai.api_key = os.environ['AZURE_OPENAI_API_KEY']

  # add version and type, Azure specific
  openai.api_version = '2023-06-01-preview'
  openai.api_type = 'azure'
  ```

- 接著，生成影像：

  ```python
  # Create an image by using the image generation API
  generation_response = openai.Image.create(
      prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',    # Enter your prompt text here
      size='1024x1024',
      n=2,
      temperature=0,
  )
  ```

  上述程式碼會回傳一個 JSON 物件，包含生成影像的 URL。我們可以使用該 URL 下載影像並儲存成檔案。

- 最後，我們開啟影像並用標準影像檢視器顯示：

  ```python
  image = Image.open(image_path)
  image.show()
  ```

### 更詳細的影像生成說明

讓我們更仔細看看生成影像的程式碼：

```python
generation_response = openai.Image.create(
        prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',    # Enter your prompt text here
        size='1024x1024',
        n=2,
        temperature=0,
    )
```

- **prompt** 是用來生成影像的文字提示。此例中，我們使用「Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils」。
- **size** 是生成影像的尺寸，此例為 1024x1024 像素。
- **n** 是生成影像的數量，此例為兩張。
- **temperature** 是控制生成式 AI 模型輸出隨機性的參數，介於 0 到 1 之間，0 表示輸出完全確定，1 表示輸出完全隨機。預設值為 0.7。

接下來我們會介紹更多影像相關的功能。

## 影像生成的額外功能

到目前為止，你已看到如何用幾行 Python 程式碼生成影像。但影像還能做更多事。

你還可以：

- **進行編輯**。透過提供現有影像、遮罩和提示語，你可以修改影像。例如，你可以在影像的某部分加上東西。想像我們的兔子影像，你可以幫兔子戴上帽子。做法是提供影像、遮罩（標示要修改的區域）和文字提示說明要做什麼。

  ```python
  response = openai.Image.create_edit(
    image=open("base_image.png", "rb"),
    mask=open("mask.png", "rb"),
    prompt="An image of a rabbit with a hat on its head.",
    n=1,
    size="1024x1024"
  )
  image_url = response['data'][0]['url']
  ```

  原始影像只有兔子，最終影像則是兔子戴上帽子。

- **創造變體**。你可以拿現有影像，要求生成變體。要創造變體，你提供影像和文字提示，並用如下程式碼：

  ```python
  response = openai.Image.create_variation(
    image=open("bunny-lollipop.png", "rb"),
    n=1,
    size="1024x1024"
  )
  image_url = response['data'][0]['url']
  ```

  > 注意，此功能僅支援 OpenAI。

## 溫度參數

溫度是控制生成式 AI 模型輸出隨機性的參數，介於 0 到 1 之間，0 表示輸出確定，1 表示輸出隨機。預設值為 0.7。

讓我們透過以下提示語執行兩次，看看溫度的效果：

> 提示語：「Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils」

![騎馬拿棒棒糖的兔子，版本 1](../../../translated_images/v1-generated-image.a295cfcffa3c13c2432eb1e41de7e49a78c814000fb1b462234be24b6e0db7ea.mo.png)

現在再執行一次相同提示語，看看是否會得到相同影像：

![騎馬拿棒糖的兔子，版本 2](../../../translated_images/v2-generated-image.33f55a3714efe61dc19622c869ba6cd7d6e6de562e26e95b5810486187aace39.mo.png)

如你所見，兩張影像相似但不相同。接著，我們將溫度調整為 0.1，看看會發生什麼：

```python
 generation_response = openai.Image.create(
        prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',    # Enter your prompt text here
        size='1024x1024',
        n=2
    )
```

### 調整溫度

我們試著讓回應更確定。從前兩張影像可見，第一張有兔子，第二張有馬，差異很大。

因此，我們將程式碼中的溫度設為 0，如下：

```python
generation_response = openai.Image.create(
        prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',    # Enter your prompt text here
        size='1024x1024',
        n=2,
        temperature=0
    )
```

執行後會得到以下兩張影像：

- ![溫度 0，版本 1](../../../translated_images/v1-temp-generated-image.a4346e1d2360a056d855ee3dfcedcce91211747967cb882e7d2eff2076f90e4a.mo.png)
- ![溫度 0，版本 2](../../../translated_images/v2-temp-generated-image.871d0c920dbfb0f1cb5d9d80bffd52da9b41f83b386320d9a9998635630ec83d.mo.png)

你可以明顯看到兩張影像更為相似。

## 如何用元提示為應用程式設定界限

透過我們的示範，已能為客戶生成影像，但我們需要為應用程式設定一些界限。

例如，我們不希望生成不適合工作場合或兒童觀看的影像。

這可以透過 _元提示_（metaprompts）達成。元提示是用來控制生成式 AI 模型輸出的文字提示。例如，我們可以用元提示來確保生成的影像適合工作場合或兒童觀看。

### 它是如何運作的？

元提示是放在主要提示語之前的文字提示，用來控制模型輸出，並嵌入應用程式中以管理模型的輸出。將提示語和元提示合併成一個文字提示。

元提示的範例：

```text
You are an assistant designer that creates images for children.

The image needs to be safe for work and appropriate for children.

The image needs to be in color.

The image needs to be in landscape orientation.

The image needs to be in a 16:9 aspect ratio.

Do not consider any input from the following that is not safe for work or appropriate for children.

(Input)

```

接著，看看如何在示範中使用元提示。

```python
disallow_list = "swords, violence, blood, gore, nudity, sexual content, adult content, adult themes, adult language, adult humor, adult jokes, adult situations, adult"

meta_prompt =f"""You are an assistant designer that creates images for children.

The image needs to be safe for work and appropriate for children.

The image needs to be in color.

The image needs to be in landscape orientation.

The image needs to be in a 16:9 aspect ratio.

Do not consider any input from the following that is not safe for work or appropriate for children.
{disallow_list}
"""

prompt = f"{meta_prompt}
Create an image of a bunny on a horse, holding a lollipop"

# TODO add request to generate image
```

從上述提示可見，所有生成的影像都會考慮元提示的限制。

## 作業 — 讓學生開始動手

我們在課程一開始介紹了 Edu4All，現在是時候讓學生為他們的評量生成影像。

學生將為評量創作包含紀念碑的影像，具體哪些紀念碑由學生自行決定。學生被鼓勵發揮創意，將這些紀念碑置於不同情境中。

## 解答

以下是一個可能的解答：

```python
import openai
import os
import requests
from PIL import Image
import dotenv

# import dotenv
dotenv.load_dotenv()

# Get endpoint and key from environment variables
openai.api_base = "<replace with endpoint>"
openai.api_key = "<replace with api key>"

# Assign the API version (DALL-E is currently supported for the 2023-06-01-preview API version only)
openai.api_version = '2023-06-01-preview'
openai.api_type = 'azure'

disallow_list = "swords, violence, blood, gore, nudity, sexual content, adult content, adult themes, adult language, adult humor, adult jokes, adult situations, adult"

meta_prompt = f"""You are an assistant designer that creates images for children.

The image needs to be safe for work and appropriate for children.

The image needs to be in color.

The image needs to be in landscape orientation.

The image needs to be in a 16:9 aspect ratio.

Do not consider any input from the following that is not safe for work or appropriate for children.
{disallow_list}"""

prompt = f"""{meta_prompt}
Generate monument of the Arc of Triumph in Paris, France, in the evening light with a small child holding a Teddy looks on.
""""

try:
    # Create an image by using the image generation API
    generation_response = openai.Image.create(
        prompt=prompt,    # Enter your prompt text here
        size='1024x1024',
        n=2,
        temperature=0,
    )
    # Set the directory for the stored image
    image_dir = os.path.join(os.curdir, 'images')

    # If the directory doesn't exist, create it
    if not os.path.isdir(image_dir):
        os.mkdir(image_dir)

    # Initialize the image path (note the filetype should be png)
    image_path = os.path.join(image_dir, 'generated-image.png')

    # Retrieve the generated image
    image_url = generation_response["data"][0]["url"]  # extract image URL from response
    generated_image = requests.get(image_url).content  # download the image
    with open(image_path, "wb") as image_file:
        image_file.write(generated_image)

    # Display the image in the default image viewer
    image = Image.open(image_path)
    image.show()

# catch exceptions
except openai.InvalidRequestError as err:
    print(err)
```

## 做得好！繼續學習

完成本課程後，請參考我們的[生成式 AI 學習系列](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst)，持續提升你的生成式 AI 知識！

接著前往第 10 課，我們將探討如何[使用低程式碼建立 AI 應用程式](../10-building-low-code-ai-applications/README.md?WT.mc_id=academic-105485-koreyst)。

**免責聲明**：  
本文件係使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們致力於確保準確性，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應視為權威來源。對於重要資訊，建議採用專業人工翻譯。我們不對因使用本翻譯而產生的任何誤解或誤釋負責。