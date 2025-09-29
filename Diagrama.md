```mermaid
graph TD
    subgraph "1. Código y Colaboración (GitHub)"
        A[Desarrollador escribe código<br>en rama 'feature'] -- "1. Pull Request" --> B(Rama 'develop');
        B -- "3. Merge Aprobado" --> C(Rama 'main');
    end

    subgraph "2. Orquestador CI/CD (Jenkins / AWS CodePipeline)"
        B -- "2. Dispara CI" --> CI_Pipeline((CI<br>Integración Continua));
        C -- "4. Dispara CD" --> CD_Pipeline((CD<br>Despliegue Continuo));
    end

    subgraph "3. Pipeline de DataOps (Procesos de Datos)"
        CI_Pipeline --> D{CI de Datos};
        D --> D1[Análisis de Código];
        D --> D2[Pruebas Unitarias];
        D --> D3[Pruebas de Calidad<br>de Datos];

        CD_Pipeline --> E{CD de Datos};
        E --> E1[Empaquetar<br>(Docker)];
        E --> E2[Desplegar Pipeline<br>de Datos];
    end

    subgraph "4. Pipeline de MLOps (Modelo de ML)"
        CI_Pipeline --> F{CI de ML};
        F --> F1[Validar Datos];
        F --> F2[Entrenar Modelo];
        F --> F3[Evaluar y Registrar<br>Modelo (MLflow)];

        CD_Pipeline --> G{CD de ML};
        G --> G1[Empaquetar Modelo];
        G --> G2[Desplegar Endpoint<br>de Inferencia];
    end

    subgraph "5. Producción y Monitoreo"
        E2 --> H[Pipelines de Datos<br>en Producción];
        G2 --> I[Modelo Sirviendo<br>Predicciones];
        I --> J[Monitoreo Activo<br>del Modelo];
        J -- "Detecta Deriva de Datos" --> |"6. Dispara CT<br>(Entrenamiento Continuo)"| F2;
    end

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#ccf,stroke:#333,stroke-width:2px
    style C fill:#cfc,stroke:#333,stroke-width:2px
```
