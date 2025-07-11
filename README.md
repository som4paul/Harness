# OphthaAI

OphthaAI is a containerized web application for ophthalmology image analysis.

## Architecture

```mermaid
flowchart TD
  U[User Upload Interface]
  subgraph Ingestion
    U -->|Upload DICOM/JPEG/PNG| S[Laravel Preprocessor Service]
    S --> E[CLIP Embedding Service]
    S --> V[GPT-4 Vision Service]
  end
  subgraph Storage & Index
    E --> VecDB[(Vector DB)]
    V --> VecDB
    S --> PG[(PostgreSQL)]
  end
  subgraph Application
    VecDB --> FE[Next.js UI Container]
    PG --> BE[Laravel API Container]
    FE --> Chat[GPT-4 Chat]
    FE --> Viz[Visualization Engine]
  end
  subgraph Integrations
    Chat --> EMR[EMR/EHR Systems]
    Viz --> Report[Auto-Report Generator]
  end
```

## Development

1. Copy `.env.example` to `.env` and adjust credentials.
2. Build and start containers:

```bash
docker-compose up --build
```

The frontend will be available on `http://localhost:3000` and backend on `http://localhost:8000`.
