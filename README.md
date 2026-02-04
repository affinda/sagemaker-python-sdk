# SageMaker Python SDK (Affinda Fork)

This is a fork of [AWS's SageMaker Python SDK](https://github.com/aws/sagemaker-python-sdk) with additional features for local mode.

## Fork-Specific Features

This fork adds two features to `src/sagemaker/local/image.py`:

1. **Nvidia GPU Driver Support** - Explicitly specifies the nvidia driver for GPU containers in local mode
2. **SM_SUBNET Environment Variable** - Allows setting a custom Docker network subnet via the `SM_SUBNET` environment variable, useful when the default `sagemaker-local` Docker network subnet conflicts with existing network configurations

## Installation

```bash
pip install git+https://github.com/affinda/sagemaker-python-sdk.git@v2.257.0
```

## Updating to a Newer Upstream Version

When AWS releases a new version and you need to update this fork:

### 1. Add AWS as upstream remote (first time only)

```bash
git remote add upstream https://github.com/aws/sagemaker-python-sdk.git
```

### 2. Fetch upstream tags

```bash
git fetch upstream --tags
```

### 3. Reset the branch to the desired AWS version

```bash
git checkout feat/affinda-updates
git reset --hard v<NEW_VERSION>
```

### 4. Cherry-pick the two custom commits

```bash
git cherry-pick af73a2af  # nvidia gpu support
git cherry-pick e1b0c0ec  # SM_SUBNET support
```

If there are conflicts, resolve them and run `git cherry-pick --continue`.

### 5. Update the version tag

```bash
git tag -f v<NEW_VERSION>
```

### 6. Force push the updated branch and tag

```bash
git push --force origin feat/affinda-updates
git push --force origin v<NEW_VERSION>
```

## Branch Structure

- `feat/affinda-updates` - Main branch with custom commits on top of AWS releases
- `master` - Not actively used

## Original Documentation

For the full SageMaker Python SDK documentation, see the [upstream repository](https://github.com/aws/sagemaker-python-sdk) and [Read the Docs](https://sagemaker.readthedocs.io).
