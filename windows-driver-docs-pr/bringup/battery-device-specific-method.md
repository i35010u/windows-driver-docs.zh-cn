---
title: 电池的特定于设备的方法
description: 本主题介绍 _DSM 控制方法和参数，以实现被动式热量电池管理。
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 962f6f2cd080f5abec695e69f1da1789ed3eec25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803425"
---
# <a name="battery-device-specific-method"></a>电池的特定于设备的方法

为了支持平台被动热量管理，Microsoft 定义了一个 \_ DSM 方法，用于与平台固件通信，这是由电池热区设置的散热限制。

有关详细信息，请参阅 [ACPI 定义的设备](acpi-defined-devices.md#thermal-zones)主题中的 **热区域** 部分。

## <a name="function-1-battery-thermal-limit"></a>函数1：电池温度限制

\_电池充电温度限制功能的 DSM 控制方法参数如下：

### <a name="arguments"></a>自变量

- **Arg0：** UUID = 4c2067e3-887d-475c-9720-4af1d3ed602e
- **Arg1：** 修订号 = 0
- **Arg2：** 函数 index = 1
- **Arg3：** 温度限制 (从0到100的整数值) 

### <a name="return"></a>返回

无。 固件负责在充电时考虑当前热量限制。
