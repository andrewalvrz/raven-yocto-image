


flowchart TD
    A[Yocto Build on Host PC] --> B[Generate raven-image]
    B --> C[Flash SD Card]
    C --> D[Raspberry Pi Boots Custom Image]
    D --> E[OTA Listener Active]
    D --> F[Telemetry Logger Active]
    E -->|MQTT Commands| PiPayload[Execute Commands on Payload]
    F -->|Logs Data| LogFile[Telemetry Log]
    G[Ground Station] -->|Send MQTT Commands| E
    F -->|Upload Data| G

