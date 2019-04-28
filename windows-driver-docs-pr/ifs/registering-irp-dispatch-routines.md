---
title: 注册 IRP 调度例程
description: 注册 IRP 调度例程
ms.assetid: 096f4bb7-2326-4e6c-b3db-a2d95ca4982b
keywords:
- 注册 IRP 调度例程
- 调度例程 WDK 文件系统
- IRP 调度例程 WDK 文件系统，注册
- Irp WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b658a41298600c8216500b8a8c8eeeb6b8e262
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344587"
---
# <a name="registering-irp-dispatch-routines"></a>注册 IRP 调度例程


## <span id="ddk_registering_irp_dispatch_routines_if"></span><span id="DDK_REGISTERING_IRP_DISPATCH_ROUTINES_IF"></span>


*DriverObject*筛选器驱动程序的参数[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程提供筛选器驱动程序的一个指向[**驱动程序对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)。 若要注册 I/O 请求数据包 (IRP) 调度例程，必须将存储到这些例程的入口点**MajorFunction**驱动程序对象的成员。 例如，假设"MyLegacyFilter"驱动程序可以按如下所示设置其调度例程的入口点：

```cpp
for (i = 0; i <= IRP_MJ_MAXIMUM_FUNCTION; i++) {
    DriverObject->MajorFunction[i] = MyLegacyFilterDispatch;
}
DriverObject->MajorFunction[IRP_MJ_CREATE] = MyLegacyFilterCreate;
DriverObject->MajorFunction[IRP_MJ_CLOSE] = MyLegacyFilterClose;
DriverObject->MajorFunction[IRP_MJ_FILE_SYSTEM_CONTROL] = MyLegacyFilterFsControl;
```

请注意，上述**为**循环分配所有 IRP 主要函数代码的默认调度例程。 此分配是好的做法，因为否则 I/O 管理器完成状态为任何无法识别的 IRP\_无效\_设备\_默认情况下请求。 文件系统筛选器驱动程序不应拒绝不熟悉 Irp 这种方式，因为此类请求通常适用于驱动程序堆栈中较低级别的另一个驱动程序。 出于此原因，默认的调度例程通常只需将传递到下一步低级驱动程序 IRP。

 

 




