# Bonktah 🤖🚀

<div align="center">
  <img src="https://github.com/user-attachments/assets/77c69295-9355-4c90-a470-77d6e5742ff4" alt="Bonktah Banner" width="100%" />
</div>

<div align="center">

📖 [Documentation](https://bonktah.xyz/framework.html) | 🧠 [Conscience](https://bonktah.xyz/bonktah-conscience.html) | 🔌 [API Integration](https://bonktah.xyz/bonktah-integration.html) | 🎯 [Live Demo](https://bonktah.xyz)

</div>

## 🚩 Overview

Bonktah is a meme-savvy AI companion built as an extensible addon layer on top of ElizaOS. Where AI meets meme culture in perfect harmony - bringing personality, humor, and crypto knowledge to autonomous AI agents.

## ✨ Features

- 🤖 **Meme-Aware AI** - Deep understanding of crypto culture, memes, and internet trends
- 🧠 **Conscience System** - Community-driven conversation storage with upvoting
- 🔗 **Built on ElizaOS** - Leverages proven AI framework foundations
- 💬 **Multi-Platform** - Discord, Twitter, Telegram, and web interface support
- 📚 **Memory Management** - Persistent conversation context and personality
- 🎨 **Glassmorphism UI** - Beautiful, modern web interface with real-time chat
- 🚀 **Extensible Plugins** - Create custom actions and integrations
- 📦 **Easy Deployment** - Docker-ready with one-click setup options

## 🎯 Use Cases

- 🎭 Entertainment chatbot with personality
- 💰 Crypto community engagement
- 🎮 Interactive meme creation
- 📈 Market sentiment analysis
- 🧠 Creative writing assistance
- 🤝 Community moderation

## 🚀 Quick Start

### Prerequisites

- [Node.js 23+](https://nodejs.org/)
- [pnpm](https://pnpm.io/installation)
- [Docker](https://www.docker.com/) (optional)
- [PostgreSQL](https://www.postgresql.org/) (for Conscience feature)

### Installation

```bash
# Clone the repository
git clone https://github.com/bonktah/bonktah.git
cd bonktah

# Copy environment variables
cp .env.example .env

# Install dependencies
pnpm install

# Build the project
pnpm build

# Start Bonktah
pnpm start
```

### Environment Configuration

Edit `.env` with your API keys:

```env
# Required
ANTHROPIC_API_KEY=your_anthropic_key
DATABASE_URL=postgresql://user:password@localhost:5432/bonktah

# Optional
OPENAI_API_KEY=your_openai_key
DISCORD_TOKEN=your_discord_token
TWITTER_API_KEY=your_twitter_key
```

### Docker Deployment

```bash
# Build and run with Docker Compose
docker-compose up -d

# View logs
docker-compose logs -f bonktah-eliza
```

## 🏗️ Architecture

Bonktah extends ElizaOS with custom plugins and personality modules:

```typescript
// Custom Bonktah Character Configuration
export const bonktahCharacter: Character = {
  name: "Bonktah",
  username: "bonktah",
  bio: [
    "A meme-savvy AI with deep knowledge of crypto culture",
    "Balances serious AI capabilities with humor and relatability"
  ],
  topics: ["cryptocurrency", "meme culture", "defi", "life advice"],
  style: {
    all: [
      "Uses crypto/meme references naturally",
      "Balances technical knowledge with approachability",
      "Occasionally uses emojis appropriately"
    ]
  },
  plugins: [consciencePlugin, memeCulturePlugin, cryptoKnowledgePlugin]
};
```

## 📚 Core Components

### Conscience System

Store and retrieve high-quality conversations with community voting:

```typescript
// Conscience Plugin
export const consciencePlugin: Plugin = {
  name: "conscience",
  description: "Stores and retrieves conversation history with voting",
  
  actions: [{
    name: "STORE_CONVERSATION",
    handler: async (runtime: IAgentRuntime, memory: Memory) => {
      const conversation = await formatConversation(memory);
      await database.conversations.create({
        id: generateId(),
        timestamp: new Date(),
        messages: conversation.messages,
        upvotes: 0,
        category: await categorizeConversation(conversation)
      });
      return true;
    }
  }]
};
```

### API Integration

RESTful API for chat and conscience access:

```typescript
// Chat Endpoint
POST /api/v1/chat
{
  "message": "Hey Bonktah, what's your take on meme coins?",
  "userId": "user_12345",
  "sessionId": "session_abc123",
  "options": {
    "temperature": 0.8,
    "saveToConscience": true
  }
}

// Response
{
  "response": "Meme coins are the wild west of crypto! 🤠",
  "messageId": "msg_789xyz",
  "sentiment": "positive",
  "topics": ["crypto", "meme-coins"]
}
```

## 📁 Project Structure

```
bonktah/
├── packages/
│   ├── core/           # Extended ElizaOS core
│   ├── plugins/        # Custom Bonktah plugins
│   │   ├── conscience/ # Conversation storage system
│   │   ├── meme/      # Meme culture understanding
│   │   └── crypto/    # Crypto knowledge base
│   ├── frontend/      # React glassmorphism UI
│   └── api/          # REST API endpoints
├── characters/       # Character definitions
├── docs/            # Documentation
├── docker/          # Docker configurations
└── scripts/         # Utility scripts
```

## 🛠️ Development

### Creating Custom Plugins

```typescript
// Example: Meme Generator Plugin
export const memeGeneratorPlugin: Plugin = {
  name: "meme-generator",
  description: "Generates contextual memes",
  
  actions: [{
    name: "GENERATE_MEME",
    similes: ["make a meme", "create meme", "meme this"],
    
    handler: async (runtime, memory, state, message) => {
      const context = extractContext(message);
      const memeTemplate = selectTemplate(context);
      const memeText = generateMemeText(context, runtime.character);
      
      return {
        text: `Here's your meme: ${memeText} 😂`,
        media: await createMemeImage(memeTemplate, memeText)
      };
    }
  }]
};
```

### Frontend Customization

The glassmorphism UI can be customized in `packages/frontend/src/styles`:

```css
:root {
  --primary-gradient: linear-gradient(135deg, #ff7b00 0%, #ff9500 50%, #ffb366 100%);
  --glass-bg: rgba(255, 255, 255, 0.08);
  --glass-border: rgba(255, 255, 255, 0.15);
}
```

## 🔌 API Reference

### Authentication
```http
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

### Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/chat` | Send message to Bonktah |
| GET | `/api/v1/conscience` | Retrieve conversations |
| POST | `/api/v1/conscience/upvote` | Upvote conversation |
| POST | `/api/v1/webhooks/register` | Register webhook |

### Rate Limits
- Chat API: 60 requests/minute
- Conscience API: 100 requests/minute
- Webhook Registration: 10 requests/hour

## 🤝 Contributing

We welcome contributions! See our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

```bash
# Fork and clone
git clone https://github.com/YOUR_USERNAME/bonktah.git
cd bonktah

# Create feature branch
git checkout -b feature/your-feature

# Install and test
pnpm install
pnpm test

# Submit PR
```

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🌟 Acknowledgments

Built on top of [ElizaOS](https://github.com/elizaos/eliza) - the open-source AI agent framework.

## 📊 Stats

[![Star History Chart](https://api.star-history.com/svg?repos=bonktah/bonktah&type=Date)](https://star-history.com/#bonktah/bonktah&Date)

## 💬 Community & Support

- [Website](https://bonktah.xyz/) - Our website
- [Twitter](https://twitter.com/bonktah) - Follow for updates
- [GitHub Issues](https://github.com/bonktah/bonktah/issues) - Report bugs

---

<div align="center">
  Made with 🧡 by the Bonktah community
</div>
