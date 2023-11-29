# Gorilla-Interaction-API
A Flask-based API for interacting with the open-source [Gorilla Large Language Model](https://github.com/ShishirPatil/gorilla) (LLM) for function calling. The sample code illustrates the creation of local and self-hosted applications with Gorilla, utilizing function calling similar to that of [OpenAI's Function Calling](https://js.langchain.com/docs/modules/model_io/models/chat/how_to/function_calling).

# Setup

1. Clone [gorilla-openfunctions-v0](https://huggingface.co/gorilla-llm/gorilla-openfunctions-v0):
```bash
git lfs install
git clone https://huggingface.co/gorilla-llm/gorilla-openfunctions-v0
```
2. Place the model in the `model` directory
3. Install `requirements.txt`:
```bash
pip install -r requirements.txt
```
4. Run Flask application:
```bash
python3 app.py
```

# Example run
### Input
Given user query:
```python
query: str = "I need to react with three words, word wow, word test, word acting"
```

With schema:
```python
functions = [
            {
                "name": "React",
                "api_name": "functioncall_react",
                "description": "Find three words from the sentence",
                "parameters":  [
                    {"name": "word1", "description": "A word"},
                    {"name": "word2", "description": "A word"},
                    {"name": "word3", "description": "A word"}
                ]
            }
        ]
```

Using GET for the `/act` endpoint:
```json
{
    "function_calls": {
        "api_name": "functioncall_react",
        "parameters": {
            "word1": "\"wow\"",
            "word2": "\"test\"",
            "word3": "\"acting\""
        }
    },
    "response": "Success at acting!"
}
```

### Output
From server side `/react` endpoint:
```python
Generated function_call: functioncall_react(word1="wow", word2="test", word3="acting")
Successful at reacting! Received function call: {
                                            'api_name': 'functioncall_react', 
                                            'parameters': {
                                                'word1': '"wow"',
                                                'word2': '"test"',
                                                'word3': '"acting"'
                                                }
                                            }
```
