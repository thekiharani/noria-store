# `noria-store`

Configurable object storage client for S3-compatible providers, with first-class support for AWS S3 and Cloudflare R2.

## Install

```bash
pip install noria-store
```

## Quick Start

```python
from noria_store import StorageClient

storage = StorageClient(
    bucket="documents",
    region="eu-west-1",
    key_prefix="tenant-a",
    public_base_url="https://cdn.example.com",
)

result = storage.put_object(
    key=["invoices", "march-2026.pdf"],
    body=b"hello",
    content_type="application/pdf",
    metadata={"source": "admin"},
)

upload = storage.create_presigned_upload_url(
    key=["uploads", "avatar.png"],
    content_type="image/png",
)
```

## Features

- one API for AWS S3 and Cloudflare R2
- direct object operations and presigned URL generation
- public URL derivation with sensible defaults and override hooks
- constructor-level defaults for metadata, tags, content headers, and TTLs
- raw boto client overrides when lower-level options are needed
- injectable boto client and presigner hooks for advanced control

## Main Exports

```python
from noria_store import (
    StorageClient,
    StorageError,
    create_storage_client,
    join_storage_key,
)
```

## Testing

```bash
uv sync --extra dev
uv run pytest
```
