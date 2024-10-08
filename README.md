# Moshi
This is a demo of the Moshi speech-to-speech model by [Kyutai Labs](https://github.com/kyutai-labs/moshi), hosted on [Modal](modal.com) GPUs, with a command line client for talking to it in realtime.

# Serving the Model
The Moshi model server is a Modal [class](https://modal.com/docs/reference/modal.Cls) app, which loads the model into memory and exposes a websocket endpoint for bidirectional streaming.

The Moshi model is stateful, maintaining an internal chat history as it converses with the user, so only one websocket connection can be active at a time. We ensure a 1:1 mapping of clients to servers by using the `allow_concurrent_inputs = 1` flag in the class decorator.

To run the server, first install the local dependencies:
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Then start the server:
```bash
modal serve src.moshi
```

This will start a temporary dev server in the cloud, at `YOUR_USERNAME--moshi-moshi-app-dev.modal.run`

# Client
The client is found in `client/client.py`.

Install dev dependencies with:
```bash
pip install -r requirements-dev.txt
```

Run the client:
```bash
python client/client.py
```

This will connect to the dev server, and start a conversation.
Press Ctrl+C to exit.
