# Bonyan llm

# AI Editor Setup for Bonyan

[bonyan.snappfood.dev/llm-bonyan.txt](https://bonyan.snappfood.dev/llm-bonyan.txt) file is a compact, text version of Bonyan docs to help AI generate accurate Bonyan code based on your prompt.

This guide shows you how to setup Bonyan documentation in popular AI-powered editors like Cursor and VSCode.

## Quick Use

### Cursor

In chat window type this and Cursor will use Bonyan's llm.txt file to generate code:

```md
@web https://bonyan.snappfood.dev/llm-bonyan.txt
```

### VSCode

In chat window type this and VSCode will use Bonyan's llm.txt file to generate code:

```md
#fetch https://bonyan.snappfood.dev/llm-bonyan.txt
```

## Editor-Specific Setup

### Cursor Setup

#### Custom Docs Integration

1. Press `⌘ CMD` + `⇧ Shift` + `P` (or `⌃ Ctrl` + `⇧ Shift` + `P` on Windows)
2. Type `Add new custom docs`
3. Add this URL:
   ```md
   https://bonyan.snappfood.dev/llm-bonyan.txt
   ```
4. Now in chat window you can type `@docs` and choose `Bonyan` to provide Bonyan docs to Cursor

#### Project-level Rules Setup

You can setup Bonyan's llm-bonyan.txt file to your repo so Cursor can use it by default. ([Read more at Cursor docs](https://docs.cursor.com/context/rules))

Run this command to save the llm-bonyan.txt file to `.cursor/rules/bonyan.mdc`:

```sh
curl -L https://bonyan.snappfood.dev/llm-bonyan.txt --create-dirs -o .cursor/rules/bonyan.mdc
```

### VSCode Setup

#### Copilot Integration

You can setup Bonyan's llm-bonyan.txt file to your repo so Copilot can use it by default. ([Read more at VSCode docs](https://code.visualstudio.com/docs/copilot/copilot-customization))

1. Run this command to save the llm-bonyan.txt file to `.vscode/bonyan.md`:

   ```sh
   curl -L https://bonyan.snappfood.dev/llm-bonyan.txt --create-dirs -o .vscode/bonyan.md
   ```

2. In `.vscode/settings.json` add this configuration:
   ```json
   {
     "github.copilot.chat.codeGeneration.instructions": [
       {
         "file": "./.vscode/bonyan.md"
       }
     ]
   }
   ```

## MCP Server Setup

MCP (Model Context Protocol) is an API to communicate with AI models. You can add MCP servers and your editor will communicate with them to get more accurate results.

We recommend using [Context7](https://context7.com/) [MCP server](https://github.com/upstash/context7-mcp) which provides many libraries including Bonyan.

### Cursor MCP Setup

1. Go to Cursor settings: `⌘ CMD` + `⇧ Shift` + `J` (or `⌃ Ctrl` + `⇧ Shift` + `J` on Windows)
2. Click `MCP` from the left sidebar
3. Click `Add new global MCP server`
4. Add this configuration:

   ```json
   {
     "mcpServers": {
       "Context7": {
         "type": "stdio",
         "command": "npx",
         "args": ["-y", "@upstash/context7-mcp@latest"]
       }
     }
   }
   ```

### VSCode MCP Setup

1. Go to MCP settings in VSCode: [`vscode://settings/mcp`](vscode://settings/mcp)
2. Click `Edit in settings.json`
3. Add this configuration:

   ```json
   {
     "mcp": {
       "servers": {
         "Context7": {
           "type": "stdio",
           "command": "npx",
           "args": ["-y", "@upstash/context7-mcp@latest"]
         }
       }
     }
   }
   ```

## Usage Examples

Once you have MCP setup, you can ask AI anything about Bonyan in `Agent Mode` by adding `use context7` at the end of your prompt.

For example:

```md
Create a Button component with primary variant in Bonyan. use context7
```

```md
Write a Tab component with 3 items using Bonyan. use context7
```

```md
Show me how to create a responsive Card layout with Bonyan. use context7
```
