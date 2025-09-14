# nano-ai

## Syntax Highlighting

**Method 1: Enable built-in syntax highlighting**

Most modern nano installations come with syntax highlighting files. Enable them by editing your nano config:

```bash
# Create/edit nano config
nano ~/.nanorc
```

Add these lines:
```bash
# Enable syntax highlighting for all supported files
include "/usr/share/nano/*.nanorc"

# Or on some systems:
# include "/usr/share/nano-syntax-highlighting/*.nanorc"

# Additional settings
set linenumbers
set mouse
set smooth
set tabsize 4
set tabstospaces
```

**Method 2: Install enhanced syntax highlighting**

For better syntax highlighting, install the enhanced collection:
```bash
# Install git if needed
sudo apt install git

# Clone enhanced syntax files
git clone https://github.com/scopatz/nanorc.git ~/.nano

# Add to your .nanorc
echo 'include "~/.nano/*.nanorc"' >> ~/.nanorc
```

**Method 3: Individual language setup**

You can also add specific languages to `~/.nanorc`:
```bash
# Python
include "/usr/share/nano/python.nanorc"

# JavaScript
include "/usr/share/nano/javascript.nanorc"

# HTML
include "/usr/share/nano/html.nanorc"

# CSS
include "/usr/share/nano/css.nanorc"

# JSON
include "/usr/share/nano/json.nanorc"
```

## Enhanced Nano Configuration

Add these useful options to `~/.nanorc`:
```bash
# Visual improvements
set linenumbers
set mouse
set smooth
set softwrap
set tabsize 4
set tabstospaces
set titlecolor brightwhite,red
set statuscolor brightwhite,green
set keycolor brightwhite,blue

# Functionality
set autoindent
set backup
set backupdir "~/.nano/backups"
set historylog
set positionlog
set multibuffer
set regexp
set smarthome

# Search and replace
set casesensitive
set regexp

# Spell checking
set speller "aspell -x -c"
```

## AI Assistance Integration

Since nano doesn't have built-in AI support, here are several approaches:

**Method 1: External AI wrapper script**

Create a script `~/bin/nano-ai`:
```bash
#!/bin/bash
# Save as ~/bin/nano-ai and make executable with chmod +x

TEMP_FILE=$(mktemp)
cp "$1" "$TEMP_FILE" 2>/dev/null || touch "$TEMP_FILE"

while true; do
    nano "$TEMP_FILE"
    
    echo "Options:"
    echo "1) Save and exit"
    echo "2) Get AI help"
    echo "3) Continue editing"
    read -p "Choose (1-3): " choice
    
    case $choice in
        1)
            cp "$TEMP_FILE" "$1"
            rm "$TEMP_FILE"
            break
            ;;
        2)
            echo "Paste your question for AI help:"
            read -p "> " question
            # You can integrate with various AI services here
            # For example, using curl with Claude API or OpenAI
            echo "AI response would appear here..."
            read -p "Press Enter to continue..."
            ;;
        3)
            continue
            ;;
        *)
            echo "Invalid choice"
            ;;
    esac
done
```

**Method 2: Use external AI tools**

Install and use AI command-line tools alongside nano:

```bash
# Install aichat (Rust-based AI CLI)
cargo install aichat

# Or install shell-gpt
pip install shell-gpt

# Or install ollama for local AI
curl -fsSL https://ollama.ai/install.sh | sh
```

Then use them in separate terminal windows or create aliases:
```bash
# Add to ~/.bashrc
alias ask="aichat"
alias code-help="aichat 'Help me with this code:'"
```

**Method 3: Integration with external editors**

Create a script that combines nano with AI:
```bash
#!/bin/bash
# Save as ~/bin/nano-plus

file="$1"
while true; do
    clear
    echo "=== Nano Plus ==="
    echo "1) Edit file"
    echo "2) Ask AI about code"
    echo "3) Generate code with AI"
    echo "4) Exit"
    read -p "Choice: " choice
    
    case $choice in
        1) nano "$file" ;;
        2) 
            echo "Current file content:"
            cat "$file"
            echo -e "\nAsk AI:"
            read question
            # Integrate your preferred AI service here
            ;;
        3)
            echo "Describe what code you want:"
            read description
            # Generate code with AI and append/replace in file
            ;;
        4) break ;;
    esac
done
```

**Method 4: Use tmux for side-by-side workflow**

```bash
# Install tmux
sudo apt install tmux

# Create a session with nano and AI assistant
tmux new-session -d -s coding
tmux split-window -h
tmux send-keys -t 0 "nano myfile.py" C-m
tmux send-keys -t 1 "aichat" C-m
tmux attach-session -t coding
```

## Useful Nano Keybindings

Add these to your workflow:
- `Ctrl+G` - Help
- `Ctrl+X` - Exit
- `Ctrl+O` - Save
- `Ctrl+W` - Search
- `Ctrl+\` - Replace
- `Alt+A` - Select all
- `Ctrl+K` - Cut line
- `Ctrl+U` - Paste
- `Ctrl+T` - Spell check
- `Alt+U` - Undo
- `Alt+E` - Redo

## Alternative: Consider VS Code or Neovim

For better AI integration, you might want to consider:
- **VS Code** with GitHub Copilot or CodeGPT extensions
- **Neovim** with AI plugins like ChatGPT.nvim or copilot.vim

But if you prefer staying with nano, the external script approach works well for occasional AI assistance!
