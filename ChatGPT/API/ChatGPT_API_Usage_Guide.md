
# ChatGPT API 利用開始手順

## 1. OpenAIの公式サイトにアクセス
[OpenAI公式サイト](https://platform.openai.com/)にアクセスします。

## 2. OpenAIアカウントにサインアップ／ログイン
- すでにOpenAIアカウントをお持ちであればログインしてください。アカウントを持っていない場合は、サインアップしてアカウントを作成してください。



## 3. APIキーを取得
- ログイン後、OpenAIの「Dashboard」に移動します。
- 「API」セクションに進み、**API Keys**の項目を探します。見つからない場合、トップバーの「Personal」メニューを展開し、「API Keys」というオプションがあります。
- 「Create new secret key」ボタンをクリックして、APIキーを生成します。このキーは一度しか表示されないため、必ず安全な場所に保存してください。

以下Developer quickstart(202409081416時点)に従うこと。

[# Developer quickstart](https://platform.openai.com/docs/quickstart/developer-quickstart)

## Create and export an API key


[Create an API key in the dashboard here](https://platform.openai.com/api-keys), which you’ll use to securely [access the API](https://platform.openai.com/docs/api-reference/authentication). Store the key in a safe location, like a [`.zshrc` file](https://www.freecodecamp.org/news/how-do-zsh-configuration-files-work/) or another text file on your computer. Once you’ve generated an API key, export it as an [environment variable](https://en.wikipedia.org/wiki/Environment_variable) in your terminal.

Windows
Export an envrionment variable in PowerShell
```bash
1
setx OPENAI_API_KEY "your_api_key_here"
```

## Make your first API request

With your OpenAI API key exported as an environment variable, you're ready to make your first API request. You can either use the [REST API](https://platform.openai.com/docs/api-reference) directly with the HTTP client of your choice, or use one of our [official SDKs](https://platform.openai.com/docs/libraries) as shown below.

Python

To use the OpenAI API in Python, you can use the official [OpenAI SDK for Python](https://github.com/openai/openai-python). Get started by installing the SDK using [pip](https://pypi.org/project/pip/):

Install the OpenAI SDK with pip

```bash
1
pip install openai
```

With the OpenAI SDK installed, create a file called `example.py` and copy one of the following examples into it:

Generate text
Create a human-like response to a prompt

```python
from openai import OpenAI
client = OpenAI()

completion = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {
            "role": "user",
            "content": "Write a haiku about recursion in programming."
        }
    ]
)

print(completion.choices[0].message)
```

Execute the code with `python example.py`. In a few moments, you should see the output of your API request!

## 5. 利用制限と料金について確認
APIの利用には制限があります。ダッシュボード内の「Usage」タブで、現在の使用量や料金プランを確認することができます。

参考：
https://chatgpt-enterprise.jp/blog/api-cost/

## 6. APIドキュメントを参照
より詳細な使い方は、OpenAIの公式APIドキュメント（[API Reference](https://platform.openai.com/docs)）を参照してください。

