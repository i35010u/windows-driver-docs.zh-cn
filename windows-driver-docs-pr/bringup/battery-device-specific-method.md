---
title: 电池特定于设备的方法
description: 本主题介绍 _DSM 控件方法和被动热量电池管理的参数。
ms.assetid: 622803F4-2548-4E8A-A330-179ABDF374AD
ms.date: 05/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5d31df93181b72a9c42767fe2e494ea5c5a8962e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525659"
---
# <a name="battery-device-specific-method"></a>电池特定于设备的方法


若要支持电池的被动热量管理平台，Microsoft 定义\_DSM 方法进行通信平台固件散热限制限制由电池的散热区域设置。

有关详细信息，请参阅**热量区域**主题中[ACPI 定义设备](acpi-defined-devices.md#thermal)主题。

## <a name="function-1-battery-thermal-limit"></a>函数 1:电池散热限制


\_DSM 控件方法参数为电池充电散热限制函数如下所示：

### <a name="arguments"></a>参数

-   **Arg0:** UUID = 4c2067e3-887d-475c-9720-4af1d3ed602e
-   **Arg1:** 修订 = 0
-   **Arg2:** 函数索引 = 1
-   **Arg3:** 热感限制 （整数值从 0 到 100）

### <a name="return"></a>返回

无。 固件负责具有吸引力的收费，如果能考虑当前的散热限制。
 

 




