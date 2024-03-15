# Groq API Test with Rust

This Rust program demonstrates how to interact with the Groq API using the
Reqwest crate. It sends a chat completion request to the API and extracts the
response to display on the console.

For more information on Groq's functionality and some simple examples, refer to
the [Groq documentation](https://console.groq.com/docs/text-chat)

[Get Groq keys](https://console.groq.com/keys)

## Groq's rate limits for chat completions for each key issued:
- 30 requests per minute (RPM)
- 14,400 requests per day (RPD)
- 40,000 tokens per minute (TPM)

## Requirements

- Rust (https://www.rust-lang.org/tools/install)
- Cargo (Rust's package manager)
- An API key for the Groq API (set as `GROQ_API_KEY` environment variable)

## Installation

1. Clone the repository:

    ```bash
    git clone git@github.com:pramatias/groq_test.git
    ```

2. Navigate to the project directory:

    ```bash
    cd groq_test
    ```

3. Build and run the program:

    ```bash
    cargo build --release
    cargo run
    ```

## Usage

Before running the program, make sure you have set the `GROQ_API_KEY`
environment variable to your Groq API key.

The program sends a chat completion request to the Groq API with predefined
messages and parameters. It then extracts the response and prints it on the
console.

## Configuration

You can modify the following parameters in the `main()` function of `main.rs` to
customize the request:

Required
- `model`: The language model to use for generating completions.
- `messages`: An array of messages defining the conversation.

Optional
- `temperature`: Controls randomness in the completion.
- `max_tokens`: Maximum number of tokens to generate.
- `top_p`: Controls diversity via nucleus sampling.
- `stop`: A stop sequence to signal the AI to stop generating content.
- `stream`: Set to `true` if partial message deltas will be sent.

## Example Request

The program sends a chat completion request to the Groq API with the following parameters:

```json
{
    "model": "mixtral-8x7b-32768",
    "messages": [
        {
            "role": "system",
            "content": "you are a helpful assistant."
        },
        {
            "role": "user",
            "content": "Explain the importance of low latency LLMs"
        }
    ],
    "temperature": 0.5,
    "max_tokens": 1024,
    "top_p": 1,
    "stop": null,
    "stream": false
}

```
User's prompt is in: messages -> content

## Example Response

```json
{
    "id": "b9f7c6c6-1146-9616-bb82-bf16a0aec686",
    "object": "chat.completion",
    "created": 1710529128,
    "model": "mixtral-8x7b-32768",
    "choices": [
        {
            "index": 0,
            "message": {
                "role": "assistant",
                "content": "Low Latency Large Language Models (LLMs) are critical..."
            },
            "logprobs": null,
            "finish_reason": "stop"
        }
    ],
    "usage": {
        "prompt_tokens": 29,
        "prompt_time": 0.007,
        "completion_tokens": 282,
        "completion_time": 0.506,
        "total_tokens": 311,
        "total_time": 0.513
    },
    "system_fingerprint": null
}

```
LLM's response is in: choices -> message -> content
