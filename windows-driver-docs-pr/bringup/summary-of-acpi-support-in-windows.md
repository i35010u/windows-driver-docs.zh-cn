---
title: Windows 中的 ACPI 支持摘要
description: 本主题概述了基于 SoC 的平台上支持 Windows 所需的 ACPI 5.0 功能的子集。
ms.assetid: BECFB30B-541B-420E-85F3-773292066A90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deac499039dcc40dd560a2dab883ffcdb2c60ac6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576345"
---
# <a name="summary-of-acpi-support-in-windows"></a>Windows 中的 ACPI 支持摘要


本主题总结了高级配置和电源接口 (ACPI) 5.0 基于 SoC 的平台上支持 Windows 所需的功能的子集。

| 功能                     | ACPI 5.0 规范的节                                                    | 说明                                                              |
|-----------------------------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| 系统描述表   | 5.2.5                                                                                | 根系统说明指针 (RSDP)                             |
|                             | 5.2.7, 5.2.8                                                                         | 根 (RSDT) 或扩展 （xsdt 表） 系统说明表 |
|                             | 5.2.9                                                                                | 固定的 ACPI 描述表 (FADT)                                |
|                             | 5.2.12                                                                               | 多个 APIC 说明表 (MADT)                             |
|                             | 5.2.24                                                                               | 泛型计时器说明表 (GTDT)                             |
|                             | 5.2.6 (规范是[此处](https://acpica.org/related-documents)。)               | 内核系统资源表 (CSRT)                                 |
|                             | 5.2.6 (规范是[此处]( https://go.microsoft.com/fwlink/p/?LinkId=691234)。) | 调试端口表 2 (DBG2)                                          |
|                             | 5.2.11.1                                                                             | 差异化的系统描述表 (DSDT)                     |
|                             | 5.2.11.2                                                                             | 辅助系统描述表 (SSDT)                          |
| 设备管理           | 6.1                                                                                  | 设备标识对象                                      |
|                             | 6.2                                                                                  | 设备配置对象                                       |
| GPIO                        | 5.6.5.1                                                                              | GPIO 控制器设备                                            |
|                             | 5.6.5                                                                                | GPIO 信号 ACPI 事件                                          |
|                             | 6.4.3.8.1, 19.5.53, 19.5.54                                                          | GPIO 资源描述符和宏                               |
|                             | 5.5.2.4.4                                                                            | GeneralPurposeIO OpRegions                                         |
| 简单外设总线 (SPB) | 6.4.3.8.2, 19.5.55, 19.5.118, 19.5.134                                               | 存储资源描述符和宏                                |
|                             |                                                                                      | GenericSerialBus OpRegions                                         |
| 设备电源管理     | 3.3                                                                                  |                                                                    |
|                             | 7.1                                                                                  | Power 资源                                                    |
|                             | 7.2                                                                                  | 设备电源管理对象                                    |
| ACPI 定义的设备        | 9.0, 10                                                                              |                                                                    |
|                             | 9.5                                                                                  | 控制方法电源按钮                                        |
|                             | 9.4                                                                                  | 控制方法合上盖子设备                                          |
|                             | 10.2                                                                                 | 控制方法电池设备                                      |
|                             | 9.18                                                                                 | 控制方法时间和警报的设备                               |
|                             | 11                                                                                   | 温度区域                                                      |
| 特定于设备的支持     | 8.4                                                                                  | 处理器                                                         |
|                             | 附录 B                                                                           | 显示                                                           |
|                             | 6.1.8, 9.13                                                                          | USB                                                                |
|                             |                                                                                      | SD 总线                                                             |
|                             |                                                                                      | 相机                                                            |
|                             |                                                                                      | HID over I²C 设备                                               |
|                             | 3.2.1, 4.8.2.2.1.2, 4.8.2.2.1.3                                                      | 按钮                                                            |
|                             |                                                                                      | 停靠和可转换为 PC 传感器                                    |

 

 

 




