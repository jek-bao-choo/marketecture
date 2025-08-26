# dd-trace-py's ddtrace-run command
![dd-trace-py ddtrace-run command](ddtrace-run.jpeg)

- The Wrapper (ddtrace-run) is the outermost box: It starts first and creates the tracing environment for everything that happens inside it.

- The Runner (uv run) is the middle box: It runs inside the wrapper's environment. Its job is to set up the correct Python virtual environment and context for your application.

- Your App (main.py) is at the core: It runs inside the runner's context, which itself is inside the wrapper's tracing environment.