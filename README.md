# Password Generator

A versatile command-line tool for generating strong, random, and memorable passwords.

## Requirements

- Python 3.6+
- `pyperclip` (for clipboard functionality)

## Installation

1.  **Clone the repository or download the script `pass_standalone.py`.**
2.  **Install dependencies:**
    ```bash
    pip install pyperclip
    ```
3.  **Make the script executable (on macOS and Linux):**
    ```bash
    chmod +x pass_standalone.py
    ```
    Now you can run it with `./pass_standalone.py`. For ease of use, you can move it to a directory in your `PATH`, for example: `sudo mv pass_standalone.py /usr/local/bin/passgen`

## Usage

The script has two main commands: `random` and `memorable`.

### Generating a Random Password

Generates a password of a specified length from a mix of character types. By default, the generated password is automatically copied to your clipboard.

**Command:**
```bash
./pass_standalone.py random [OPTIONS]
```

**Examples:**

- **Generate a default 16-character password:**
  ```bash
  ./pass_standalone.py random
  ```

- **Generate a 24-character password:**
  ```bash
  ./pass_standalone.py random -l 24
  ```

- **Generate a password with no symbols and don't copy it to the clipboard:**
  ```bash
  ./pass_standalone.py random --no-symbols -nc
  ```

- **Generate 5 passwords:**
  ```bash
  ./pass_standalone.py random -c 5
  ```

### Generating a Memorable Password

Creates a password from a list of words, with transformations to enhance security. By default, the generated password is automatically copied to your clipboard.

**Command:**
```bash
./pass_standalone.py memorable [OPTIONS]
```

**Examples:**

- **Generate a default memorable password:**
  ```bash
  ./pass_standalone.py memorable
  ```

- **Generate a password with 4 words, 2 numbers, and 2 symbols:**
  ```bash
  ./pass_standalone.py memorable -w 4 -n 2 -S 2
  ```

- **Generate a password with random capitalization and full leetspeak:**
  ```bash
  ./pass_standalone.py memorable -C random -L all
  ```

- **Generate a password with a minimum length of 20 and a maximum of 25:**
  ```bash
  ./pass_standalone.py memorable -m 20 -M 25
  ```

## All Options

### Common Options

| Option | Short | Description | Default |
|---|---|---|---|
| `--count` | `-c` | Number of passwords to generate. | 1 |
| `--no-copy` | `-nc` | Do not copy the password to the clipboard. | Copy is default |
| `--mask` | | Mask the password in the terminal. | |

### `random` Command Options

| Option | Short | Description | Default |
|---|---|---|---|
| `--length` | `-l` | Length of the password. | 16 |
| `--no-uppercase` | | Exclude uppercase letters. | |
| `--no-lowercase` | | Exclude lowercase letters. | |
| `--no-numbers` | | Exclude numbers. | |
| `--no-symbols` | | Exclude symbols. | |

### `memorable` Command Options

| Option | Short | Description | Default |
|---|---|---|---|
| `--num-words` | `-w` | Number of words to combine. | 2 |
| `--min-length` | `-m` | Minimum password length. | 0 |
| `--max-length` | `-M` | Maximum password length. | 0 |
| `--num-numbers` | `-n` | Number of numbers to include. | 2 |
| `--num-symbols` | `-S` | Number of symbols to include. | 2 |
| `--capitalization`| `-C` | Capitalization style (`none`, `first`, `random`). | `first` |
| `--leet` | `-L` | Leetspeak level (`none`, `some`, `all`). | `some` |
