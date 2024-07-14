erDiagram
    %% ERP 시스템 엔티티
    PRODUCT_ERP {
        int product_id PK "제품ID"
        string product_name "제품명"
        float standard_cost "표준원가"
        float ideal_cycle_time "이상적사이클시간"
    }
    PRODUCTION_PLAN_ERP {
        int plan_id PK "계획ID"
        int product_id FK "제품ID"
        date plan_date "계획일자"
        int planned_quantity "계획수량"
        float planned_runtime "계획가동시간"
    }
    RAW_MATERIAL_ERP {
        int material_id PK "원재료ID"
        string material_name "원재료명"
        float unit_cost "단위비용"
    }
    LABOR_ERP {
        int labor_id PK "노동ID"
        string labor_type "노동유형"
        float hourly_rate "시간당임률"
    }
    EQUIPMENT_ERP {
        int equipment_id PK "설비ID"
        string equipment_name "설비명"
        float depreciation_rate "감가상각률"
    }

    %% 제조원가 테이블
    MANUFACTURING_COST_CORE {
        int cost_id PK "원가ID"
        int production_id FK "생산ID"
        float direct_material_cost "직접재료비"
        float direct_labor_cost "직접노무비"
        float manufacturing_overhead "제조간접비"
        float energy_cost "에너지비용"
        float maintenance_cost "유지보수비용"
        float inefficiency_cost "비효율비용"
        float quality_control_cost "품질관리비용"
        float regulatory_compliance_cost "규제준수비용"
        float waste_management_cost "폐기물관리비용"
        float total_cost "총원가"
        float unit_cost "단위원가"
    }

    %% MES 시스템 엔티티
    PRODUCTION_ACTUAL_MES {
        int production_id PK "생산ID"
        int plan_id FK "계획ID"
        int product_id FK "제품ID"
        date production_date "생산일자"
        int actual_quantity "실제생산수량"
        int good_quantity "양품수량"
        float actual_runtime "실제가동시간"
        float downtime "비가동시간"
    }
    BATCH_INFO_MES {
        int batch_id PK "배치ID"
        int production_id FK "생산ID"
        datetime start_time "시작시간"
        datetime end_time "종료시간"
        float batch_size "배치크기"
    }
    MATERIAL_USAGE_MES {
        int usage_id PK "사용ID"
        int production_id FK "생산ID"
        int material_id FK "원재료ID"
        float quantity_used "사용량"
    }
    LABOR_HOURS_MES {
        int labor_hours_id PK "노동시간ID"
        int production_id FK "생산ID"
        int labor_id FK "노동ID"
        float hours_worked "작업시간"
    }
    EQUIPMENT_USAGE_MES {
        int usage_id PK "사용ID"
        int production_id FK "생산ID"
        int equipment_id FK "설비ID"
        float usage_hours "사용시간"
    }
    ENERGY_CONSUMPTION_MES {
        int energy_id PK "에너지ID"
        int production_id FK "생산ID"
        float kwh_used "사용전력량"
        float kwh_rate "전력단가"
    }
    OEE_DATA_MES {
        int oee_id PK "OEE_ID"
        int production_id FK "생산ID"
        float availability "가동률"
        float performance "성능률"
        float quality "품질률"
        float oee "종합설비효율"
    }
    AVAILABILITY_DETAIL_MES {
        int availability_id PK "가동률상세ID"
        int oee_id FK "OEE_ID"
        float planned_production_time "계획생산시간"
        float run_time "실제가동시간"
        float setup_time "셋업시간"
        float unplanned_stop_time "계획외정지시간"
    }
    PERFORMANCE_DETAIL_MES {
        int performance_id PK "성능률상세ID"
        int oee_id FK "OEE_ID"
        float ideal_cycle_time "이상사이클타임"
        float actual_cycle_time "실제사이클타임"
        int total_pieces "총생산수량"
        float minor_stop_time "소정지시간"
        float speed_loss_time "속도손실시간"
    }
    QUALITY_DETAIL_MES {
        int quality_id PK "품질률상세ID"
        int oee_id FK "OEE_ID"
        int total_production "총생산수량"
        int good_pieces "양품수량"
        int defect_pieces "불량수량"
        string defect_reasons "불량사유"
    }
    QUALITY_INSPECTION_MES {
        int inspection_id PK "검사ID"
        int batch_id FK "배치ID"
        datetime inspection_time "검사시간"
        string inspection_result "검사결과"
        string failure_reason "불량원인"
    }
    INVENTORY_MANAGEMENT_MES {
        int inventory_id PK "재고ID"
        int material_id FK "원재료ID"
        int product_id FK "제품ID"
        float quantity "수량"
        date expiry_date "유통기한"
    }
    EQUIPMENT_CLEANING_MES {
        int cleaning_id PK "세척ID"
        int equipment_id FK "설비ID"
        datetime cleaning_time "세척시간"
        string cleaning_method "세척방법"
    }
    WASTE_MANAGEMENT_MES {
        int waste_id PK "폐기물ID"
        int production_id FK "생산ID"
        float waste_quantity "폐기물량"
        float disposal_cost "처리비용"
    }

    %% 관계 정의
    PRODUCT_ERP ||--|{ PRODUCTION_PLAN_ERP : "계획 수립"
    PRODUCT_ERP ||--|{ PRODUCTION_ACTUAL_MES : "생산"
    PRODUCTION_PLAN_ERP ||--|{ PRODUCTION_ACTUAL_MES : "계획 실행"
    RAW_MATERIAL_ERP ||--|{ MATERIAL_USAGE_MES : "원재료 사용"
    LABOR_ERP ||--|{ LABOR_HOURS_MES : "노동 제공"
    EQUIPMENT_ERP ||--|{ EQUIPMENT_USAGE_MES : "설비 사용"
    MANUFACTURING_COST_CORE ||--|| PRODUCTION_ACTUAL_MES : "원가 산출"
    PRODUCTION_ACTUAL_MES ||--|{ MATERIAL_USAGE_MES : "원재료 사용"
    PRODUCTION_ACTUAL_MES ||--|{ LABOR_HOURS_MES : "노동 투입"
    PRODUCTION_ACTUAL_MES ||--|{ EQUIPMENT_USAGE_MES : "설비 사용"
    PRODUCTION_ACTUAL_MES ||--|{ ENERGY_CONSUMPTION_MES : "에너지 소비"
    PRODUCTION_ACTUAL_MES ||--|| OEE_DATA_MES : "OEE 측정"
    OEE_DATA_MES ||--|| AVAILABILITY_DETAIL_MES : "가동률 상세"
    OEE_DATA_MES ||--|| PERFORMANCE_DETAIL_MES : "성능률 상세"
    OEE_DATA_MES ||--|| QUALITY_DETAIL_MES : "품질률 상세"
    PRODUCTION_ACTUAL_MES ||--|{ BATCH_INFO_MES : "배치 생산"
    BATCH_INFO_MES ||--|{ QUALITY_INSPECTION_MES : "품질 검사"
    PRODUCTION_ACTUAL_MES ||--|{ INVENTORY_MANAGEMENT_MES : "재고 관리"
    EQUIPMENT_USAGE_MES ||--|{ EQUIPMENT_CLEANING_MES : "설비 세척"
    PRODUCTION_ACTUAL_MES ||--|{ WASTE_MANAGEMENT_MES : "폐기물 발생"
