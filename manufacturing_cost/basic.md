flowchart TD
    A[원재료 구매] --> B[생산 계획]
    B --> C[생산 실행]
    C --> D[품질 관리]
    D --> E[완제품 재고]
    E --> F[판매]

    G[인력 관리] --> C
    H[설비 관리] --> C
    I[에너지 관리] --> C

    C --> J[생산성 분석]
    J --> K[비효율 비용 산출]

    A & G & H & I --> L[원가 요소 집계]
    C & D & K --> L
    L --> M[제조원가 산출]
    M --> N[수익성 분석]

    style M fill:#ff9999,stroke:#ff0000,stroke-width:4px
    style N fill:#99ff99,stroke:#009900,stroke-width:4px

    subgraph 비용 절감 기회
        J
        K
    end

    subgraph 핵심 비즈니스 지표
        M
        N
    end  
