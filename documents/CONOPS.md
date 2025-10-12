Purpose:

To describe the way ESP32-bbsed CubeSat educational prototype operates in each mode and how students interact with it

Mission statement:

Provide an accessible, model-based learning platform for students to understand CubeSat subsystem design, task scheduling, telemetry handling, and systems engineering lifecycle using COTS components and MBSE documentation.


Operational Concept:

1. Boot mode

Power-on self-test and initialization of I2C, UART, and Wifi subsystems. It is triggered by applying power. It aims to check sensors, mount SD card, connect Wi-Fi

2. Nominal mode:

Normal operation with periodic sensor sampling, filtering, and telemetry. Triggered by complete initialization. it perform 4 task on the rtos which are sensorTask, filterTask, storageTask, telemetryTask

3. Safe mode: 

minimal power draw, it only perform data logging without telemetry. Triggered by low voltage or wifi loss. During this period it only monitor power and SD logging.

4. Relay/EWS mode:

acts as a data relay node or early-warning system via MQTT. It is initiated with an external command or threshold alert. It priotitize event publishing to the GCS.

Data Flow:
1. ESP32 acquires data (MPU6050, BMP280, NEO-6M)
2. FreeRTOS schedules tasks for filtering, logging, and transmission
3. wifi sends telemetry jeson to web gcs
4. GCS displays live plots and logs data

Educational workflow:
1. Modeling: students identify requirements (FRign: create SysML diagrams (block, sequence).
2. Design: create a SysML diagrams block and sequence 
3. Build: assemble CubeSat structure and flash firmware.
4. Verify: compare system behavior vs. modeled requirements.
5. Reflect: document lessons in V&V sheet.
