# 📝 Notely - iOS Note-Taking App

![Swift](https://img.shields.io/badge/swift-F54A2A?style=for-the-badge\&logo=swift\&logoColor=white)
![iOS](https://img.shields.io/badge/iOS-000000?style=for-the-badge\&logo=ios\&logoColor=white)
![Xcode](https://img.shields.io/badge/Xcode-007ACC?style=for-the-badge\&logo=Xcode\&logoColor=white)
![SwiftUI](https://img.shields.io/badge/SwiftUI-0D96F6?style=for-the-badge\&logo=swift\&logoColor=white)
![CloudKit](https://img.shields.io/badge/CloudKit-2AA198?style=for-the-badge\&logo=apple\&logoColor=white)

A modern, privacy-first note-taking application for iOS built with Swift and SwiftUI. Create, organize, and search notes — text, markdown, handwriting, images, and audio — with lightning-fast performance and beautiful, distraction-free UI.

---

## 📋 Table of Contents

* [Problem Statement](#-problem-statement)
* [Solution](#-solution)
* [Tech Stack](#-tech-stack)
* [Tools Used](#-tools-used)
* [Features](#-features)
* [Screenshots](#-screenshots)
* [Architecture](#-architecture)
* [Getting Started](#-getting-started)
* [Installation](#-installation)
* [Usage](#-usage)
* [Testing](#-testing)
* [Future Scope](#-future-scope)
* [Contributing](#-contributing)
* [License](#-license)

---

## 🎯 Problem Statement

People struggle with note-taking apps that are either too simple or too complex. Common pain points:

* **Fragmented note types** — needing separate apps for text, handwriting, and audio
* **Poor organization** — hard to find notes quickly
* **Slow search** — inefficient indexing of content and attachments
* **Privacy concerns** — sensitive notes stored on third-party servers
* **Limited input methods** — weak support for Apple Pencil and handwriting
* **No offline reliability** — app depends on constant internet
* **Cluttered UI** — distractions reduce productivity
* **Weak export & collaboration** — poor sharing and versioning

---

## ✨ Solution

Notely is a delightful, all-in-one note-taking experience focusing on speed, privacy, and flexibility.

### 🚀 Key Benefits

* **Unified Notes** — text, markdown, rich text, handwriting, sketches, audio, and attachments in one place
* **Powerful Organization** — tags, notebooks, pinned notes, smart filters
* **Fast Search** — full-text search (including OCR & handwriting recognition)
* **Privacy-First** — local-first storage with optional iCloud encryption and CloudKit sync
* **Apple Pencil & Handwriting** — smooth drawing, pressure support, and handwriting-to-text
* **Offline First** — full functionality without internet
* **Beautiful, Minimal UI** — distraction-free writing modes and themes

---

## 🛠️ Tech Stack

### Core Technologies

* **Swift 5.9** – Primary language
* **SwiftUI** – Main UI framework
* **Combine** – Reactive data pipelines
* **Swift Concurrency (async/await)** – Asynchronous tasks

### Frameworks & Libraries

* **Core Data** – Local persistence with efficient querying
* **CloudKit** – Optional cross-device sync
* **FileProvider / UIDocument** – Attachments and Files integration
* **Vision (OCR)** – Image text extraction
* **PencilKit** – Apple Pencil drawing and sketches
* **Speech** – Audio note transcription
* **Natural Language** – Smart tagging and summarization
* **Spotlight / Core Spotlight** – System search indexing
* **WidgetKit & Live Activities** – Widgets and pinned note live-updates

---

## ⚡ Features

### Core Functionality

* ✅ **Rich Text & Markdown Editor** with live preview and formatting toolbar
* ✅ **Plain Text Mode** for distraction-free writing
* ✅ **Handwriting & Sketching** using PencilKit; convert handwriting to text
* ✅ **Audio Notes** with optional transcription
* ✅ **Attachments**: images, PDFs, documents, web clippings
* ✅ **Tags & Notebooks**: multi-tag support and nested notebooks
* ✅ **Smart Filters**: unread, pinned, recent, attachments, tag-based queries
* ✅ **Full-Text Search** including OCR'd text and transcribed audio
* ✅ **Version History** and undo/redo for notes
* ✅ **Password / Biometric Lock** per-note or notebook
* ✅ **Export**: PDF, Markdown, Plain Text, Evernote XML
* ✅ **Share & Collaboration**: read-only links, edit invitations (optional)

### iOS & System Integration

* ✅ **iPad & Multitasking** support; Slide Over / Split View
* ✅ **Apple Pencil** tilt/pressure and palm rejection
* ✅ **Spotlight Indexing** for global search
* ✅ **Shortcuts & Siri** actions (create note, search tag)
* ✅ **Home Screen Widgets** for quick notes and pinned items
* ✅ **Share Extension** for saving web clippings and selected text
* ✅ **Dark Mode & Dynamic Type** for accessibility

### Privacy & Sync

* ✅ **Local-first data storage** (Core Data) with optional encrypted iCloud sync
* ✅ **End-to-end encryption** option for user-selected notebooks
* ✅ **On-device ML** for tagging and summarization
* ✅ **No third-party analytics by default**; opt-in telemetry

---

## 📸 Screenshots

<div align="center">

| Notes List                               | Editor (Markdown)                 | Handwriting                                 |
| ---------------------------------------- | --------------------------------- | ------------------------------------------- |
| ![NotesList](screenshots/notes_list.png) | ![Editor](screenshots/editor.png) | ![Handwriting](screenshots/handwriting.png) |

| Widgets                             | Tag View                      | Attachments                                 |
| ----------------------------------- | ----------------------------- | ------------------------------------------- |
| ![Widgets](screenshots/widgets.png) | ![Tags](screenshots/tags.png) | ![Attachments](screenshots/attachments.png) |

</div>

---

## 🏗️ Architecture

### MVVM + Services

```
┌─────────────────────────────────────────────┐
│                SwiftUI Views                │
│ (NotesListView, NoteEditorView, TagView...) │
└──────────────────┬──────────────────────────┘
                   │
                   │ @StateObject / @ObservedObject
                   │
┌──────────────────▼──────────────────────────┐
│                ViewModels                   │
│ (NotesViewModel, EditorViewModel, TagVM)    │
│ - @Published state                           │
│ - Formatting & undo logic                    │
└──────────────────┬──────────────────────────┘
                   │
                   │ Dependency Injection / Protocols
                   │
┌──────────────────▼──────────────────────────┐
│                 Services                     │
│ - PersistenceService (Core Data)             │
│ - SyncService (CloudKit / iCloud)            │
│ - SearchService (Spotlight, Vision OCR)      │
│ - AttachmentService (FileProvider)           │
└──────────────────┬──────────────────────────┘
                   │
      ┌────────────┼────────────┐
      │            │            │
┌─────▼─────┐ ┌────▼────┐ ┌────▼─────┐
│Core Data  │ │CloudKit │ │PencilKit │
└───────────┘ └─────────┘ └──────────┘
```

### Project Structure

```
Notely/
├── App/
│   ├── NotelyApp.swift
│   └── AppDelegate.swift
├── Models/
│   ├── Note.swift
│   ├── Tag.swift
│   ├── Notebook.swift
│   └── Attachment.swift
├── Views/
│   ├── NotesList/
│   ├── Editor/
│   ├── Tags/
│   ├── Widgets/
│   └── Settings/
├── ViewModels/
│   ├── NotesViewModel.swift
│   ├── EditorViewModel.swift
│   └── SearchViewModel.swift
├── Services/
│   ├── PersistenceService.swift
│   ├── SyncService.swift
│   ├── SearchService.swift
│   └── AttachmentService.swift
├── Utilities/
│   ├── Extensions/
│   ├── Formatters/
│   └── Helpers.swift
├── Resources/
│   ├── Assets.xcassets
│   └── Localizable.strings
└── Tests/
    ├── UnitTests/
    └── UITests/
```

---

## 🚀 Getting Started

### Prerequisites

* macOS 13.0 (Ventura) or later
* Xcode 15.0 or later
* iOS 16.0+ target device or simulator
* Apple Developer Account (for device testing and CloudKit)
* Swift Package Manager (SPM)

### System Requirements

```
Minimum iOS Version: 16.0
Supported Devices: iPhone 11 and newer
iPad: iPadOS 16+
```

---

## 📥 Installation

### 1. Clone the repository

```bash
git clone https://github.com/ANKUR-PRAJAPATI/Notely-iOS.git
cd Notely-iOS
```

### 2. Install Dependencies (SPM recommended)

```bash
# Open the project in Xcode and SPM packages will resolve automatically
open Notely.xcodeproj
```

### 3. Configure Signing

1. Open `Notely.xcodeproj` in Xcode
2. Select the project in the navigator
3. Go to "Signing & Capabilities"
4. Select your Team and update Bundle Identifier

### 4. Add Capabilities

* ✅ CloudKit / iCloud
* ✅ PencilKit (no entitlement required)
* ✅ Background Modes (audio recording, fetch)
* ✅ Siri & Shortcuts
* ✅ App Groups (for extensions)

### 5. Update Info.plist

Add privacy descriptions and usage strings for microphone, camera, and motion if needed.

---

## 💻 Usage

### Basic Workflow

#### 1. First Launch Onboarding

* Welcome screen
* Option to enable iCloud sync and encryption
* Set up default notebook and import options

#### 2. Create a Note

1. Tap the "+" button
2. Choose type (Text / Markdown / Handwriting / Audio)
3. Start typing, drawing, or recording
4. Add tags, attachments, and pin if needed
5. Tap Save (auto-save enabled)

#### 3. Search & Organization

* Use the search bar to find text, tags, or OCR results
* Use smart filters to show pinned, recent, or attachment notes
* Drag & drop notes between notebooks on iPad

#### 4. Share & Export

* Export as PDF / Markdown
* Share a read-only link or invite collaborators
* Use Share Extension to clip web content

---

## 🧪 Testing

### Unit Tests

```bash
xcodebuild test -scheme Notely -destination 'platform=iOS Simulator,name=iPhone 15 Pro'
```

### UI Tests

```bash
xcodebuild test -scheme Notely -destination 'platform=iOS Simulator,name=iPhone 15 Pro' -only-testing:NotelyUITests
```

### Test Coverage

```bash
xcodebuild test -scheme Notely -enableCodeCoverage YES -destination 'platform=iOS Simulator,name=iPhone 15 Pro'
```

---

## 🔮 Future Scope

### Planned Features

* [ ] **Real-Time Collaboration** (multi-user editing)
* [ ] **Encrypted Cloud Sync** (user-controlled keys)
* [ ] **Advanced Handwriting Search** (improved on-device models)
* [ ] **Built-in Templates** (meeting notes, lecture, journal)
* [ ] **AI Summaries & Smart Tags** (on-device ML)
* [ ] **Web Clipper Extension** for Safari & Chrome
* [ ] **macOS Native App** with Catalyst or SwiftUI macOS target
* [ ] **Widget Shortcuts** for quick capture
* [ ] **End-to-end encrypted sharing** for private notebooks
* [ ] **Publish to web** (share a public note page)

### Technical Improvements

* [ ] Background indexing optimizations
* [ ] Add GraphQL backend if server features are required
* [ ] Improve conflict resolution for CloudKit sync
* [ ] Localization for 20+ languages

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Follow Swift style guidelines and write tests
4. Update documentation and migration notes
5. Open a pull request with a clear description and screenshots

### Commit Message Convention

```
feat: Add new feature
fix: Bug fix
docs: Documentation update
style: Code style changes
refactor: Code refactor
test: Add tests
chore: Maintenance tasks
```

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Ankur Prajapati**

💼 **LinkedIn:** [linkedin.com/in/ankur-prajapati-5618a1258](https://linkedin.com/in/ankur-prajapati-5618a1258)
📧 **Email:** [prajapatiankur37@gmail.com](mailto:prajapatiankur37@gmail.com)
💻 **GitHub:** [@ANKUR-PRAJAPATI](https://github.com/ANKUR-PRAJAPATI)

---

## 🙏 Acknowledgments

* Apple for Swift, SwiftUI, and developer tools
* PencilKit and Vision frameworks for handwriting and OCR
* Open-source note-taking projects and community for inspiration

---


---

<div align="center">

### ⭐ If you found this helpful, please consider giving it a star!

**Made with ❤️ and lots of ☕**

📬 **Feel free to reach out for collaborations or questions!**

</div>
