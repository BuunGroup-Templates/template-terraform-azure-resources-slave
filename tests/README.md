# Terraform Module Tests

This directory contains the main test configurations for this Terraform module, using Terraform's built-in testing framework.

## Test Directory Structure

The `tests/` directory is the central location for all test files. To support modular and organized test development, additional subdirectories may be present:

```
tests/
├── README.md                # This file
├── provider.tf              # Provider configuration for tests
├── variables.tf             # Common variables used across tests
├── defaults.tftest.hcl      # Test cases for default configuration
├── mock-data/               # Mock data used in tests
│   └── main.tf              # Mock resource configurations
├── unit_tests/              # Unit-level test cases (optional)
│   └── ...
├── intergration_tests/      # Integration-level test cases (optional)
│   └── ...
├── examples/                # Example configurations for testing (optional)
│   └── ...
```

## How Tests Are Run in CI

When running tests in CI (GitHub Actions), the workflow automatically copies all files from the following subdirectories into the root of `tests/` **before** running `terraform test`:

- `tests/unit_tests/`
- `tests/intergration_tests/`
- `tests/examples/`

This means any `.tftest.hcl` or other test files placed in these subfolders will be included in the test run. This approach allows you to organize tests by type or source, while ensuring all are executed together.

> **Note:** If files with the same name exist in multiple subfolders, the last one copied will overwrite previous ones in `tests/` during the CI run.

## Running Tests Locally

To run all tests locally (only those already in `tests/` will be picked up):

1. Configure your Azure credentials (environment variables or Azure CLI login)
2. Initialize Terraform:
   ```bash
   terraform init
   ```
3. Run the tests:
   ```bash
   terraform test
   ```

If you want to include tests from `unit_tests/`, `intergration_tests/`, or `examples/` locally, manually copy them into `tests/` before running `terraform test`.

## Test Cases

The test suite may include:

- Default configuration tests (`defaults.tftest.hcl`)
- Unit tests (from `unit_tests/`)
- Integration tests (from `intergration_tests/`)
- Example-based tests (from `examples/`)

## Adding New Tests

1. Create a new `.tftest.hcl` file in `tests/`, `unit_tests/`, `intergration_tests/`, or `examples/`.
2. Define your test cases using the standard test block syntax.
3. Add mock data if needed in the `mock-data` directory.
4. Update this README with details about your new test cases or structure as needed. 