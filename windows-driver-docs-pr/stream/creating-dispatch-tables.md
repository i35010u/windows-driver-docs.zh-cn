---
title: 创建调度表
description: 创建调度表
ms.assetid: 0771aeac-68b2-4dec-8887-a0b313899ce8
keywords:
- BDA 微型驱动程序 WDK AVStream，调度表
- 调度表 WDK AVStream
- 筛选器调度表 WDK BDA
- pin 调度表 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0edc893b23c9fd71097d2b845f34f7e526bdb2a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378383"
---
# <a name="creating-dispatch-tables"></a>创建调度表





必须创建筛选器描述符的筛选器调度表 ([**KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)) 的 BDA 微型驱动程序，以便网络提供程序筛选器可以打开并初始化的实例筛选和更高版本的筛选器实例。 您还必须创建每个 pin 描述符的 pin 调度表 ([**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)) 中的筛选器的模板拓扑中可用的 pin 类型数组. 网络提供程序筛选器使用 pin 调度表来打开并初始化 pin 和更高版本的 pin。 下面的代码段显示了筛选器和 pin 调度表的示例：

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

 

 




