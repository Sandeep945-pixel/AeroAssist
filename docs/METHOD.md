# Method and prompt composition

## What RDR contributes

Guided Reflective Diagnostic Reasoning organizes an inference request into four stages: independent observations, cross-modal synthesis and self-critique, structured reporting, and a concise summary. Its purpose is to make the requested analytical process explicit when applying a general multimodal model to aircraft-maintenance examples.

The approach changes the prompt and in-context examples. It does not introduce new model weights, a new multimodal encoder, or an independently trained fusion network.

## Input assembly

A case consists of a video with embedded audio, a sensor-data string, and a question or task instruction. The source uploads the test video through the Gemini file API and waits for processing before requesting a response.

Sensor logs are included as text. Their timestamps provide a basis for comparison with observations in the video, but the source does not implement a separate synchronization or signal-alignment algorithm.

## Zero-shot and few-shot paths

The zero-shot section supplies the four-stage instruction, inline sensor readings, and an uploaded video.

The few-shot path uses `build_final_prompt(...)` to concatenate:

1. RDR instructions.
2. Example filenames, sensor logs, and reference reports.
3. The test filename, test sensor readings, and final task.
4. An instruction to return a single JSON object.

The final `analyze_turbine_video(...)` call sends that text and the uploaded test-video object to the model. Example filenames appear in the prompt, but the demonstration videos themselves are not uploaded by this function. A filename in a text prompt does not give the model access to the file.

## Output contract

The final few-shot instruction requests the following top-level structure:

```json
{
  "phase1_analysis": {},
  "phase2_synthesis": {},
  "phase3_formal_report": {},
  "phase4_executive_summary": ""
}
```

This is a schematic structure, not a model output or a formal JSON Schema. The source returns response text and does not validate the response against a schema. Some embedded example reports also mix prose and JSON, so format compliance should be checked before downstream use.

The zero-shot prompt separately requests a report and a summary; it does not enforce the same single-object contract as the final few-shot instruction.

## Interpreting the figures

The README's architecture image is Figure 1 of the supplied paper; the multimodal input illustration is Figure 5. Both are retained unchanged.

The architecture figure includes the name “AeroQwen” inside the prompt. That is a persona string in the historical source, not evidence that Qwen is the model backend. The API calls use Gemini model identifiers.

The input figure shows how video, audio, and sensor readings are presented together. The paper describes semi-synthetic sensor traces; the image should not be interpreted as proof of independently measured, synchronized aircraft telemetry.

## Evaluation boundaries

The paper studies whether examples improve the requested analysis and report quality. It also reports perceptual failures that prompting did not consistently resolve. Structured explanations and self-reported confidence are generated outputs, not independent verification of a diagnosis.

The experiment relies on semi-synthetic cases and model-assisted reference generation and scoring. Independent assessment by qualified maintenance professionals and broader real-world data would be needed to establish operational usefulness.

[Back to AeroAssist](../README.md)
