# [Blog Generator with OpenAI and Python](blog_generator.py)

> A project from [Codedex](https://www.codedex.io/projects/generate-a-blog-with-openai).

A command-line blog generator that uses GPT-3 to write paragraphs on any topic you give it. Enter a topic, get a paragraph — repeat as many times as you want.

## Setup

**1. Install dependencies**

```bash
pip install openai python-dotenv
```

**2. Add your API key**

Create a `.env` file in the project root:

```
API_KEY=your_api_key_here
```

Get your key from [openai.com](https://www.openai.com). Keep it secret — don't commit `.env` to GitHub (add it to `.gitignore`).

**3. Run it**

```bash
python blog_generator.py
```

## How It Works

The core function sends a topic to OpenAI's `gpt-3.5-turbo-instruct` model and returns a generated paragraph:

```python
def generate_blog(paragraph_topic):
    response = openai.completions.create(
        model='gpt-3.5-turbo-instruct',
        prompt='Write a paragraph about the following topic. ' + paragraph_topic,
        max_tokens=400,
        temperature=0.3
    )
    return response.choices[0].text.strip()
```

A `while` loop then lets you keep generating paragraphs until you're done.

## Parameters

| Parameter | What it does |
|---|---|
| `model` | The GPT model to use |
| `prompt` | The instruction + your topic |
| `max_tokens` | Max response length (~400 tokens ≈ 1 paragraph) |
| `temperature` | Randomness: `0` = consistent, `1` = creative |
