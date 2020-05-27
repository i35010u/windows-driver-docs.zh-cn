---
title: Windows 中的 ACPI 支持摘要
description: 本主题概述了支持基于 SoC 的平台上的 Windows 所需的 ACPI 5.0 功能的子集。
ms.assetid: BECFB30B-541B-420E-85F3-773292066A90
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: a394640485adbce7211c44dc89192fb763c93715
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851717"
---
# <a name="summary-of-acpi-support-in-windows"></a>Windows 中的 ACPI 支持摘要

本主题概述了支持基于 SoC 的平台上的 Windows 所需的高级配置和电源接口（ACPI）5.0 功能的子集。

| Feature | "ACPI 5.0 规范" 部分 | 说明 |
| --- | --- | --- |
| 系统说明表 | 5.2.5 | 根系统说明指针（RSDP） |
| | 5.2.7、5.2。8 | 根（RSDT）或扩展（XSDT）系统说明表 |
| | 5.2.9 | 固定 ACPI 说明表（FADT） |
| | 5.2.12 | 多个 APIC 说明表（MADT） |
| | 5.2.24 | 一般计时器说明表（GTDT） |
| | 5.2.6  | 核心系统资源表（CSRT）[规范](https://acpica.org/related-documents) |
| | 5.2.6  | 调试端口表2（DBG2）[规范](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn639131(v=vs.85)) |
| | 5.2.11.1 | 差分系统说明表（DSDT） |
| | 5.2.11.2 | 辅助系统说明表（SSDT） |
| 设备管理 | 6.1 | 设备标识对象 |
| | 6.2 | 设备配置对象 |
| GPIO | 5.6.5.1 | GPIO 控制器设备 |
| | 5.6.5 | GPIO-已发出 ACPI 事件 |
| | 6.4.3.8.1, 19.5.53, 19.5.54 | GPIO 资源描述符和宏 |
| | 5.5.2.4.4 | GeneralPurposeIO OpRegions |
| 简单外设总线 (SPB) | 6.4.3.8.2, 19.5.55, 19.5.118, 19.5.134 | SPB 资源描述符和宏 |
| | | GenericSerialBus OpRegions |
| 设备电源管理 | 3.3 | |
| | 7.1 | 电源资源 |
| | 7.2 | 设备电源管理对象 |
| ACPI 定义的设备 | 9.0、10 | |
| | 9.5 | Control 方法电源按钮 |
| | 9.4 | 控制方法盖子设备 |
| | 10.2 | 控制方法电池设备 |
| | 9.18 | 控制方法时间和警报设备 |
| | 11 | 热量区域 |
| 特定于设备的支持 | 8.4 | Processors |
| | 附录 B | 显示 |
| | 6.1.8，9.13 | USB |
| | | SD 总线 |
| | | 相机 |
| | | HID-over I i2c 设备 |
| | 3.2.1、4.8.2.2.1.2、4.8.2.2.1。3 | 按钮 |
| | | 停靠和可转换的 PC 传感器 |
