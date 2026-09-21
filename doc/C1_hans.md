# 电壁挂炉

Midea 设备类型 **C1** 的采暖支持（已在型号 **2760001Z** 上验证）。该配置仅支持采暖；部分 Lua 脚本中的生活热水/沐浴控制未开放。

## 功能

- 目标温度（30–60 °C，步进 1 °C）
- 采暖预设模式：`user`（居家）、`activity`（外出）、`sleep`（睡眠）
- 通过 climate 或可选开关控制电源

## 生成实体

### 默认生成实体

| 实体ID                      | 类型    | 描述       |
| --------------------------- | ------- | ---------- |
| climate.{DEVICEID}\_climate | climate | 恒温器实体 |

### 额外生成实体

| EntityID                                            | 类型          | 名称             |
| --------------------------------------------------- | ------------- | ---------------- |
| binary_sensor.{DEVICEID}\_heating                   | binary_sensor | 采暖中           |
| binary_sensor.{DEVICEID}\_fault                     | binary_sensor | 故障             |
| binary_sensor.{DEVICEID}\_pump_on                   | binary_sensor | 水泵             |
| binary_sensor.{DEVICEID}\_standby                   | binary_sensor | 待机             |
| binary_sensor.{DEVICEID}\_warm_power                | binary_sensor | 制热功率         |
| binary_sensor.{DEVICEID}\_cold_power                | binary_sensor | 制冷功率         |
| binary_sensor.{DEVICEID}\_sleep_power               | binary_sensor | 睡眠功率         |
| sensor.{DEVICEID}\_current_temperature              | sensor        | 当前温度         |
| sensor.{DEVICEID}\_return_temperature               | sensor        | 回水温度         |
| sensor.{DEVICEID}\_heating_temperature              | sensor        | 采暖温度         |
| sensor.{DEVICEID}\_heating_gap_temperature          | sensor        | 采暖回差温度     |
| sensor.{DEVICEID}\_user_mode_target_temperature     | sensor        | 居家模式目标温度 |
| sensor.{DEVICEID}\_activity_mode_target_temperature | sensor        | 外出模式目标温度 |
| sensor.{DEVICEID}\_sleep_mode_target_temperature    | sensor        | 睡眠模式目标温度 |
| sensor.{DEVICEID}\_flow_volume                      | sensor        | 循环流量         |
| sensor.{DEVICEID}\_last_time                        | sensor        | 上次时间         |
| sensor.{DEVICEID}\_error_code                       | sensor        | 错误码           |
| sensor.{DEVICEID}\_heating_unit_type                | sensor        | 采暖末端类型     |
| sensor.{DEVICEID}\_three_way_mode                   | sensor        | 三通阀模式       |
| sensor.{DEVICEID}\_status                           | sensor        | 状态             |
| select.{DEVICEID}\_heating_mode                     | select        | 采暖模式         |
| switch.{DEVICEID}\_power                            | switch        | 电源开关         |

## 服务

### midea_ac_lan.set_attribute

[![Service](https://my.home-assistant.io/badges/developer_call_service.svg)](https://my.home-assistant.io/redirect/developer_call_service/?service=midea_ac_lan.set_attribute)

设置设备属性，服务数据:

| 名称      | 描述                  |
| --------- | --------------------- |
| device_id | 设备的编号(Device ID) |
| attribute | "power"               |
| value     | true 或 false         |

| 名称      | 描述                    |
| --------- | ----------------------- |
| device_id | 设备的编号(Device ID)   |
| attribute | "heating_mode"          |
| value     | user、activity 或 sleep |

示例

```yaml
service: midea_ac_lan.set_attribute
data:
  device_id: XXXXXXXXXXXX
  attribute: power
  value: true
```

```yaml
service: midea_ac_lan.set_attribute
data:
  device_id: XXXXXXXXXXXX
  attribute: heating_mode
  value: activity
```
