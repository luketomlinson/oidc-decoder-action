# OIDC Token Decoder Action

A GitHub Action that fetches and decodes GitHub Actions OIDC (OpenID Connect) tokens, displaying the JWT header, payload claims, and key metadata. Useful for debugging and understanding OIDC token contents in your workflows.

## Features

- Fetches an OIDC token from GitHub's token endpoint
- Decodes and displays the JWT header and payload
- Writes decoded token contents to the GitHub Step Summary
- Outputs decoded header and payload as JSON for use in subsequent steps
- Displays key claims analysis including issuer, subject, audience, repository info, and timestamps

## Usage

```yaml
name: Decode OIDC Token

on:
  workflow_dispatch:

permissions:
  id-token: write
  contents: read

jobs:
  decode:
    runs-on: ubuntu-latest
    steps:
      - name: Decode OIDC Token
        id: oidc
        uses: luketomlinson/oidc-decoder-action@main

      - name: Use decoded token
        run: |
          echo "Header: ${{ steps.oidc.outputs.header }}"
          echo "Payload: ${{ steps.oidc.outputs.payload }}"
```

## Permissions

This action requires the `id-token: write` permission to fetch an OIDC token:

```yaml
permissions:
  id-token: write
  contents: read
```

## Outputs

| Output    | Description                     |
|-----------|---------------------------------|
| `header`  | Decoded JWT header as JSON      |
| `payload` | Decoded JWT payload as JSON     |
