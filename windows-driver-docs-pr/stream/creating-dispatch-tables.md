---
title: 创建调度表
description: 创建调度表
keywords:
- BDA 微型驱动程序 WDK AVStream，调度表
- 调度表 WDK AVStream
- 筛选器调度表 WDK BDA
- 固定调度表 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38bf69a988d111faeddc7441775f36ea55acebdc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811389"
---
# <a name="creating-dispatch-tables"></a>创建调度表





必须为筛选器描述符 ([**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)) 为 BDA 微型驱动程序创建筛选器调度表，以便网络提供程序筛选器可以打开和初始化筛选器实例，稍后再发布筛选器实例。 还必须为每个 pin 描述符 ([**KSPIN \_ 描述符 \_**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) （) 在筛选器模板拓扑中可用的 pin 类型数组中）创建 pin 调度表。 网络提供程序筛选器使用 pin 调度表来打开和初始化 pin，并在以后释放 pin。 以下代码片段显示筛选器和固定调度表的示例：

```cpp
//
//  Filter Dispatch Table
//
//  Lists the dispatch routines for major events at the filter
//  level.
//
const
KSFILTER_DISPATCH
FilterDispatch =
{
    CFilter::Create,        // Create
    CFilter::FilterClose,   // Close
    NULL,                   // Process
    NULL                    // Reset
};

//
//  Input Pin Dispatch Table
//  Lists the dispatch routines for major events at the pin level.
//
const
KSPIN_DISPATCH
AntennaPinDispatch =
{
    CAntennaPin::PinCreate,         // Create
    CAntennaPin::PinClose,          // Close
    NULL,                           // Process signal data
    NULL,                           // Reset
    NULL,                           // SetDataFormat
    CAntennaPin::PinSetDeviceState, // SetDeviceState
    NULL,                           // Connect
    NULL,                           // Disconnect
    NULL,                           // Clock
    NULL                            // Allocator
};
```

 

