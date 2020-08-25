---
title: 电池的特定于设备的方法
description: 本主题介绍 _DSM 控制方法和参数，以实现被动式热量电池管理。
ms.assetid: 622803F4-2548-4E8A-A330-179ABDF374AD
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 17b19b5ac685b3c4ba540c16561ecf321d732e8b
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850253"
---
# <a name="battery-device-specific-method"></a>电池的特定于设备的方法

为了支持平台被动热量管理，Microsoft 定义了一个 \_ DSM 方法，用于与平台固件通信，这是由电池热区设置的散热限制。

有关详细信息，请参阅[ACPI 定义的设备](acpi-defined-devices.md#thermal-zones)主题中的**热区域**部分。

## <a name="function-1-battery-thermal-limit"></a>函数1：电池温度限制

\_电池充电温度限制功能的 DSM 控制方法参数如下：

### <a name="arguments"></a>参数

- **Arg0：** UUID = 4c2067e3-887d-475c-9720-4af1d3ed602e
- **Arg1：** 修订号 = 0
- **Arg2：** 函数 index = 1
- **Arg3：** 温度限制 (从0到100的整数值) 

### <a name="return"></a>返回

无。 固件负责在充电时考虑当前热量限制。
