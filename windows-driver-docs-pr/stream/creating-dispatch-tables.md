---
title: 创建调度表
description: 创建调度表
ms.assetid: 0771aeac-68b2-4dec-8887-a0b313899ce8
keywords:
- BDA 微型驱动程序 WDK AVStream，调度表
- 调度表 WDK AVStream
- 筛选器调度表 WDK BDA
- 固定调度表 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b99f1ad4614e0152f59bb9f97c3315a90e5dc137
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827123"
---
# <a name="creating-dispatch-tables"></a>创建调度表





必须为 BDA 微型驱动程序的筛选器描述符（[**KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)）创建筛选器调度表，以便网络提供程序筛选器可以打开和初始化筛选器实例，稍后再发布筛选器实例。 还必须在该类型的 pin 类型（在筛选器模板拓扑中可用）的数组中为每个 pin 描述符（[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)）创建 pin 调度表。 网络提供程序筛选器使用 pin 调度表来打开和初始化 pin，并在以后释放 pin。 以下代码片段显示筛选器和固定调度表的示例：

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

 

 




