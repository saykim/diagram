flowchart TD
    subgraph ERP["ERP 시스템"]
        A[시작]
        B[생산 계획 입력]
        C[원재료 및 인력 할당]
    end

    subgraph MES["MES 시스템"]
        D[생산 실행]
        E{실시간 데이터 수집}
        F[원재료 사용량 집계]
        G[작업 시간 집계]
        H[전력 사용량 집계]
        I[설비 상태 모니터링]
        J[총 생산량 집계]
        K[양품 수량 집계]

        subgraph OEE["OEE 계산"]
            O[가용성 Availability 계산\n계획 생산 시간 대비\n실제 생산 시간]
            P[성능 Performance 계산\n이론적 생산량 대비\n실제 생산량]
            Q[품질 Quality 계산\n총 생산량 대비\n양품 수량]
            R[종합 OEE 계산\nAvailability x Performance x Quality]
        end

        S[비효율 비용 계산]
    end

    subgraph COST["제조원가 산출 시스템"]
        L[직접비 계산]
        M[간접비 계산]
        T[총 제조원가 계산]
        U[단위당 제조원가 계산]
        V[원가 분석 및 보고서 생성]
    end

    %% ERP 내부 흐름
    A --> B
    B --> C

    %% MES 내부 흐름
    C --> D
    D --> E
    E --> F & G & H & I & J & K
    J & K --> O & P & Q
    O & P & Q --> R
    R --> S

    %% 제조원가 계산 흐름
    F & G --> L
    H & I --> M
    S --> M
    L & M --> T
    T & K --> U
    U --> V

    %% 시스템 간 데이터 흐름
    B -->|계획 생산 시간| O
    B -->|이론적 생산량| P
    C -->|원재료 및 인력 정보| D

    V --> Z[종료]

    %% 스타일 지정
    classDef erpStyle fill:#f9f,stroke:#333,stroke-width:2px;
    classDef mesStyle fill:#bbf,stroke:#333,stroke-width:2px;
    classDef costStyle fill:#ff9,stroke:#333,stroke-width:2px;
    classDef oeeStyle fill:#bfb,stroke:#333,stroke-width:2px;

    class A,B,C erpStyle;
    class D,E,F,G,H,I,J,K,S mesStyle;
    class L,M,T,U,V costStyle;
    class O,P,Q,R oeeStyle;

    %% 서브그래프 스타일
    style ERP fill:none,stroke:#f66,stroke-width:2px;
    style MES fill:none,stroke:#66f,stroke-width:2px;
    style COST fill:none,stroke:#fd6,stroke-width:2px;
    style OEE fill:none,stroke:#6f6,stroke-width:2px;
