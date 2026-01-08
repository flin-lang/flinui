# FlinUI PRO — AI Components

Complete suite of production-ready AI components for building intelligent applications.

## Components Overview

**26 Total Components** across 5 categories:
- **Chat Interface**: 10 components (ChatGPT-style interfaces)
- **AI Interaction**: 5 components (Prompts & responses)
- **AI Tools & Code**: 3 components (Developer tools)
- **AI Generation**: 5 components (Content creation)
- **AI Analysis**: 2 components (Document & agent monitoring)

---

# Chat Interface Components (10 Total)

### 🎯 Main Interface

#### **AIChatbot.flin**
Full-featured ChatGPT-style chat interface with streaming, message history, and model selection.

```flin
<AIChatbot
    title="AI Assistant"
    model="claude-sonnet-4-5"
    showReasoningPanel={false}
    showSidebar={true}
/>
```

**Props:**
- `title`: text (default: "AI Assistant")
- `model`: text (default: "claude-sonnet-4-5")
- `showReasoningPanel`: boolean (default: false)
- `showSidebar`: boolean (default: true)

---

### 💬 Message Components

#### **ChatMessages.flin**
Conversation thread displaying user and assistant messages with avatars.

```flin
<ChatMessages
    messages={messageList}
    showAvatars={true}
    showTimestamps={false}
/>
```

**Props:**
- `messages`: list (required)
- `showAvatars`: boolean (default: true)
- `showTimestamps`: boolean (default: false)

---

#### **ChatBubble.flin**
Individual message bubble with role-based styling and markdown support.

```flin
<ChatBubble
    content="Hello, how can I help you?"
    role="assistant"
    isStreaming={false}
/>
```

**Props:**
- `content`: text (required)
- `role`: "user" | "assistant" (default: "user")
- `isStreaming`: boolean (default: false)

---

#### **ChatTypingIndicator.flin**
Animated typing indicator with pulsing dots.

```flin
<ChatTypingIndicator size="md" />
```

**Props:**
- `size`: "sm" | "md" | "lg" (default: "md")

---

#### **ChatStreamingText.flin**
Character-by-character text display with cursor animation.

```flin
<ChatStreamingText
    text={streamedContent}
    speed={30}
    showCursor={true}
/>
```

**Props:**
- `text`: text (required)
- `speed`: number (ms per char, default: 30)
- `showCursor`: boolean (default: true)

---

### 🎛️ Input & Controls

#### **ChatInput.flin**
Text input area with file upload and voice input buttons.

```flin
<ChatInput
    onSend={(text) => sendMessage(text)}
    placeholder="Type a message..."
    disabled={false}
    showFileUpload={true}
    showVoice={true}
/>
```

**Props:**
- `onSend`: function (required)
- `placeholder`: text (default: "Type a message...")
- `disabled`: boolean (default: false)
- `showFileUpload`: boolean (default: true)
- `showVoice`: boolean (default: true)

**Features:**
- Auto-expanding textarea
- File attachment support
- Voice input button
- Enter to send, Shift+Enter for new line
- Send button with active state

---

#### **ChatModelSelector.flin**
Dropdown selector for AI model selection.

```flin
<ChatModelSelector
    model="claude-sonnet-4-5"
    onChange={(model) => setModel(model)}
    disabled={false}
/>
```

**Props:**
- `model`: text (default: "claude-sonnet-4-5")
- `onChange`: function
- `disabled`: boolean (default: false)

**Built-in Models:**
- Claude Opus 4.5
- Claude Sonnet 4.5
- Claude Haiku 4
- GPT-4
- GPT-3.5 Turbo

---

### 🔬 Advanced Features

#### **ChatReasoningPanel.flin**
Collapsible panel displaying AI reasoning/thinking process.

```flin
<ChatReasoningPanel
    reasoning={message.reasoning}
    isExpanded={false}
    title="Reasoning"
/>
```

**Props:**
- `reasoning`: text (required)
- `isExpanded`: boolean (default: false)
- `title`: text (default: "Reasoning")

---

#### **ChatSourceCitations.flin**
Expandable list of sources and citations with links.

```flin
<ChatSourceCitations
    sources={[
        { title: "Source 1", url: "https://...", description: "..." },
        { title: "Source 2", url: "https://...", description: "..." }
    ]}
    isExpanded={false}
    maxVisible={3}
/>
```

**Props:**
- `sources`: list (required)
- `isExpanded`: boolean (default: false)
- `maxVisible`: number (default: 3)

**Source Object:**
```flin
{
    title: "Source Title",
    url: "https://example.com",
    description: "Brief description"
}
```

---

#### **ChatConversationList.flin**
Sidebar displaying conversation history with search and actions.

```flin
<ChatConversationList
    onSelect={(conv) => loadConversation(conv)}
    onNew={() => createNewChat()}
    currentConversationId={currentId}
/>
```

**Props:**
- `onSelect`: function
- `onNew`: function
- `currentConversationId`: number

**Features:**
- Search conversations
- Grouped by time (Today, Yesterday, This Week, Older)
- Delete conversations
- New chat button
- Active conversation highlight

---

## Design System

All components use **FlinUI design tokens exclusively**:

### Colors
- Dark background: `var(--flin-bg-deep)`, `var(--flin-bg-surface)`, `var(--flin-bg-elevated)`
- Text: `var(--flin-text-primary)`, `var(--flin-text-secondary)`, `var(--flin-text-muted)`
- Accents: `var(--flin-accent-gold)`, `var(--flin-accent-violet)`, `var(--flin-accent-cyan)`
- User messages: `var(--flin-accent-gold-muted)` background
- Assistant messages: `var(--flin-bg-elevated)` background

### Typography
- Body font: `var(--flin-font-body)`
- Mono font: `var(--flin-font-mono)` (for code blocks and model names)
- Sizes: `var(--flin-text-sm)`, `var(--flin-text-xs)`, etc.

### Spacing
- Consistent spacing: `var(--flin-space-1)` through `var(--flin-space-96)`
- Component padding: `var(--flin-space-3)` to `var(--flin-space-4)`

### Animations
- Transitions: `var(--flin-transition-fast)`, `var(--flin-transition-normal)`
- Easing: `var(--flin-ease-out)`, `var(--flin-ease-in-out)`
- Message reveals: Staggered slide-in animation
- Typing indicator: Pulsing dots animation

---

## Data Models

### Message Entity
```flin
entity Message {
    role: text = "user"          // "user" | "assistant"
    content: text                // Message content
    timestamp: datetime = now()  // When sent
    model: text = "claude-sonnet-4-5"  // AI model used
    reasoning: text = ""         // Optional reasoning
    sources: list = []           // Optional citations
}
```

### Conversation Entity
```flin
entity Conversation {
    title: text = "New Conversation"
    created_at: datetime = now()
    updated_at: datetime = now()
    message_count: number = 0
}
```

---

## Complete Examples

### Minimal Chat Interface
```flin
<AIChatbot />
```

### Custom Chat with All Features
```flin
entity Message {
    role: text = "user"
    content: text
    timestamp: datetime = now()
    model: text = "claude-sonnet-4-5"
    reasoning: text = ""
    sources: list = []
}

currentModel = "claude-sonnet-4-5"
messages = Message.all.order_by("timestamp asc")
isStreaming = false

<div class="my-chat-app">
    <ChatConversationList
        currentConversationId={currentConv.id}
        onNew={() => createConversation()}
    />

    <div class="chat-area">
        <div class="header">
            <h1>AI Assistant</h1>
            <ChatModelSelector
                model={currentModel}
                onChange={(m) => { currentModel = m }}
            />
        </div>

        <div class="messages">
            <ChatMessages messages={messages} showTimestamps={true} />

            {if isStreaming}
                <ChatTypingIndicator />
            {/if}
        </div>

        <ChatInput
            onSend={(text) => {
                Message.create({
                    role: "user",
                    content: text,
                    conversation_id: currentConv.id
                })
                isStreaming = true
                // Trigger AI response...
            }}
        />
    </div>
</div>
```

### Individual Message with Citations
```flin
message = {
    role: "assistant",
    content: "Based on recent research...",
    model: "claude-sonnet-4-5",
    reasoning: "I analyzed multiple sources and considered...",
    sources: [
        {
            title: "Research Paper on AI",
            url: "https://arxiv.org/...",
            description: "Key findings on neural networks"
        }
    ]
}

<div class="message">
    <ChatBubble content={message.content} role={message.role} />
    <ChatReasoningPanel reasoning={message.reasoning} />
    <ChatSourceCitations sources={message.sources} />
</div>
```

---

## Tech Stack

- **Design System**: FlinUI Design Tokens
- **Theme**: African Dusk (dark mode first)
- **Fonts**: Outfit (body), JetBrains Mono (code)
- **State Management**: FLIN entities
- **Animations**: CSS animations with design token timing

---

## Browser Support

All components use standard CSS and modern web APIs. Tested on:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+

---

## License

Part of FlinUI PRO — proprietary component library by ZeroSuite, Inc.

---

## Contributing

For bugs or feature requests, contact the FlinUI team.

---

# AI Interaction Components (5 Total)

Prompt and response handling with feedback mechanisms.

## AIPromptInput.flin

Input field with AI prompt suggestions and templates.

```flin
<AIPromptInput
    variant="primary"
    placeholder="Ask anything..."
    showSuggestions={true}
    suggestions={["Explain this code", "Write a function that..."]}
    onSubmit={(prompt) => sendToAI(prompt)}
/>
```

**Props:**
- `variant`: "primary" | "secondary" | "minimal" (default: "primary")
- `placeholder`: text (default: "Ask anything...")
- `showSuggestions`: boolean (default: true)
- `suggestions`: list of suggestion texts
- `onSubmit`: function (receives prompt text)

**Features:**
- Multi-line textarea with auto-resize
- Character counter
- Suggestion grid (responsive)
- Enter to submit, Shift+Enter for new line
- Template button for future expansion

---

## AIPromptLibrary.flin

Saved prompts grid with search and categories.

```flin
<AIPromptLibrary
    prompts={[
        { id: 1, title: "Code Review", description: "Review my code", category: "Development" }
    ]}
    onSelect={(prompt) => usePrompt(prompt)}
    columns={3}
/>
```

**Props:**
- `prompts`: list of prompt objects
- `onSelect`: function (receives selected prompt)
- `columns`: number (default: 3, responsive)

**Prompt Object:**
```flin
{
    id: number,
    title: text,
    description: text,
    category: text
}
```

**Features:**
- Search by title/description
- Category filtering
- Responsive grid (3 cols → 2 cols → 1 col)
- Hover animations with gold accent
- Empty state handling

---

## AIResponseCard.flin

Formatted AI response with copy, share, and regenerate actions.

```flin
<AIResponseCard
    content={aiResponse}
    timestamp="10:30 AM"
    model="Claude Sonnet 4.5"
    onCopy={(text) => copyToClipboard(text)}
    onRegenerate={() => regenerate()}
    onShare={() => share()}
/>
```

**Props:**
- `content`: text (required)
- `timestamp`: text
- `model`: text (default: "Claude Sonnet 4.5")
- `onCopy`: function
- `onRegenerate`: function
- `onShare`: function

**Features:**
- Model badge with timestamp
- Copy button with "Copied!" feedback
- Character count
- Optional regenerate/share actions
- Card elevation on hover

---

## AILoadingState.flin

Animated processing indicator with 4 variants.

```flin
<AILoadingState
    variant="thinking"
    message="AI is thinking..."
    showProgress={true}
    progress={45}
/>
```

**Props:**
- `variant`: "dots" | "pulse" | "thinking" | "typing" (default: "thinking")
- `message`: text (default: "AI is thinking...")
- `showProgress`: boolean (default: false)
- `progress`: number (0-100)

**Variants:**
- **dots**: 3 pulsing dots
- **pulse**: Expanding ring animation
- **thinking**: Spinning circle
- **typing**: Blinking cursor

---

## AIFeedbackButtons.flin

Feedback actions: thumbs up/down, copy, regenerate.

```flin
<AIFeedbackButtons
    onThumbsUp={() => rateLike()}
    onThumbsDown={() => rateDislike()}
    onCopy={() => copyResponse()}
    onRegenerate={() => regenerate()}
    variant="horizontal"
    size="md"
/>
```

**Props:**
- `onThumbsUp`: function
- `onThumbsDown`: function
- `onCopy`: function
- `onRegenerate`: function
- `variant`: "horizontal" | "vertical" (default: "horizontal")
- `size`: "sm" | "md" | "lg" (default: "md")

**Features:**
- Emoji icons (👍👎📋🔄)
- Active state highlighting
- Copy feedback ("Copied!")
- Separator between rating and actions
- Responsive sizing

---

# AI Tools & Code Components (3 Total)

Developer-focused components for code and tool execution display.

## AIToolCall.flin

Display AI tool/function execution with status and results.

```flin
<AIToolCall
    toolName="search_database"
    status="success"
    input={{ query: "users", limit: 10 }}
    output={{ count: 42, results: [...] }}
    duration={1250}
    expanded={false}
/>
```

**Props:**
- `toolName`: text (required)
- `status`: "pending" | "running" | "success" | "error" (default: "pending")
- `input`: object
- `output`: any
- `duration`: number (milliseconds)
- `expanded`: boolean (default: false)

**Features:**
- Status icon with color coding (⏳⚙️✓✕)
- Collapsible details
- JSON input/output display
- Duration counter
- Spinning animation for running state
- Border color changes by status

---

## AICodeBlock.flin

Syntax highlighted code block with copy button.

```flin
<AICodeBlock
    code={codeString}
    language="javascript"
    showLineNumbers={true}
    fileName="example.js"
    onCopy={(code) => navigator.clipboard.writeText(code)}
/>
```

**Props:**
- `code`: text (required)
- `language`: text (default: "text")
- `showLineNumbers`: boolean (default: true)
- `fileName`: text (optional)
- `onCopy`: function

**Features:**
- Language badge with color coding
- Line numbers (toggleable)
- Filename display
- Copy button with feedback
- Monospace font rendering
- Scrollable for long code

**Language Colors:**
- JavaScript: Gold
- TypeScript: Cyan
- Python: Emerald
- Rust: Orange
- Flin: Violet

---

## AIMarkdownRenderer.flin

Rich text renderer for AI markdown responses.

```flin
<AIMarkdownRenderer
    content={markdownText}
    variant="editorial"
/>
```

**Props:**
- `content`: text (required, HTML or markdown)
- `variant`: "default" | "compact" | "editorial" (default: "default")

**Supported Elements:**
- Headings (h1-h4)
- Paragraphs with relaxed line height
- Links with gold underlines
- Lists (ul/ol) with gold markers
- Blockquotes with left border
- Inline code with violet background
- Code blocks with syntax highlighting
- Tables with striped rows
- Horizontal rules
- Images with rounded corners

**Variants:**
- **default**: Standard spacing and sizes
- **compact**: Reduced margins
- **editorial**: Larger text, generous spacing

---

# AI Generation Components (5 Total)

Content and media generation interfaces.

## AIImageGenerator.flin

Image generation interface with prompt input and result grid.

```flin
<AIImageGenerator
    onGenerate={(params) => generateImage(params)}
    images={[
        { url: "https://...", prompt: "A sunset..." }
    ]}
    isGenerating={false}
    columns={2}
/>
```

**Props:**
- `onGenerate`: function (receives { prompt, aspectRatio, style })
- `images`: list of image objects
- `isGenerating`: boolean (default: false)
- `columns`: number (default: 2)

**Image Object:**
```flin
{
    url: text,
    prompt: text
}
```

**Features:**
- Multi-line prompt input
- Aspect ratio selection: Square (1:1), Portrait (3:4), Landscape (4:3)
- Style presets: Realistic, Artistic, Minimal, Vivid
- Generate button with loading state
- Responsive image grid
- Hover overlays showing prompts

---

## AIVoiceInput.flin

Speech-to-text input with recording visualization.

```flin
<AIVoiceInput
    onTranscript={(text) => handleTranscript(text)}
    placeholder="Click to start recording"
    language="en-US"
    showTranscript={true}
/>
```

**Props:**
- `onTranscript`: function (receives transcript text)
- `placeholder`: text (default: "Click to start recording")
- `language`: text (default: "en-US")
- `showTranscript`: boolean (default: true)

**Features:**
- Record button (🎙️/⏸️ emoji toggle)
- Pulse animation when recording
- Real-time audio visualization (20 bars)
- Live transcript display
- Clear button
- Recording status indicator

---

## Additional Generation Components

### AIFormGenerator.flin
Dynamic form generation from natural language prompts.

### AITableGenerator.flin
Table generation from data descriptions.

### AIChartGenerator.flin
Chart generation with multiple chart types.

*(See existing chat components documentation above for full details)*

---

# AI Analysis Components (2 Total)

Document analysis and agent monitoring.

## AIDocumentSummary.flin
Document analysis with key points, sentiment, and entities.

## AIAgentStatus.flin
Real-time agent monitoring with logs and metrics.

*(See existing chat components documentation above for full details)*

---

# Design Tokens Reference

All components use **100% design tokens** (zero hardcoded values).

## Color Tokens
```css
/* Backgrounds */
--flin-bg-deep: #0a0a0f
--flin-bg-surface: #12121a
--flin-bg-elevated: #1a1a25
--flin-bg-hover: #22222f

/* Text */
--flin-text-primary: #f5f5f7
--flin-text-secondary: #a0a0b0
--flin-text-muted: #606070

/* Accents */
--flin-accent-gold: #d4a853
--flin-accent-gold-bright: #f5d78e
--flin-accent-gold-muted: rgba(212, 168, 83, 0.2)
--flin-accent-violet: #8b5cf6
--flin-accent-cyan: #22d3ee
--flin-accent-emerald: #34d399
--flin-accent-rose: #f472b6

/* Borders */
--flin-border-subtle: rgba(255, 255, 255, 0.06)
--flin-border-medium: rgba(255, 255, 255, 0.1)
```

## Typography Tokens
```css
--flin-font-body: 'Outfit', sans-serif
--flin-font-mono: 'JetBrains Mono', monospace
--flin-font-bold: 700
--flin-text-xs: 0.75rem
--flin-text-sm: 0.875rem
--flin-text-base: 1rem
--flin-text-lg: 1.125rem
--flin-text-xl: 1.25rem
--flin-text-2xl: 1.5rem
--flin-leading-tight: 1.25
--flin-leading-relaxed: 1.625
```

## Spacing Tokens
```css
--flin-space-1: 0.25rem
--flin-space-2: 0.5rem
--flin-space-3: 0.75rem
--flin-space-4: 1rem
--flin-space-6: 1.5rem
--flin-space-8: 2rem
```

## Other Tokens
```css
--flin-radius-sm: 0.125rem
--flin-radius-md: 0.375rem
--flin-radius-lg: 0.5rem
--flin-radius-badge: 100px
--flin-radius-card: 20px
--flin-transition-fast: 150ms cubic-bezier(0.4, 0, 0.2, 1)
--flin-transition-normal: 200ms cubic-bezier(0.4, 0, 0.2, 1)
--flin-ease-out: cubic-bezier(0, 0, 0.2, 1)
```

---

# Component Line Counts

| Component | Lines | Category |
|-----------|-------|----------|
| AIDocumentSummary | 428 | Analysis |
| AIAgentStatus | 422 | Analysis |
| AITableGenerator | 405 | Generation |
| AIFormGenerator | 371 | Generation |
| AIChartGenerator | 352 | Generation |
| AIImageGenerator | 294 | Generation |
| AIVoiceInput | 269 | Generation |
| AIPromptInput | 244 | Interaction |
| AIPromptLibrary | 227 | Interaction |
| AIToolCall | 227 | Tools |
| AICodeBlock | 201 | Tools |
| AILoadingState | 201 | Interaction |
| AIResponseCard | 197 | Interaction |
| AIFeedbackButtons | 197 | Interaction |
| AIMarkdownRenderer | 187 | Tools |
| AIChatbot | 149 | Chat |
| *+ 9 chat components* | ~800 | Chat |
| **TOTAL** | **~5,200** | **26 components** |

---

**Built with FLIN** — É flîn nù (It remembers things)
