# Hermes OpenRouter Model Catalog

A user-curated model catalog for [Hermes Agent](https://hermes-agent.nousresearch.com/) using the OpenRouter provider.

The catalog is a JSON manifest compatible with Hermes Agent's [model catalog schema](https://hermes-agent.nousresearch.com/docs/reference/model-catalog). It contains a focused set of 19 OpenRouter model IDs across Google, OpenAI, Thinking Machines, Mistral, Meta, and NVIDIA. `openai/gpt-5.6-terra` is the catalog default.

## Contents

- `model-catalog-openrouter.json` — the custom catalog manifest.

## Use locally

Point Hermes at the file with a per-provider override:

```yaml
model_catalog:
  providers:
    openrouter:
      url: file:///absolute/path/to/model-catalog-openrouter.json
```

For this repository after cloning locally, replace `/absolute/path/to` with the repository's actual absolute path. The `file://` URL allows Hermes to load the catalog without hosting it on a web server.

## Important behavior

Hermes validates the JSON manifest, then its OpenRouter picker consults OpenRouter's live model endpoint and filters models that do not currently advertise tool-calling support. As a result, an entry can remain part of this catalog while not appearing in the agent model picker until OpenRouter reports compatible capabilities for it.

## Updating

1. Edit `model-catalog-openrouter.json`.
2. Keep `version` at a schema version supported by Hermes.
3. Ensure every model has a non-empty `id`.
4. Keep exactly one OpenRouter model marked with `"default": true`.
5. Validate JSON before committing:

   ```bash
   python3 -m json.tool model-catalog-openrouter.json >/dev/null
   ```
