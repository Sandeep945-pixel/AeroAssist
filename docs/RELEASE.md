# Repository and setup notes

## What is available

The current repository contains a Colab-exported source file, nine demonstration videos, ten test videos, and a results workbook. Sensor readings and example reports are embedded directly in `main.py`.

The paper describes a larger evaluation set than the ten test videos present here. The workbook's presence alone does not establish a complete, reproducible benchmark release.

## Why the export does not run as a normal script

`main.py` contains notebook shell syntax such as `!pip`, Colab authentication and secret access, a stray standalone video path, repeated setup blocks, and unrelated privacy experiments appended after the aviation workflow. Running `python main.py` is not a supported startup procedure.

This update documents the existing research export. It does not migrate the implementation or execute its API calls.

## Preparing a controlled experiment

1. Extract the aviation workflow into a clean Colab notebook or Python module; omit unrelated experiments and account-debugging cells.
2. Configure your own API access. The original workflow reads a Colab secret named `GOOGLE_API_KEY`; do not reuse the project-specific cloud configuration embedded in the export.
3. Resolve video paths explicitly. Demonstration files live in `Prompt data/`, and test videos live in `test_data/`, while the source often uses bare filenames. The single-shot example also refers to a filename absent from this release.
4. Select a test video and its corresponding sensor readings. Do not pair a different video with the hard-coded sensor trace and treat the result as a reproduced case.
5. Check model availability and SDK compatibility. The export uses `google.generativeai`; the repository has no pinned environment or dependency manifest.
6. Validate the returned response before parsing it or using it in an evaluation. The existing code displays response text without enforcing a JSON schema.

The upload polling loop has no explicit timeout, and uploaded-file cleanup is not implemented. API execution sends the selected video and prompt content to the configured external service and may incur charges.

## Reproduction status

No model calls or cloud-account operations were run during this documentation update. A complete reproduction would require a cleaned execution path, a tested environment, the full case mapping, and the evaluation procedure behind the reported results.

## Media and use

This repository includes research media sourced or generated for the study. Do not infer a blanket redistribution license from their presence. Use the system only for research and human-reviewed demonstrations; generated labels and recommendations are not operational maintenance instructions.

[Back to AeroAssist](../README.md)
