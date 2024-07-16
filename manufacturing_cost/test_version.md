graph 
    subgraph 제조 데이터
        subgraph ERP System
            subgraph 생산계획
                A[생산지시]
            end
            subgraph 재고
                C[재고관리]
            end
            subgraph 원가 계산
                D1[직접비]
                D2[간접비]
                D3[변동비]
            end
            subgraph 분석
                N[품질비용]
                P[효율성 분석]
            end
            L[제조원가 산출]
            F[생산실적 등록]
        end

        subgraph MES_System
            subgraph 생산 관리
                B[생산실행]
                E[생산실적 집계]
                R[실시간 모니터링]
            end
            subgraph 데이터 수집
                G1[설비 가동시간]
                G2[설비 상태 데이터]
                G3[생산수량 데이터]
                G4[품질검사 데이터]
            end
            M[품질검사]
            S[실시간 데이터 처리]
        end

        subgraph OEE_계산
            O1[가용성]
            O2[성능]
            O3[품질]
            O4[OEE 산출]
            subgraph 가용성 계산
                OA1[계획 생산시간]
                OA2[실제 가동시간]
                OA3[계획 정지시간]
            end
            subgraph 성능 계산
                OB1[이론적 사이클 타임]
                OB2[총 생산수량]
            end
            subgraph 품질 계산
                OC1[총 생산수량]
                OC2[불량품 수량]
            end
        end
    end

    A -->|계획 전달| B
    A -->|원재료 출고| C
    B -->|생산데이터| E
    E -->|실적 전송| F
    F -->|완제품 입고| C

    G1 & G2 & G3 & G4 -->|실시간 데이터| S
    S -->|처리된 데이터| R
    S -->|OEE 계산용 데이터| O1
    S -->|OEE 계산용 데이터| O2
    S -->|OEE 계산용 데이터| O3

    R -->|실시간 피드백| B
    O4 -->|실시간 OEE 데이터| R

    G1 -->|가동시간 데이터| D1
    G2 -->|설비 상태 데이터| D2
    G3 -->|생산수량 데이터| D3
    G4 -->|품질 데이터| N

    OA1 & OA2 & OA3 -->|가용성 계산| O1
    OB1 & OB2 -->|성능 계산| O2
    OC1 & OC2 -->|품질 계산| O3
    O1 & O2 & O3 -->|종합| O4

    O4 -->|OEE 데이터| P
    M -->|품질검사 결과| N
    M -->|불량률| O3

    D1 & D2 & D3 & N & P --> L

    classDef mesSystem fill:#ffdddd,stroke:#ff0000,stroke-width:2px;
    classDef oeeCalc fill:#f0e6ff,stroke:#9966ff,stroke-width:2px;
    class MES_System mesSystem;
    class OEE_계산 oeeCalc;
