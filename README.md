# FocusFlow - ADHD + Dyslexia-First Study App

**Capture lectures, recover what you missed, and study fast.**

FocusFlow is an AI-powered study companion designed specifically for students with ADHD and dyslexia. Upload your lecture recordings or documents, and we'll help you stay on track with smart transcription, gap recovery, and personalized study tools.

## ✨ Features

### 🎙️ Capture
- Upload audio/video lectures or documents (PDF, DOCX)
- Live recording with automatic transcription
- Searchable, editable transcript with timestamps

### 🧠 Recovery Mode
- Tap "I zoned out" to mark moments you missed
- AI generates bullet-point summaries of what you missed
- Understanding questions to check comprehension
- All content is **source-grounded** with citations

### 📚 Study Mode
- AI-generated summaries and key points
- Flashcard deck with spaced repetition
- Text-to-speech for all content
- Source links for every piece of AI-generated content

### ♿ Accessibility-First
- **Dyslexia Mode**: OpenDyslexic font, pastel backgrounds, extra spacing
- **Reading Ruler**: Visual guide that follows your reading
- **Large Touch Targets**: 44px minimum for all interactive elements
- **Reduced Motion**: Respects system preferences
- **TTS**: Read any content aloud

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- Docker & Docker Compose (for PostgreSQL + Redis)
- Azure account (optional, for full features)

### Installation

```bash
# Clone the repo
git clone https://github.com/yourusername/focusflow.git
cd focusflow

# Install dependencies
npm install

# Copy environment file
cp .env.example .env.local

# Start database services
docker-compose up -d

# Run database migrations
npx prisma migrate dev

# Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the app.

### Demo Mode

FocusFlow works without Azure credentials! In demo mode:
- Transcription uses pre-generated sample content
- AI outputs are simulated with realistic examples
- All features remain fully functional

## 🔧 Configuration

### Environment Variables

```env
# Database
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/focusflow"

# Redis
REDIS_URL="redis://localhost:6379"

# Auth (NextAuth)
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-secret-here"

# Email (for magic link auth)
EMAIL_SERVER="smtp://..."
EMAIL_FROM="noreply@focusflow.app"

# Azure (optional - enables full features)
AZURE_STORAGE_CONNECTION_STRING="..."
AZURE_SPEECH_KEY="..."
AZURE_SPEECH_REGION="eastus"
AZURE_OPENAI_ENDPOINT="..."
AZURE_OPENAI_KEY="..."
AZURE_OPENAI_DEPLOYMENT="gpt-4"
```

## 📁 Project Structure

```
src/
├── app/                    # Next.js App Router
│   ├── (app)/             # Authenticated routes
│   │   ├── dashboard/     # Session list
│   │   ├── sessions/      # Session viewer, recovery, study
│   │   └── settings/      # User preferences
│   ├── api/               # API routes
│   └── sign-in/           # Authentication
├── components/
│   ├── accessibility/     # Accessibility controls
│   ├── layout/            # App shell components
│   ├── session/           # Session-related components
│   └── ui/                # shadcn/ui components
├── lib/
│   ├── stores/            # Zustand state stores
│   ├── hooks/             # Custom React hooks
│   └── *.ts               # Utility modules
└── workers/               # BullMQ background workers
```

## 🧪 Testing

```bash
# Run unit tests
npm test

# Run with coverage
npm run test:coverage

# Run E2E tests
npm run test:e2e
```

## 🛠️ Tech Stack

- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS + shadcn/ui
- **Database**: PostgreSQL + Prisma
- **Cache/Queue**: Redis + BullMQ
- **Auth**: NextAuth.js (email magic link)
- **AI**: Azure OpenAI (GPT-4)
- **Speech**: Azure Cognitive Services (STT/TTS)
- **Storage**: Azure Blob Storage

## 📖 API Reference

### Sessions
- `POST /api/upload` - Upload files and create session
- `GET /api/sessions/:id` - Get session details
- `PATCH /api/sessions/:id/chunks/:chunkId` - Edit transcript chunk

### Markers
- `POST /api/sessions/:id/markers` - Create "zoned out" marker
- `GET /api/sessions/:id/markers` - List markers

### Flashcards
- `POST /api/sessions/:id/flashcards/:id/review` - Submit review

### Notes
- `GET /api/sessions/:id/notes` - Get notes
- `POST /api/sessions/:id/notes` - Save notes

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

## 🙏 Acknowledgments

- [OpenDyslexic](https://opendyslexic.org/) font
- [shadcn/ui](https://ui.shadcn.com/) components
- [Lexend](https://www.lexend.com/) font for improved readability
