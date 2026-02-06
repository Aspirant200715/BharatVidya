# BharatVidya 🇮🇳

**Transforming Rural Education Through Offline-First AI**

> An offline-first, AI-powered educational platform that converts text (NCERT, Wikipedia) into 2-minute regional language video lessons for rural India. Works on 2GB RAM devices with 2G networks at 33x lower cost than competitors.

---

## 📋 Table of Contents

- [Problem Statement](#-problem-statement)
- [Solution Overview](#-solution-overview)
- [Key Features](#-key-features)
- [Technical Architecture](#-technical-architecture)
- [User Journeys](#-user-journeys)
- [Performance Targets](#-performance-targets)
- [Competitive Advantages](#-competitive-advantages)

---

## 🎯 Problem Statement

### The Rural Education Crisis

**60% of rural educators** face persistent network connectivity issues, and students lose **3-4 hours daily** switching between networks to access educational content.

### Market Gap

| Platform | Issue | Cost | Connectivity |
|----------|-------|------|--------------|
| **DIKSHA** | 30% usability issues | Free (high data) | 3G/4G required |
| **Byju's** | Not optimized for low-end devices | ₹3,000+/year | 4G dependent |
| **Khan Academy** | English-only, no regional support | Free (high data) | Stable broadband |
| **Unacademy** | Live classes need real-time connectivity | ₹2,500+/year | 4G required |

### Our Solution

**BharatVidya** addresses the intersection of:
- ✅ Ultra-low connectivity (2G networks)
- ✅ Ultra-low-cost devices (2GB RAM, Snapdragon 4xx)
- ✅ Regional language support (12+ Indian languages)
- ✅ Offline-first architecture with intelligent sync
- ✅ Teacher content creation without technical skills

---

## 💡 Solution Overview

BharatVidya is an **offline-first educational video generation platform** designed specifically for rural India:

### Value Proposition

- **33x Cheaper**: ₹89/year vs ₹3,000+ for competitors
- **Works on 2G**: Offline-first design with < 2KB sync operations
- **2GB RAM Optimized**: Runs smoothly on entry-level devices
- **12+ Languages**: Hindi, Tamil, Telugu, Marathi, Bengali, and more
- **5-Minute Video Creation**: Teachers create content without editing skills
- **45MB Initial Install**: Entire app functionality after minimal download

---

## ✨ Key Features

### For Students

#### 🔌 Offline-First Learning
- **100% functionality** after 45MB initial install
- Watch lessons without internet connectivity
- Local quiz completion with automatic sync
- Progress tracking works offline

#### 📱 Smart Synchronization
- **< 2KB** progress updates (less than a WhatsApp text)
- Auto-sync on WiFi detection
- Background sync during "cheap data" windows (2 AM)
- 70% payload reduction through Brotli compression

#### 🌐 Multilingual Support
- Content in **12+ regional languages**
- Natural Indic voices (Indic-TTS)
- Local dialect support
- One-tap language switching

#### 👥 Shared Device Mode
- Multiple user profiles on one device
- **< 3 second** profile switching
- PIN/biometric authentication (no login required)
- Isolated user data and progress

### For Teachers

#### 🤖 AI Content Creator
- Convert text/PDF to video in **< 5 minutes**
- Paste NCERT/Wikipedia content
- AI-powered script generation (Gemma-2B)
- Automated scene design and visuals

#### 🎬 Zero-Skill Production
- No video editing required
- AI-generated avatars with regional attire
- Natural lip-sync (95%+ accuracy)
- One-click translation to 12 languages

#### 📊 Analytics Dashboard
- Track student progress offline
- Engagement metrics and completion rates
- Works with intermittent connectivity
- Actionable insights for teaching

---

## 🏗️ Technical Architecture

### 5-Layer Architecture

```
┌─────────────────────────────────────────────────────────┐
│  Layer 1: Mobile UI (React Native)                      │
│  • Student App • Teacher App • Profile Manager          │
└─────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│  Layer 2: Edge AI (On-Device)                           │
│  • Gemma-2B (300MB, 4-bit quantized)                    │
│  • IndicBERT (Bharat-specific corpus)                   │
│  • ONNX Runtime + Qualcomm AI Stack                     │
└─────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│  Layer 3: Local Storage (ObjectBox)                     │
│  • User Profiles • Content Cache • Progress Data        │
│  • Zero-copy operations • Offline-first sync            │
└─────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│  Layer 4: Sync Layer (WorkManager)                      │
│  • Smart Sync • Delta Sync • Brotli Compression         │
│  • Constraint-aware (WiFi, Battery, Time)               │
└─────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│  Layer 5: Cloud Infrastructure (AWS)                    │
│  • AWS Batch (GPU workers) • SageMaker (avatars)        │
│  • Wav2Lip (lip-sync) • S3+CloudFront (CDN)             │
│  • MLOps Pipeline (QLoRA fine-tuning)                   │
└─────────────────────────────────────────────────────────┘
```

### Technology Stack

**Mobile Layer:**
- React Native (Android 8.0+)
- ObjectBox (offline NoSQL)
- WorkManager (background sync)
- ONNX Runtime (edge inference)

**Edge AI Layer:**
- Gemma-2B (4-bit quantized, 300MB)
- IndicBERT (regional languages)
- LoRA fine-tuning
- Qualcomm AI Stack

**Multimedia Layer:**
- AWS SageMaker/EC2 (avatar generation)
- Indic-TTS (12+ languages)
- Wav2Lip (lip-sync)
- H.265/HEVC encoding

**Cloud Layer:**
- AWS Batch (serverless GPU workers)
- S3 + CloudFront (global CDN)
- Lambda (sync endpoints)
- DynamoDB (user data)

**MLOps Layer:**
- MLflow (experiment tracking)
- QLoRA (continuous fine-tuning)
- A/B testing framework
- Model versioning

---

## � User Journeyse

### Student's 24-Hour Learning Cycle

#### Morning (6:00 AM) - Offline Study
```
📱 Opens app on weak 2G signal
✅ App works 100% offline
📚 Watches 3-4 cached lessons (10MB total)
📝 Progress tracked locally
```

#### School (12:00 PM) - Smart Sync
```
📶 WiFi detected automatically
⬆️ Syncs progress (< 2KB per lesson)
⬇️ Downloads next 5 lessons (~12.5MB)
⚡ Total sync time: < 30 seconds
```

#### Evening (6:00 PM) - Offline Practice
```
📝 Completes offline quizzes
💾 Results saved locally
📖 Reviews previous lessons
🎯 All data persisted in ObjectBox
```

#### Night (2:00 AM) - Background Sync
```
🔋 Device charging + WiFi connected
☁️ WorkManager triggers background sync
📤 Uploads quiz results and analytics
📥 Downloads tomorrow's content
✅ Ready for next day
```

### Teacher's Content Creation Flow

#### Step 1: Content Input (2 minutes)
```
📄 Paste text or upload PDF (NCERT/Wikipedia)
🌐 Select target language
👨‍🏫 Choose avatar and voice
```

#### Step 2: AI Processing (3 minutes)
```
🤖 Gemma-2B generates structured script
🎬 AI designs scenes automatically
🖼️ Generates visuals and transitions
```

#### Step 3: Publish (1 minute)
```
🌍 One-click translation to 12 languages
☁️ Cloud rendering (5-10 minutes)
📹 H.265 encoded videos delivered via CDN
✅ Available to students instantly
```

---

## 📊 Performance Targets

### Technical Performance Goals

| Metric | Target |
|--------|--------|
| App Startup Time | < 5 seconds |
| Model Inference | < 10 seconds |
| Video Generation | < 5 minutes |
| Sync Data Usage | < 2KB per operation |
| Initial Install Size | 45MB |
| Memory Usage (2GB RAM) | < 600MB |
| Crash Rate | < 0.1% |
| Sync Success Rate | > 99% |

### Business Goals

| Metric | Target |
|--------|--------|
| Cost per User | ₹89/year |
| Infrastructure Scaling | 1.2x cost for 10x users |
| User Acquisition Cost | < ₹50 |
| Monthly Retention | 80% |
| Daily Active Users | 60% |

### Educational Impact Goals

| Metric | Target |
|--------|--------|
| Test Score Improvement | 25% |
| Content Completion Rate | 80% |
| Teacher Productivity | 5x increase |
| Languages Supported | 12+ |
| Rural Students Reached | 1M+ in first year |

---

## 🏆 Competitive Advantages

### 1. Quantized Model Moat

**Proprietary Optimization:**
- Custom 4-bit quantization for educational content
- LoRA fine-tuning on Bharat-specific corpus
- 95%+ accuracy despite 75% size reduction
- 18-24 months lead time for competitors

**Technical Barrier:**
- Requires proprietary training data
- Domain-specific optimization techniques
- Continuous improvement through user data

### 2. Data Moat

**Proprietary Dataset:**
- Regional language educational corpus (12+ languages)
- Student interaction patterns and learning analytics
- Teacher-generated content library
- Cultural context and local dialect variations

**Network Effects:**
- More users → More content → Better models → More users
- Teacher-generated content creates unique library
- Student progress data improves personalization

### 3. Infrastructure Moat

**Cost Optimization:**
- Sub-linear scaling (1.2x cost for 10x users)
- 90% reduction in bandwidth costs through caching
- 70% reduction in compute costs via spot instances
- Edge inference eliminates cloud API costs

**Technical Barrier:**
- Competitors need 10x infrastructure investment
- Offline-first requires fundamental redesign
- Delta sync and compression require deep expertise

### 4. User Experience Moat

**Offline-First Design:**
- Only platform with true offline-first for rural education
- 45MB install vs competitors' 200MB+
- 2KB sync vs competitors' 50KB+ overhead
- Works on 2G while competitors require 4G

**Switching Costs:**
- Students build learning history
- Teachers invest in content creation
- Shared device profiles create family lock-in
- Offline content library represents sunk data costs

---

## 📚 Project Documentation

For detailed technical specifications, please refer to:

- **Requirements Document**: `.kiro/specs/rural-education-video-app/requirements.md`
- **Design Document**: `.kiro/specs/rural-education-video-app/design.md`
- **Implementation Tasks**: `.kiro/specs/rural-education-video-app/tasks.md`

---

<div align="center">

**Made for Rural India**

*Project Status: In Development*

</div>
