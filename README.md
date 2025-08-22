# MemoriasDev — Portfolio
## Prepared for Gauntlet AI - Cohort 3 Application 
### [In-Progress!]


A curated index of my featured projects with CARL summaries (Context, Action, Result, Learning).

## Projects

* **Module-Mind** — Open-source video-to-course transformation platform  
  * Repo: https://github.com/MemoriasDev/module-mind-open  
  * Live: [Demo Coming Soon]  
  * Type: Open Source Template & SaaS Foundation

* **AI Academy** — Video → Course generation pipeline  
  * Repo: https://github.com/MemoriasDev/ai-academy  
  * Live: https://ai-academy-rouge.vercel.app/  
  * Type: Proprietary Implementation

---

## Module-Mind (CARL)

### Context

Educational videos are everywhere but lack structure—making them hard to navigate, search, and study effectively. Hours of valuable content remain buried in linear formats without timestamps, searchable transcripts, or interactive elements. Traditional video platforms don't extract the rich educational context that could transform passive viewing into active learning.

### Action

Built **Module-Mind**, an open-source platform that automatically transforms any video into a structured, interactive course. The system features:

- **AI-powered transcription** using OpenAI Whisper for 99%+ accuracy
- **Content extraction** that identifies learning objectives, code examples, and key concepts
- **Smart timestamping** for precise video navigation and topic jumping
- **React/TypeScript frontend** with mobile-responsive design and progress tracking
- **Supabase backend** for authentication, secure video storage, and user management
- **Quality assurance pipeline** ensuring 93.8/100 average course quality scores
- **Authentication toggle** (`VITE_ENABLE_AUTH`) supporting both quick demos and production deployment

### Result

Delivered a complete video-to-course transformation ecosystem:

- **Clean open-source template** ready for community contributions and commercial use
- **Multiple video sources** supporting YouTube, Supabase Storage, and local files
- **Interactive learning experience** with clickable timestamps and progress tracking
- **Comprehensive documentation** including setup guides, deployment instructions, and architecture docs
- **Enterprise-ready features** including role-based access and video protection
- **Reusable processing pipeline** that can handle any video format or source

The platform demonstrates converting 22+ hours of technical content into structured courses with automated quality validation and interactive navigation.

### Learning

Validated that AI can unlock hidden value in existing video content, creating scalable opportunities across multiple domains:

- **Educational content creators** can enhance video libraries without manual restructuring
- **Corporate training teams** can transform recorded sessions into structured onboarding materials
- **Technical educators** can automatically extract code examples and create interactive programming courses
- **Content marketers** can repurpose webinars into professional course experiences

The project established a reusable "video → structured learning" pipeline that demonstrates how AI-native tools can create new business models from existing content while building open-source infrastructure for the broader education technology ecosystem.

**Tech Stack:** React, TypeScript, Tailwind CSS, Supabase, OpenAI Whisper, Python, Vercel

---

## AI Academy (CARL)

### Context

I received the Aitra Legacy Courses as raw video. Goal: transform passive, hard-to-navigate content into a modern learning experience that surfaces key ideas and enables structured study.

### Action

Built a React + Supabase platform and used OpenAI Whisper to transcribe long-form videos. Added workflows to convert transcripts into structured courses—timestamped navigation, summaries, and interactive lessons—demonstrating a repeatable "video → course" pipeline.

### Result

Shipped AI Academy featuring the full Cohort 2 curriculum (22 lessons across 9 weeks). The repo also illustrates a reusable pipeline (via Module-Mind) for converting legacy video libraries into interactive courses—suitable as an open-source tool, an MVP agency service, or a SaaS foundation.

### Learning

Beyond mastering transcription + structure + platform design, I validated that AI can productize static video into new workflows and business models (video → structured learning). This originated as a personal Gauntlet 2 challenge to sharpen AI-native builder skills.

---

More projects and deep dives coming soon.
