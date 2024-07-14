flowchart TD
    subgraph ERP["ERP 시스템"]
        A1[재고 관리]
        A2[원재료 구매]
        A3[생산 계획 수립]
        A4[인력 관리]
        A5[설비 관리]
        A6[완제품 관리]
        A7[제조원가 계산]
    end

    subgraph MES["MES 시스템"]
        B1[생산 실행]
        B2[실시간 데이터 수집]
        B3[원재료 사용 추적]
        B4[작업 시간 기록]
        B5[설비 가동 모니터링]
        B6[품질 검사]
        
        subgraph OEE["OEE 계산"]
            C1[가용성 Availability]
            C2[성능 Performance]
            C3[품질 Quality]
            C4[OEE 종합 계산]
        end
        
        B7[비효율 비용 산출]
    end

    subgraph COST["제조원가 산출"]
        D1[직접비 계산]
        D2[간접비 계산]
        D3[총 제조원가 계산]
        D4[단위당 제조원가 계산]
        D5[원가 분석 보고서]
    end

    %% ERP 내부 흐름
    A1 --> A2
    A1 --> A3
    A4 --> A3
    A5 --> A3
    A3 --> B1
    A6 --> A7

    %% MES 내부 흐름
    B1 --> B2
    B2 --> B3
    B2 --> B4
    B2 --> B5
    B2 --> B6
    B5 --> C1
    B5 --> C2
    B6 --> C3
    C1 & C2 & C3 --> C4
    C4 --> B7

    %% MES to ERP
    B3 --> A1
    B4 --> A4
    B5 --> A5
    B1 --> A6

    %% 제조원가 계산
    A2 & B3 --> D1
    A4 & B4 --> D1
    A5 & B5 --> D2
    B7 --> D2
    D1 & D2 --> D3
    D3 --> D4
    D4 --> D5
    D5 --> A7

    %% 스타일
    classDef erpStyle fill:#f9f,stroke:#333,stroke-width:2px;
    classDef mesStyle fill:#bbf,stroke:#333,stroke-width:2px;
    classDef costStyle fill:#ff9,stroke:#333,stroke-width:2px;
    classDef oeeStyle fill:#bfb,stroke:#333,stroke-width:2px;

    class A1,A2,A3,A4,A5,A6,A7 erpStyle;
    class B1,B2,B3,B4,B5,B6,B7 mesStyle;
    class C1,C2,C3,C4 oeeStyle;
    class D1,D2,D3,D4,D5 costStyle;

    %% 서브그래프 스타일
    style ERP fill:none,stroke:#f66,stroke-width:2px;
    style MES fill:none,stroke:#66f,stroke-width:2px;
    style COST fill:none,stroke:#fd6,stroke-width:2px;
    style OEE fill:none,stroke:#6f6,stroke-width:2px;
