---
title: 注册微筛选器驱动程序
description: 注册微筛选器驱动程序
ms.assetid: 943082c9-dcff-478f-80ba-2a2e72f6ead2
keywords:
- 注册微筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7479cb6139d593b764aa1c69b2156944649b56cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370101"
---
# <a name="registering-the-minifilter-driver"></a>注册微筛选器驱动程序


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


每个微筛选器驱动程序必须调用[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)从其**DriverEntry**例程可以将其添加到已注册微筛选器驱动程序的全局列表，并为具有一系列回调例程和驱动程序有关的其他信息的筛选器管理器。

在 MiniSpy 示例中，微筛选器驱动程序是已注册，如下面的代码示例中所示：

```cpp
NTSTATUS status;
status = FltRegisterFilter(
           DriverObject,                  //Driver
           &FilterRegistration,           //Registration
           &MiniSpyData.FilterHandle);    //RetFilter
```

**FltRegisterFilter**具有两个输入参数。 第一种*驱动程序*，是作为接收微筛选器驱动程序的驱动程序对象指针*DriverObject*输入的参数及其**DriverEntry**例程。 第二类是*注册*，指向的指针[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)结构，其中包含条目指向微筛选器驱动程序的回调例程。

此外， **FltRegisterFilter**具有输出参数*RetFilter*，用于接收微筛选器驱动程序的不透明的筛选器指针。 此筛选器指针是必需的输入的参数为许多 **Flt * * * Xxx*支持例程，其中包括[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)并[ **FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)。

 

 




