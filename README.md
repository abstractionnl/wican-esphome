# Samples for flashing the WiCAN obd dongle (https://www.meatpi.com/products/wican) with Esphome

Included are some working templates for the Hyundai Ioniq Electric (my 2016-2019) and Kia Niro PHEV (my 2016-2022) 
Uses a custom component to read OBD pids (https://github.com/abstractionnl/esphome/tree/obd_component/esphome/components/obd)

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
 - Warning: When polling is not disabled, the 12v battery will be drained within a few hours.
 - Odometer and TPMS only respond when the car is running, not while charging.