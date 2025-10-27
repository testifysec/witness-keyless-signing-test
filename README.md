# Witness Keyless Signing Test

This repository tests keyless code signing with [Witness](https://github.com/in-toto/witness) using:
- **Fulcio** - Certificate authority for code signing certificates based on OIDC identity
- **TSA** - Timestamp Authority for RFC 3161 timestamps

## What This Tests

The GitHub Actions workflow in `.github/workflows/test-witness-signing.yaml`:

1. Installs the witness CLI
2. Creates a test artifact
3. Runs witness with keyless signing configured to use:
   - GitHub Actions OIDC token as identity
   - Fulcio instance at `https://fulcio.testifysec-demo.xyz` for certificates
   - TSA instance at `https://tsa.testifysec-demo.xyz` for timestamps
4. Uploads the generated attestation as a workflow artifact

## Infrastructure

This test validates the Judge platform deployment with:
- GitHub Actions OIDC issuer configured in Fulcio
- Istio service mesh integration for TSA
- End-to-end keyless signing workflow

## Running the Test

The workflow runs automatically on:
- Push to `main` branch
- Pull requests to `main` branch
- Manual trigger via `workflow_dispatch`

To trigger manually:
1. Go to the "Actions" tab
2. Select "Test Witness Keyless Signing"
3. Click "Run workflow"

## Expected Results

A successful run should:
- ✅ Install witness CLI
- ✅ Create test artifact
- ✅ Generate signed attestation using Fulcio certificate
- ✅ Include TSA timestamp in attestation
- ✅ Upload attestation as workflow artifact

## Troubleshooting

If the workflow fails:
1. Check that Fulcio is accessible at `https://fulcio.testifysec-demo.xyz`
2. Check that TSA is accessible at `https://tsa.testifysec-demo.xyz`
3. Verify GitHub Actions OIDC issuer is configured in Fulcio
4. Check workflow logs for specific error messages
