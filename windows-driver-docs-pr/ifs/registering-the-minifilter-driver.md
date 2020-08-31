---
title: 注册微筛选器驱动程序
description: 注册微筛选器驱动程序
ms.assetid: 943082c9-dcff-478f-80ba-2a2e72f6ead2
keywords:
- 正在注册微筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4da06433f9e408ea99f5a0ca985b9b62bc998522
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063246"
---
# <a name="registering-the-minifilter-driver"></a>注册微筛选器驱动程序


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


每个微筛选器驱动程序都必须从其**DriverEntry**例程调用[**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) ，将其自身添加到已注册的微筛选器驱动程序的全局列表中，并向筛选器管理器提供回调例程列表和有关驱动程序的其他信息。

在 MiniSpy 示例中，将注册微筛选器驱动程序，如下面的代码示例所示：

```cpp
NTSTATUS status;
status = FltRegisterFilter(
           DriverObject,                  //Driver
           &FilterRegistration,           //Registration
           &MiniSpyData.FilterHandle);    //RetFilter
```

**FltRegisterFilter** 有两个输入参数。 第一个 *驱动*程序是微筛选器驱动程序作为 *DriverObject* 输入参数接收到其 **DriverEntry** 例程的驱动程序对象指针。 第二个 *注册*是指向 [**FLT \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration) 结构的指针，该结构包含微筛选器驱动程序的回调例程的入口点。

此外， **FltRegisterFilter** 还具有一个输出参数 *RetFilter*，该参数接收微筛选器驱动程序的不透明筛选器指针。 对于许多 **Flt**_Xxx_ 支持例程（包括 [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering) 和 [**FltUnregisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)），此筛选器指针是必需的输入参数。

 

