# Visual Stress-Test Flow

- Request 2 HTML files that mimic screenshots
  - Choose standalone artifact HTML approach
  - Use token-first shadcn semantic structure
  - Build dashboard and modal mockups
  - Tighten visual fidelity in several passes
  - Extract shared primitive token CSS
  - Compare primitives against Tini token library
  - Create CorePVS token pack from Tini values
  - Duplicate HTML files and swap to CorePVS tokens
  - Convert duplicates to support OKLch tokens
  - Compare primitive vs CorePVS look and feel
  - Document gaps, comparison, and flow

```mermaid
flowchart TD
    A[Request 2 screenshot-mimic HTML files] --> B[Choose standalone artifact approach]
    B --> C[Adopt token-first shadcn semantic structure]
    C --> D[Build dashboard and modal HTML artifacts]
    D --> E[Tighten layout and visual fidelity in multiple passes]
    E --> F[Extract shared primitive token CSS]
    F --> G[Compare primitives against Tini token library]
    G --> H[Create CorePVS token pack from Tini values]
    H --> I[Duplicate HTML files and swap to CorePVS tokens]
    I --> J[Convert duplicates to support OKLch tokens]
    J --> K[Compare primitive vs CorePVS looks and feel]
    K --> L[Document gaps, comparison, and decision flow]

    style C fill:#eefcf3,stroke:#16a34a,stroke-width:1.5px
    style D fill:#eefcf3,stroke:#16a34a,stroke-width:1.5px
    style F fill:#fff8e8,stroke:#d97706,stroke-width:1.5px
    style H fill:#f5f3ff,stroke:#7c3aed,stroke-width:1.5px
    style K fill:#eef6ff,stroke:#3b82f6,stroke-width:1.5px
```
