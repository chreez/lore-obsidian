# Lore Obsidian Plugin

**Seamlessly integrate Lore research sessions into your Obsidian vault.**

## Overview

The Lore Obsidian plugin connects your Obsidian vault to a running Lore research engine, allowing you to conduct AI-powered research directly within your note-taking workflow.

## 🚀 Quick Start

### Installation

1. **Install from Community Plugins** (coming soon)
   - Open Obsidian Settings → Community Plugins
   - Search for "Lore Research"
   - Install and enable

2. **Manual Installation** (development)
   ```bash
   cd /path/to/your/vault/.obsidian/plugins/
   git clone https://github.com/chreez/lore-obsidian.git
   cd lore-obsidian
   npm install && npm run build
   ```

### Setup

1. **Start Lore Engine**
   ```bash
   lore server start
   # Optionally: lore server install-daemon (auto-start on macOS)
   ```

2. **Configure Plugin**
   - Open Obsidian Settings → Lore Research
   - Set API URL: `http://localhost:3000`
   - Test connection

3. **Start Researching**
   - Use Command Palette: "Lore: Start Research"
   - Or use ribbon icon
   - Or type in any note: `/lore sustainable packaging`

## 🎯 Features

### Research Integration
- **Start Research**: Command palette or slash command integration
- **Real-time Sync**: Research notes appear in your vault as they're generated
- **Vault Organization**: Creates organized `/lore-sessions/` folder structure
- **Zettelkasten Format**: Generated notes follow Zettelkasten conventions

### Note Management
- **Auto-linking**: Uses Obsidian `[[wikilink]]` syntax for connections
- **Tag Integration**: Research tags sync with Obsidian tags
- **Source Attribution**: Every note links back to its source
- **Confidence Indicators**: Visual confidence scores in note metadata

### Vault Compatibility
- **Non-destructive**: Never modifies existing notes
- **Standard Markdown**: All generated notes are plain markdown
- **Export Options**: Export research to other formats anytime
- **Offline Access**: Research data remains available offline

## 🔌 Lore API Integration

**API Version**: `1.0.0`  
**Types**: References lore engine `src/interfaces/api.ts`  
**Specification**: Follows `lore/docs/api/openapi.yaml`

```typescript
import { LoreNote, LoreResearchSession } from '../types/lore-api';

// Plugin connects to local Lore engine
const session = await this.loreApi.research.start({
  topic: "sustainable packaging",
  vault_path: this.app.vault.adapter.path
});
```

## 📁 Vault Structure

When you start a research session, the plugin creates:

```
your-vault/
├── lore-sessions/
│   └── 20241215-143022-sustainable-packaging/
│       ├── session.md              # Research session overview
│       ├── sources/                # Source documents and metadata
│       │   ├── youtube-video-1.md
│       │   ├── web-article-2.md
│       │   └── academic-paper-3.md
│       └── notes/                  # Atomic research notes
│           ├── 20241215-143022-sustainable-packaging-001.md
│           ├── 20241215-143022-sustainable-packaging-002.md
│           └── connections.md      # Note relationships
└── your-existing-notes/            # Unchanged
```

### Note Format Example

```markdown
---
id: 20241215-143022-sustainable-packaging-001
source: https://example.com/sustainable-packaging-trends
confidence: 0.85
tags: [market-analysis, sustainability, packaging]
created: 2024-12-15T14:30:22Z
---

# Market Size Growth

The global sustainable packaging market was valued at $220 billion in 2023 and is projected to reach $370 billion by 2030.

## Source
- [[youtube-video-sustainable-trends]]
- Original: [Sustainable Packaging Market Report](https://example.com/report)

## Related Notes
- [[20241215-143022-sustainable-packaging-002]] - Consumer preferences
- [[20241215-143022-sustainable-packaging-003]] - Technology innovations

#fact #market-data #sustainability
```

## ⚙️ Plugin Commands

### Command Palette
- **"Lore: Start Research"** - Start new research session
- **"Lore: Check Status"** - View active research progress
- **"Lore: Open Research Dashboard"** - Open web interface
- **"Lore: Export Session"** - Export current session data
- **"Lore: Connect to Engine"** - Test Lore API connection

### Slash Commands (in notes)
- `/lore <topic>` - Start research on topic
- `/lore status` - Show research status
- `/lore query <question>` - Query existing research

### Ribbon Actions
- Research icon - Quick access to start research
- Status indicator - Shows active research sessions

## 🔧 Settings

```yaml
# Plugin Settings
api_url: "http://localhost:3000"
api_key: ""                     # Optional API key
auto_sync: true                 # Real-time note updates
vault_organization:
  sessions_folder: "lore-sessions"
  note_template: "zettelkasten"
  link_format: "wikilink"
display:
  show_confidence: true
  show_ribbon_icon: true
  show_status_bar: true
research_defaults:
  depth_limit: 2
  cost_limit: 15
  auto_start: false
```

## 🔄 Real-time Sync

The plugin maintains a live connection to the Lore engine:

- **Progress Updates**: Real-time research progress in status bar
- **New Notes**: Notes appear in vault as they're generated
- **Link Discovery**: Connections update automatically
- **Session Completion**: Notification when research finishes

## 🧪 Development

```bash
# Clone and setup
git clone https://github.com/chreez/lore-obsidian.git
cd lore-obsidian
npm install

# Development build (with watch)
npm run dev

# Production build
npm run build

# Install in Obsidian vault
npm run install-vault /path/to/vault

# Testing
npm run test
```

## 📱 Mobile Support

The plugin works on Obsidian mobile with some limitations:

- ✅ View research notes and navigate links
- ✅ Read session summaries and sources
- ✅ Export research data
- ❌ Start new research (requires desktop/server)
- ❌ Real-time sync (limited by mobile background processing)

## 🤝 Contributing

1. Reference Lore API specification for integration changes
2. Follow Obsidian plugin development guidelines
3. Test with various vault configurations
4. Maintain backwards compatibility with note formats
5. Document new features and settings

## 🔒 Privacy & Security

- **Local-First**: All research data stored in your vault
- **No Cloud Dependency**: Works entirely offline after research completion
- **Source Attribution**: Complete traceability to original sources
- **Export Freedom**: Standard markdown, no lock-in

## 📄 License

MIT License - see LICENSE file for details.

---

**Note**: This plugin requires a running Lore research engine. See the main [lore repository](https://github.com/chreez/lore) for installation instructions.