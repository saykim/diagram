flowchart TD
    subgraph ERP["ERP 시스템"]
        B[생산 계획 입력]
        C[원재료 및 인력 할당]
    end

    subgraph MES["MES 시스템"]
        D[생산 실행]
        E{실시간 데이터 수집}
        F[원재료비 계산]
        G[직접노무비 계산]
        H[전력비 계산]
        I[설비유지보수비 계산]
        J[총 생산량 집계]
        K[양품 수량 집계]
        L[직접비 계산]
        M[간접비 계산]

        subgraph OEE["OEE 계산"]
            O[가용성 Availability\n계획 생산 시간 대비\n실제 생산 시간]
            P[성능 Performance\n이론적 생산량 대비\n실제 생산량]
            Q[품질 Quality\n총 생산량 대비\n양품 수량]
            R[종합 OEE 계산\nAvailability x Performance x Quality]
        end

        S[비효율 비용 계산]
    end

    subgraph COST["제조원가 산출"]
        T[총 제조원가 계산]
        U[단위당 제조원가 계산]
        V[원가 분석 및 보고서 생성]
    end

    A[시작] --> B
    B --> C
    C --> D
    D --> E
    E --> |원재료 사용량| F
    E --> |작업 시간| G
    E --> |전력 사용량| H
    E --> |설비 상태| I
    E --> |생산량| J
    E --> |품질 검사 결과| K
    F & G --> L
    H & I --> M
    J & K --> O & P & Q
    O & P & Q --> R
    R --> S
    L & M & S --> T
    K & T --> U
    U --> V
    V --> W[종료]

    %% ERP에서 MES로의 데이터 흐름
    C -->|원재료 및 인력 정보| D
    B -->|계획 생산 시간| O
    B -->|이론적 생산량| P

    %% MES에서 제조원가 산출로의 데이터 흐름
    L -->|직접비| T
    M -->|간접비| T
    S -->|비효율 비용| T
    K -->|양품 수량| U

    %% OEE에서 비효율 비용으로의 데이터 흐름
    R -->|OEE 지표| S

    %% 스타일 지정
    classDef erpStyle fill:#f9f,stroke:#333,stroke-width:2px;
    classDef mesStyle fill:#bbf,stroke:#333,stroke-width:2px;
    classDef costStyle fill:#ff9,stroke:#333,stroke-width:2px;
    classDef oeeStyle fill:#bfb,stroke:#333,stroke-width:2px;

    class B,C erpStyle;
    class D,E,F,G,H,I,J,K,L,M,S mesStyle;
    class T,U,V costStyle;
    class O,P,Q,R oeeStyle;

    %% 서브그래프 스타일
    style ERP fill:none,stroke:#f66,stroke-width:2px;
    style MES fill:none,stroke:#66f,stroke-width:2px;
    style COST fill:none,stroke:#fd6,stroke-width:2px;
    style OEE fill:none,stroke:#6f6,stroke-width:2px;
