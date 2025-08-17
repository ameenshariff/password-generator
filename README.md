# Advanced Password Generator

This script generates strong, random, and memorable passwords using Python's `secrets` module for cryptographic security. It offers two main modes: generating completely random strings and creating memorable passwords from a wordlist, with various options for customization.

## Features

- **Two Password Modes:**
  - `random`: Generates a password of a specified length with a mix of uppercase letters, lowercase letters, numbers, and symbols.
  - `memorable`: Creates a password by combining words from a built-in list, with options for capitalization, leetspeak substitutions, and the inclusion of numbers and symbols.
- **Cryptographically Secure:** Uses the `secrets` module to ensure that generated passwords are unpredictable and suitable for long-term security.
- **Customizable:** Allows for detailed control over the password's structure, including length, character types, word count, and more.
- **Clipboard Integration:** Can automatically copy the generated password to the clipboard for immediate use (requires `pyperclip`).
- **Masking:** Can hide the password output in the terminal for privacy.

## Requirements

- Python 3.6+
- `pyperclip` (optional, for clipboard functionality)

## Installation

1. **Clone the repository or download the script.**
2. **(Optional) Install `pyperclip`:**
   For the `--copy` feature to work, you need to install the `pyperclip` library. You can do this using pip:
   ```bash
   pip install pyperclip
   ```

## Making the Script Executable

To make the script easier to run, you can make it executable.

### For macOS and Linux:

In your terminal, run the following command to give the script execute permissions:

```bash
chmod +x pass_standalone.py
```

After this, you can run the script directly:

```bash
./pass_standalone.py random
```

### For Windows:

On Windows, Python scripts can be run directly if the `.py` file extension is associated with the Python interpreter. If you installed Python from the official installer, this is usually done automatically. You can run the script from the command prompt as follows:

```bash
python pass_standalone.py random
```

## Running from Anywhere

To run the script from any directory without specifying the full path, you can add it to your system's `PATH`.

### For macOS and Linux:

1.  **Choose a directory in your `PATH`.** A common choice is `/usr/local/bin`.
2.  **Move the script** to that directory. It's a good practice to rename it to something simpler, like `passgen`.

    ```bash
    sudo mv pass_standalone.py /usr/local/bin/passgen
    ```

3.  **Now you can run the script from anywhere:**

    ```bash
    passgen random -l 20
    ```

### For Windows:

1.  **Create a folder** to store your scripts (e.g., `C:\Scripts`).
2.  **Move `pass_standalone.py`** to this folder.
3.  **Add the folder to your `PATH`:**
    -   Search for "Environment Variables" in the Start Menu and select "Edit the system environment variables."
    -   Click the "Environment Variables..." button.
    -   Under "System variables," find and select the `Path` variable, then click "Edit..."
    -   Click "New" and add the path to your scripts folder (e.g., `C:\Scripts`).
    -   Click "OK" to close all windows.
4.  **Restart your command prompt.** You can now run the script from any directory:

    ```bash
    python pass_standalone.py memorable
    ```

## Usage

The script is run from the command line and uses sub-commands to select the password generation mode.

### Basic Commands

- To see the help message:
  ```bash
  pass_standalone.py --help
  ```
- To see the help message for a specific command (e.g., `random`):
  ```bash
  pass_standalone.py random --help
  ```

### Generating a Random Password

The `random` command generates a password from a mix of character types.

**Command:**
```bash
pass_standalone.py random [OPTIONS]
```

**Options:**

| Option | Short | Description | Default |
|---|---|---|---|
| `--length` | `-l` | Length of the password. | 16 |
| `--no-uppercase` | | Exclude uppercase letters. | |
| `--no-lowercase` | | Exclude lowercase letters. | |
| `--no-numbers` | | Exclude numbers. | |
| `--no-symbols` | | Exclude symbols. | |
| `--count` | `-c` | Number of passwords to generate. | 1 |
| `--copy` | | Copy the password to the clipboard. | |
| `--mask` | | Mask the password in the terminal. | |

**Examples:**

- **Generate a default 16-character password:**
  ```bash
  pass_standalone.py random
  ```

- **Generate a 24-character password and copy it to the clipboard:**
  ```bash
  pass_standalone.py random -l 24 --copy
  ```

- **Generate a password with no symbols:**
  ```bash
  pass_standalone.py random --no-symbols
  ```

- **Generate 5 passwords at once:**
  ```bash
  pass_standalone.py random -c 5
  ```

### Generating a Memorable Password

The `memorable` command creates a password from a list of words, with various transformations to enhance security.

**Command:**
```bash
pass_standalone.py memorable [OPTIONS]
```

**Options:**

| Option | Short | Description | Default |
|---|---|---|---|
| `--num-words` | `-w` | Number of words to combine. | 2 |
| `--min-length` | | Minimum password length. | 0 |
| `--max-length` | | Maximum password length. | 0 |
| `--num-numbers` | `-n` | Number of numbers to include. | 2 |
| `--num-symbols` | `-S` | Number of symbols to include. | 2 |
| `--capitalization`| `-C` | Capitalization style (`none`, `first`, `random`). | `first` |
| `--leet` | `-L` | Leetspeak level (`none`, `some`, `all`). | `some` |
| `--count` | `-c` | Number of passwords to generate. | 1 |
| `--copy` | | Copy the password to the clipboard. | |
| `--mask` | | Mask the password in the terminal. | |

**Examples:**

- **Generate a default memorable password:**
  ```bash
  pass_standalone.py memorable
  ```

- **Generate a password with 4 words, 2 numbers, and 2 symbols:**
  ```bash
  pass_standalone.py memorable -w 4 -n 2 -S 2
  ```

- **Generate a password with random capitalization and full leetspeak:**
  ```bash
  pass_standalone.py memorable -C random -L all
  ```

- **Generate a password with a minimum length of 20 characters:**
  ```bash
  pass_standalone.py memorable --min-length 20
  ```

## How It Works

### Random Passwords

The `random` password generator creates a character set based on the user's choices (uppercase, lowercase, numbers, symbols). It then uses `secrets.choice` to select characters from this set until the desired password length is reached. This ensures that each character is chosen with equal probability from the allowed set, resulting in a non-biased, unpredictable password.

### Memorable Passwords

The `memorable` password generator follows a more complex process:

1. **Word Selection:** It randomly selects the specified number of words from a large, built-in wordlist.
2. **Capitalization:** It applies capitalization rules (`none`, `first` letter of each word, or `random` capitalization throughout).
3. **Leetspeak:** It substitutes letters with numbers and symbols based on the chosen leetspeak level (`none`, `some` substitutions, or `all` possible substitutions).
4. **Numbers and Symbols:** It generates the specified number of random digits and symbols.
5. **Shuffling:** It shuffles the words, numbers, and symbols to create a more complex password. To ensure the password starts with a word, one word is selected to be the first part of the password, and the rest of the parts are shuffled.
6. **Padding and Truncating:** If a minimum length is set, it pads the password with random characters. If a maximum length is set, it truncates the password.

This multi-step process creates passwords that are easier for humans to remember than purely random strings but are still difficult to guess due to the added complexity and randomness.
