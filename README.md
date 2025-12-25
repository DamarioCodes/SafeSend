# SafeSend

SafeSend is a secure file transfer backend that lets users upload files and share time-limited download links.
Files are stored in AWS S3 and shared via short-lived pre-signed URLs so the backend does not directly stream file data.

## MVP Features
- Upload a file and generate a shareable link token
- Download via token with expiration and max-download limits
- Audit logging for download attempts (success/fail + reason)
- Authenticated users can view file metadata and revoke links

## Tech Stack
- Java, Spring Boot (REST API)
- AWS S3 (object storage, pre-signed upload/download)
- PostgreSQL (metadata + audit logs)
- Docker (local dev)
- Swagger / OpenAPI (API docs)

## Architecture (high level)
- Client requests an upload
- API creates a metadata record and returns a pre-signed S3 upload URL
- Client uploads directly to S3
- Client shares a token-based link
- Download requests validate token rules and return a pre-signed S3 download URL

## API Endpoints (planned)
### Auth
- `POST /auth/register`
- `POST /auth/login`

### Files
- `POST /files`  
  Creates a file record and returns a pre-signed upload URL + share token.
- `GET /files/{token}`  
  Validates token rules and returns a pre-signed download URL.
- `GET /files/{id}/metadata`  
  Returns file metadata (owner-only).
- `POST /files/{id}/revoke`  
  Revokes an existing share token (owner-only).

## Local Development
Coming soon.

## Demo
Coming soon.

## Roadmap
- Add rate limiting
- Add background cleanup for expired files
- Add optional malware scan hook / scan status field
