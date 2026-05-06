# Configure the Model

AutoLXB needs an LLM / VLM endpoint compatible with the OpenAI Chat Completions style API. Visual execution and semantic route adaptation require **image understanding**.

## Entry

Open: `Config -> Device-side LLM Config`

Fill in:

- `API Base URL`
- `API Key`
- `Model`

The config page shows the final resolved request URL in real time, which helps you confirm whether the `/chat/completions` endpoint is correct.

## Test the model

After filling in the fields, tap the test button.

A successful test means:

- The app can reach the model service.
- The API key and model name are usable.
- The model can process image input.

!!! warning "Choose a model with image understanding"
    If the model only supports text, a basic connection test may pass, but visual execution, screen observation, and semantic adaptation will not work properly.
