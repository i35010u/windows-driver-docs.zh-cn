---
title: Microsoft 热量扩展的特定于设备的方法
description: 为了支持更灵活的热区域和热传感器设计，Windows 支持向 ACPI 热区模型扩展。
ms.date: 01/14/2021
ms.localizationpriority: medium
ms.openlocfilehash: 7f595f63027c9bb29a1e0050556e50374c1c4bb6
ms.sourcegitcommit: 3c25e3d23e63869f9906846314a95f1b6338a5a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98223781"
---
# <a name="device-specific-method-for-microsoft-thermal-extensions"></a>Microsoft 热量扩展的特定于设备的方法

为了支持更灵活的热区域和热传感器设计，Windows 支持向 ACPI 热区模型扩展。 具体而言，Windows 支持每个热量区域 (MTL) 的热量最小限制，还支持在热量区域之间共享温度传感器。

有关 MTL 的详细信息，请参阅 [Windows 中的热管理](/windows-hardware/design/device-experiences/thermal-management-in-windows)

若要使用这些功能，Oem 可以 \_ 在任何热区的命名空间中包含以下 Device-Specific 方法 (DSM) 。

## <a name="function-1-minimum-throttle-limit"></a>函数1：最小限制限制

\_热量最小限制限制的 DSM 控制方法参数如下：

### <a name="arguments-minimum-throttle-limit"></a>参数 (最小限制限制) 

- **Arg0：** UUID = 14d399cd-7a27-4b18-8fb4-7cb7b9f4e500
- **Arg1：** 修订版 ID = 0
- **Arg2：** 函数 index = 1
- **Arg3：** 空包 (未使用) 

### <a name="return-minimum-throttle-limit"></a>返回 (最小限制限制) 

一个整数值，它具有当前的最小限制限制（以百分比表示）。 Windows 不会将限制限制设置为低于此值。

## <a name="function-2-temperature-sensor-device"></a>函数2：温度传感器设备

\_温度传感器设备的 DSM 控制方法参数如下：

### <a name="arguments-temperature-sensor-device"></a>温度传感器设备) 的参数 (

- **Arg0：** UUID = 14d399cd-7a27-4b18-8fb4-7cb7b9f4e500
- **Arg1：** 修订版 ID = 0
- **Arg2：** 函数 index = 2
- **Arg3：** 空包 (未使用) 

### <a name="return-temperature-sensor-device"></a>返回 (温度传感器设备) 

对将返回此热区温度的设备的引用。

## <a name="temperature-sensor-device-dependency-requirement"></a>温度传感器设备依赖关系要求

如果温度传感器设备是通过 \_ DSM 函数索引2报告的，则该热区还需要包含一个用于 \_ 标识温度传感器设备上的热区依赖的 DEP 对象。

> [!NOTE]
> 每个 DSM 的函数索引 0 \_ 是一个查询函数，它返回支持的函数索引集，并且始终是必需的。 有关详细信息，请参阅 \_ ACPI 5.0 规范的 "DSM (设备特定方法) " 部分。
