# Multi-Session LLM Runner

A sleek, client-side web application that lets you run multiple LLM sessions in parallel using the OpenRouter API, compare outputs side-by-side, and iterate quickly without ever sending your API key to a server.

## Description

The Multi-Session LLM Runner is designed for rapid exploration and comparison of LLM outputs. Whether you're brainstorming ideas, testing prompts, or comparing model performance, this tool lets you fire the same prompt to multiple parallel sessions and view all responses in one organized interface.

Key benefits:
- **Parallel execution**: Run up to 10 sessions simultaneously for instant comparison
- **Client-side security**: Your OpenRouter API key never leaves your browser
- **Session management**: Track progress, filter by status, and focus on individual results
- **Append mode**: Compare results across multiple runs without losing previous sessions
- **Template support**: Quick-start with common prompt patterns
- **Error handling**: Robust retry logic with exponential backoff for rate limits

## Features

- ✅ **Zero server dependency** - Everything runs in your browser
- ✅ **Parallel session execution** - Run multiple LLM calls simultaneously  
- ✅ **Session filtering** - View all, completed, or errored sessions
- ✅ **Template prompts** - Pre-built templates for common use cases
- ✅ **Append mode** - Accumulate sessions across multiple runs
- ✅ **Real-time status tracking** - Live updates as sessions complete
- ✅ **Error resilience** - Automatic retry with exponential backoff
- ✅ **Responsive design** - Works on desktop, tablet, and mobile
- ✅ **Dark theme** - Modern, accessible UI with smooth animations

## Tech Stack

- **HTML5** - Semantic markup and modern web standards
- **CSS3** - Custom properties, Grid/Flexbox layout, smooth animations
- **Vanilla JavaScript ES2022** - Modern async/await patterns, fetch API
- **OpenRouter API** - Access to 100+ LLM models
- **Client-side only** - No backend required

## File Structure

```
multi-session-llmRunner.html
```

The entire application is contained in a single HTML file:

- **`<head>`** - CSS styles with custom properties for theming
- **`<body>`** - Application interface with two-panel layout
- **`<script>`** - Core logic for API calls, session management, and UI updates
- **CSS grid layout** - Responsive design that adapts to screen size
- **Event-driven UI** - Real-time updates as sessions progress

## Getting Started

### Prerequisites

- Modern web browser (Chrome, Firefox, Safari, Edge)
- OpenRouter API key (free at [openrouter.ai](https://openrouter.ai/keys))
- Internet connection

### Installation

No installation required! Simply:

1. Download the `multi-session-llmRunner.html` file
2. Open it in any modern web browser
3. Start using immediately - no server setup needed

### Browser Security Note

For the application to work properly with OpenRouter's API, you may need to:
- Use a browser that allows `fetch()` requests to external APIs
- Ensure your browser isn't blocking CORS requests
- Consider using a local HTTP server if opening the file directly fails

## Usage

### Basic Operation

1. **Enter your API key** in the OpenRouter API Key field
2. **Write or select a prompt** - either type your own or choose from templates
3. **Configure settings**:
   - Number of sessions (1-10)
   - Model ID (e.g., "anthropic/claude-3-haiku")
   - Temperature (0.0-2.0)
4. **Click "Run Sessions"** to start parallel execution

### Advanced Features

#### Templates
Quick-start with pre-built prompts:
```javascript
// Available templates:
"brainstorm-ideas"  // 10 creative ideas for any topic
"summarize"         // Clear, concise summary
"cold-email"        // Short, direct outreach email  
"code-review"       // Code analysis and improvement suggestions
```

#### Append Mode
Enable "Append sessions" to accumulate results across multiple runs:
```javascript
// First run: sessions 0-2
// Second run with append: sessions 3-5 (original 0-2 preserved)
// Great for iterative experimentation and comparison
```

#### Session Management
- **Filter sessions** by clicking "All", "Done", or "Error"
- **Click any session** to view its full response in the detail panel
- **Real-time status** shows pending, completed, or failed sessions

### API Integration

The app uses OpenRouter's standard chat completions endpoint:

```javascript
const payload = {
  model: "your-model-id",
  messages: [
    { role: "system", content: `You are session #${index}` },
    { role: "user", content: prompt }
  ],
  temperature: 0.7
};

const response = await fetch("https://openrouter.ai/api/v1/chat/completions", {
  method: "POST",
  headers: {
    "Authorization": `Bearer ${apiKey}`,
    "Content-Type": "application/json",
    "HTTP-Referer": window.location.href
  },
  body: JSON.stringify(payload)
});
```

### Error Handling

The app includes robust error handling:
- **Rate limit retries** with exponential backoff
- **Network error recovery** 
- **Detailed error messages** for debugging
- **Graceful degradation** when sessions fail

### Example Workflows

#### A/B Testing Prompts
1. Run 3 sessions with your original prompt
2. Enable append mode
3. Modify the prompt and run 3 more sessions
4. Compare all 6 responses side-by-side

#### Model Comparison
1. Set session count to 2
2. Run with "openai/gpt-3.5-turbo"
3. Enable append mode  
4. Change model to "anthropic/claude-3-haiku"
5. Run again and compare outputs

#### Brainstorming Sessions
1. Select the "Brainstorm ideas" template
2. Enter your topic
3. Run 5-10 sessions for diverse idea generation
4. Review and filter results

## Security

- **Zero data persistence** - Nothing is stored locally or remotely
- **Client-side only** - API key never leaves your browser
- **Secure headers** - Includes required OpenRouter attribution headers
- **No analytics** - No tracking or telemetry

## Browser Compatibility

- ✅ Chrome 90+
- ✅ Firefox 88+  
- ✅ Safari 14+
- ✅ Edge 90+
- ⚠️ May need local HTTP server for file:// protocol

## Contributing

This is a standalone client-side application. To modify:

1. Edit the HTML file directly
2. Test in your browser
3. No build process required

Key areas for customization:
- **Templates**: Modify `getTemplatePrompt()` function
- **Styling**: Update CSS custom properties in `:root`
- **Session limits**: Adjust max sessions in validation
- **Models**: Pre-populate common model IDs

## License

This is a personal tool provided as-is. Feel free to use, modify, and distribute.

## Support

For issues:
1. Check browser console for errors
2. Verify your OpenRouter API key
3. Ensure your browser allows external fetch requests
4. Try using a local HTTP server instead of file://

For feature requests or questions, the code is fully visible and modifiable in the single HTML file.