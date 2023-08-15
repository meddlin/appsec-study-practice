# Application Architecture

This is similar to what the full-fledged deployment would look like.

```mermaid
flowchart LR
    db[(KV-store)] --> B1[API]
    db[(KV-store)] --> B2[API]
    db[(KV-store)] --> B3[API]

    subgraph APILayer
        B1 --> C(API gateway)
        B2 --> C(API gateway)
        B3 --> C(API gateway)
    end

    C --> FE-1[web front-end] --> WAF1
    C --> FE-2[web front-end] --> WAF2
    C --> FE-3[web front-end] --> WAF3   
```

## Simplified

A simplified model to start with.

```mermaid
flowchart LR
    db[("`
        KV-store
        **_data_**
    `")] --> A1[API]
    A1 <--> FE-1[web front-end]
```

## OWASP \# 1 - Broken Access Control

This means "_the user can access something they aren't supposed to_".

The logic for a "broken access control" will primarily take place in the API, 
but the effects of this vulnerability will show up in the interaction between
API and front-end.

```mermaid
flowchart LR
    A1-. bug here .->FE-1[web front-end]
```

Ref: [https://owasp.org/Top10/A01_2021-Broken_Access_Control/](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)