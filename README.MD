flowchart TD
    HostPC[Yocto Build on Host PC] --> RavenImage[Generate raven-image]
    RavenImage --> SDCard[Flash SD Card]
    SDCard --> PiBoot[Raspberry Pi Boots Custom Image]
    PiBoot --> OTA[OTA Listener Active]
    PiBoot --> Telemetry[Telemetry Logger Active]
    OTA --> Payload[Execute Commands on Payload]
    Telemetry --> Log[Telemetry Log]
    GroundStation[Ground Station] --> OTA
    OTA -->|MQTT Commands| Payload
    Telemetry -->|Logs Data| Log
    Log -->|Upload Data| GroundStation
