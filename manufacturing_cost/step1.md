flowchart TD
    subgraph ERP["ERP 시스템"]
        A1["재고 관리"]
        A2["원재료 구매"]
        A3["생산 계획 및 일정"]
        A4["직접 인건비"]
        A5["제조 간접비"]
        A6["완제품 재고"]
        A7["출하 및 판매"]
        A8["제조 원가 산출"]
        A9["보고서 작성"]
    end

    subgraph MES["MES 시스템"]
        B1["생산 기록"]
        B2["원재료 사용"]
        B3["노동 시간"]
        B4["설비 사용"]
        B5["품질 검사"]

        subgraph OEE["OEE 구성 요소"]
            C1["가용성"]
            C2["성능"]
            C3["품질"]
            C4["비효율 원가 분석"]
        end
    end

    %% ERP 내부 흐름
    A1 -->|"재고 부족 시"| A2
    A1 --> A3
    A3 --> B1
    A4 --> A8
    A5 --> A8
    A6 --> A7
    A7 --> A8
    A8 --> A9

    %% MES to ERP
    B1 -->|"실시간 완제품 정보<br/>실시간 데이터 수집 및 모니터링"| A6
    B2 -->|"정확한 재고 데이터<br/>비용 절감"| A1
    B3 -->|"정확한 노무비 계산<br/>비용 절감"| A4
    B4 -->|"정확한 간접비 산출<br/>비용 절감"| A5

    %% MES 내부 흐름
    B1 --> B2
    B1 --> B3
    B1 --> B4
    B1 -->|"규제 준수 및 추적성"| B5

    %% MES to OEE
    B1 --> C1
    B1 --> C2
    B5 -->|"품질 관리 강화"| C3
    B4 --> C1
    B4 --> C2

    %% OEE 내부 흐름
    C1 & C2 & C3 -->|"생산성 향상"| C4

    %% OEE to ERP
    C4 -.->|"비효율 분석 정보<br/>의사결정 지원"| A8

    %% 스타일
    classDef erpStyle fill:#f9f,stroke:#333,stroke-width:2px;
    classDef mesStyle fill:#bbf,stroke:#333,stroke-width:2px;
    classDef oeeStyle fill:#bfb,stroke:#333,stroke-width:2px;
    

    class A1,A2,A3,A4,A5,A6,A7,A8,A9 erpStyle;
    class B1,B2,B3,B4,B5 mesStyle;
    class C1,C2,C3,C4 oeeStyle;
