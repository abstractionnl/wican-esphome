# Samples for flashing the [WiCAN obd dongle](https://www.meatpi.com/products/wican) with Esphome

Included are some working templates for the Hyundai Ioniq Electric (my 2016-2019) and Kia Niro PHEV (my 2016-2022) 
Uses a custom component to read [OBD pids](https://github.com/abstractionnl/esphome/tree/obd_component/esphome/components/obd)

Flashing for the first time must be done by connecting the WiCAN via USB. [Short the pins](https://meatpihq.github.io/wican-fw/config/firmware-update#_2-usb-flash-for-wican) before connecting USB and flash using the ESPhome tool

Features:
 - Polling various pids from the car on a set frequency
 - Push sensor data over MQTT to Home Assistant
 - Stop polling when car is switched off or no longer charging by monitoring aux battery voltage to prevent dead battery
 - Re-enable polling when the car is started or charging is started or by switch in Home Assistant.
 - Automatically reconnect to wifi when car is switched off to send latest data on arrival home.

 Available sensors:
 - BMS: SOC Display, SOC BMS, State of Health, battery voltage, battery current, total energy (dis)charged, charging cable status, charging status
 - Odometer
 - TPMS: Tire pressure

Some shortcomings:
 - When the car is 'asleep' (not running or charging), it does not respond to any obd request, so charge cable status might not be correct after connect/disconnect. It does briefly respond after connecting charge cable though.
 - **Warning**: When polling is not disabled, the 12v battery will be drained within a few hours.
 - Odometer and TPMS only respond when the car is running, not while charging.

 Sources:
  - https://github.com/JejuSoul/OBD-PIDs-for-HKMC-EVs/tree/master/Ioniq%20EV%20-%2028kWh/extendedpids
  - https://github.com/JejuSoul/OBD-PIDs-for-HKMC-EVs/tree/master/Kia%20Niro%20PHEV%20-%208.9kWh/extendedpids
  - https://github.com/openvehicles/Open-Vehicle-Monitoring-System-3/blob/master/vehicle/OVMS.V3/components/vehicle_hyundai_ioniqvfl/src/vehicle_hyundai_ioniqvfl.cpp#L65 
  - https://gist.github.com/felixstorm/18f8ad9fb31ca71bbf62ba32801c34ae