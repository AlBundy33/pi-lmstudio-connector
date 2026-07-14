# LM Studio Provider

A specialized provider for the **Pi Coding Agent** that automates model discovery and registration from one or more LM Studio instances.

## 🎯 Purpose
Currently, models must be manually entered into a local `models.json` file to be usable by "pi". This project eliminates this manual step by providing an automated bridge:
1. It connects to one or more **LM Studio** instances.
2. It automatically fetches available models from those instances.
3. It registers them directly into the system, ensuring that `models.json` stays up-to-date without manual intervention.

## ✨ Key Features
- **Automated Registration**: No more manual editing of `models.json`.
- **Multi-Instance Support**: Connect to and aggregate models from multiple LM Studio instances simultaneously.
- **Seamless Integration**: Functions as a robust provider layer between LM Studio's API and the "pi" infrastructure.

## 🛠 Configuration
The configuration is handled via a JSON file which defines the connection details for your LM Studio instance(s).

**Configuration Path:** `~/.pi/agent/lmstudio-connector.json`

Example Configuration:
```json
[
  {
    "url": "http://my-ai-server:1234",
    "name": "lm-studio-server",
    "api_key": "some-api-key-12345"
  },
  {
    "url": "http://localhost:1234",
    "name": "local-lm-studio"
  }
]
```

## 🚀 Getting Started

### Setup
Ensure that your **LM Studio** instance has the "Local Server" enabled and is reachable from the host running this provider.

### LM Studio CLI Commands

**Start server (for remote access):**
```bash
lms server start --bind 0.0.0.0 --cors
```

**Load a model with GPU offload and context length:**
```bash
lms load <model_key> --gpu max --context-length 49152
```

Context length reference:
| Value | Tokens |
|-------|--------|
| 4k | 4096 |
| 8k | 8192 |
| 16k | 16384 |
| 32k | 32768 |
| 48k | 49152 |
| 64k | 65536 |
| 128k | 131072 |
| 256k | 262144 |

Other useful commands:
- `lms get <model>` — Download a model
- `lms ls` — List downloaded models
- `lms ps` — List loaded models
- `lms unload --all` — Unload all models

### Authentication (optional)

To enable authentication for the API server:
1. Open LM Studio GUI
2. Go to Developer → Server Settings
3. Enable "Require Authentication"
4. Create an API token under "Manage Tokens"

The token is passed as `Authorization: Bearer <token>` in API requests.

> **Note:** Authentication cannot be enabled via CLI. Use the GUI instead.

### Complete Example

```bash
# 1. Start server for remote access
lms server start --bind 0.0.0.0 --cors

# 2. Download a model
lms get google/gemma-4-e4b

# 3. Load the model with 48k context
lms load google/gemma-4-e4b --gpu max --context-length 49152

# 4. Verify loaded models
lms ps
```

### Usage
1. Configure your connection details in `~/.pi/agent/lmstudio-connector.json`.
2. Start the provider to begin the automatic synchronization of models into the system.

## 📜 License
This project is licensed under the [MIT License](LICENSE).

## 🤖 Development Note
This provider was created using AI-assisted coding. The implementation was carried out by [Pi](https://pi.dev) and [OpenCode](https://opencode.ai) based on the requirements described above.
