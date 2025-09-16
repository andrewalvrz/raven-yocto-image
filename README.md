

flowchart TD
    A[Yocto Build on Host PC] --> B[Generate raven-image]
    B --> C[Flash SD Card]
    C --> D[Raspberry Pi Boots Custom Image]
    D --> E[OTA Listener Active]
    D --> F[Telemetry Logger Active]
    E --> PiPayload[Execute Commands on Payload]
    F --> LogFile[Telemetry Log]
    G[Ground Station] --> E
    E -->|MQTT Commands| PiPayload
    F -->|Logs Data| LogFile
    LogFile -->|Upload Data| G
