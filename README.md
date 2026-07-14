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

**Configuration Path:** `~/.pi/agent/lmstudio-connector.json` (or as defined in your environment)

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

### Usage
1. Configure your connection details in `lmstudio-connector.json`.
2. Start the provider to begin the automatic synchronization of models into the system.

## 📜 License
This project is licensed under the [MIT License](LICENSE).

## 🤖 Development Note
This provider was created using AI-assisted coding. The implementation was carried out by [Pi](https://pi.dev) and [OpenCode](https://opencode.ai) based on the requirements described above.
