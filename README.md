# DIS21a 1 - BIG DATA

## Setup

1. Setup and activate your virtual environment

    ```bash
    python3 -m venv .venv
    source .venv/Scripts/activate
    ```

2. Install requirements

    ```bash
    pip install -r requirements.txt
    ```

3. Setup VSCode

    1. Download JQ (flexible command-line JSON processor) from [here](https://github.com/stedolan/jq/releases/download/jq-1.6/jq-win64.exe)
    2. Create the following Folder: `C:\Program Files\jq`
    3. Add the following line to your PATH environment variable: `C:\Program Files\jq`
    4. Rename the downloaded JQ file to `jq.exe` and move it to the previously created folder
    5. Add the following lines to your .gitconfig file (usually found in C:\Users\YOUR_USERNAME\.gitconfig)

        ```bash
        [core]
            attributesfile = ~/.gitattributes_global
        [filter "nbstrip_meta"]
            clean = "jq --indent 4 \
                    '(.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
                    | .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
                    | .cells[].metadata = {} \
                    '"
            smudge = cat
            required = true
        [filter "nbstrip_full"]
            clean = "jq --indent 4 \
                    '(.cells[] | select(has(\"outputs\")) | .outputs) = []  \
                    | (.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
                    | .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
                    | .cells[].metadata = {} \
                    '"
            smudge = cat
            required = true
        ```

    6. Create a `.gitattributes_global` file at the same location as your `.gitconfig` file and add the following lines:

        ```bash
        *.ipynb filter=nbstrip_meta
        ```
