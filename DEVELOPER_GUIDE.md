# MindTug - Developer Guide

This document outlines the technical requirements, architecture, and future steps to turn this prototype into a full-fledged AI Learning System.

## Project Overview
MindTug is a gamified learning platform where students compete in a tug-of-war battle by answering questions generated from a syllabus.

### Current Architecture (Prototype)
- **Frontend**: React (Vite) + Tailwind CSS
- **State**: React Context (`GameContext`, `UserContext`)
- **Animation**: Framer Motion
- **Backend / AI**: Mocked in `src/lib/mockAI.js`

## Requirements for Full Production

To take this to production (Hackathon or Real-world), you need:

1.  **Backend API** (Node.js/Express or Python/FastAPI)
    - Handle real-time WebSocket connections (Socket.io) for synchronized game state.
    - Secure database (PostgreSQL/MongoDB) for user profiles and history.

2.  **AI Integration** (Replace `mockAI.js`)
    - **Model**: OpenAI GPT-4o or Google Gemini 1.5 Pro.
    - **API Key**: Required from the respective provider.

## AI API Integration Guide

### 1. Topic Analyzer (Question Generation)
**Goal**: Convert syllabus text into structured questions.

**Prompt Strategy:**
```text
Role: Educational Question Generator
Input: {syllabus_text}
Output: JSON array of 5 questions.
Format: 
[
  { "id": 1, "text": "Question?", "difficulty": "easy", "correct_answer_key": "..." }
]
Constraint: Questions must test understanding, not just recall.
```

### 2. Answer Evaluator (Grading)
**Goal**: Score student answers (0-100) and provide feedback.

**Prompt Strategy:**
```text
Role: Strict Teacher
Context: Question: "{question_text}"
Input: Student Answer: "{student_answer}"
Task: Rate the answer from 0 to 100 based on accuracy and depth.
Output: JSON { "score": 85, "feedback": "Great explanation of X, but missed Y." }
```

## Step-by-Step Setup Guide

### 1. Installation
```bash
cd mind-tug-app
npm install
```

### 2. Running Locally
```bash
npm run dev
```

### 3. Usage Flow
1.  Open two browser windows.
2.  **Window 1 (Teacher)**:
    - Login as Teacher.
    - Paste dummy syllabus (e.g., "Photosynthesis is the process...").
    - Click "Generate Battle".
    - Copy the **Room Code**.
3.  **Window 2 (Student)**:
    - Login as Student (pick an avatar).
    - Enter the Room Code.
    - Wait for Teacher to start (or force start in prototype).
4.  **Battle**:
    - Student types answer.
    - "AI" grades it.
    - Rope moves based on score.

## Future Roadmap
- [ ] **WebSockets**: Implement `socket.io-client` in `GameContext` to sync rope position across devices.
- [ ] **Database**: Store user rankings and history.
- [ ] **Voice Input**: Allow students to speak answers (Web Speech API).
