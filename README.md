# gassist_text

A Python library for interacting with Google Assistant API via text

## Credits

Uses <https://pypi.org/project/google-assistant-grpc/>. See instructions there how to get `credentials.json`.

Code is essentially a copy of <https://github.com/googlesamples/assistant-sdk-python/blob/master/google-assistant-sdk/googlesamples/assistant/grpc/textinput.py> wrapped in a package.

## Example

```python
import json
import google.oauth2.credentials
with open('/path/to/credentials.json', 'r') as f:
    credentials = google.oauth2.credentials.Credentials(token=None, **json.load(f))

from gassist_text import TextAssistant
with TextAssistant(credentials) as assistant:
    print(assistant.assist('tell me a joke')[0])
    print(assistant.assist('another one')[0])
```

## Limitations/Known issues

- Most queries return an empty text response. However all return a non empty HTML response.

If you have not registered a device and model:

- Most queries for media controls don't work.
  - not working: e.g. play music on kitchen speaker, stop kitchen speaker
  - working: e.g. play news on kitchen speaker, play rain sounds on bedroom speaker
- Routines don't work
- Queries for personal results don't work

## Development environment

```sh
python3 -m venv .venv
source .venv/bin/activate
# for Windows CMD:
# .venv\Scripts\activate.bat
# for Windows PowerShell:
# .venv\Scripts\Activate.ps1

# Install dependencies
python -m pip install --upgrade pip
python -m pip install flake8 pytest
pip install -r requirements.txt

# Run lint
flake8 gassist_text tests --count --select=E9,F63,F7,F82 --show-source --statistics
flake8 gassist_text tests --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics

# Run tests
pytest

# Run command line interactive tool
python gassist_text/textinput.py
```
