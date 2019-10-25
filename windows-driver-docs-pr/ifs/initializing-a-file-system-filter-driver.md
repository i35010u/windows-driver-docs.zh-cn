---
title: 初始化文件系统筛选器驱动程序
description: 初始化文件系统筛选器驱动程序
ms.assetid: 8a487665-0210-49f5-af91-de78de982506
keywords:
- 初始化筛选器驱动程序
- 筛选器驱动程序 WDK 文件系统，初始化
- 文件系统筛选器驱动程序 WDK，初始化
- DriverEntry WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49f2a025fd1d6ce3aaf79cbc72bb346bc3473ef6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841201"
---
# <a name="initializing-a-file-system-filter-driver"></a>初始化文件系统筛选器驱动程序


## <span id="ddk_initializing_a_file_system_filter_driver_if"></span><span id="DDK_INITIALIZING_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


用于初始化文件系统筛选器驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程与用于初始化设备驱动程序的**DriverEntry**例程非常类似。 加载驱动程序后，加载驱动程序的同一组件还会通过调用驱动程序的**DriverEntry**例程来初始化驱动程序。 对于文件系统筛选器驱动程序，加载驱动程序的组件可以是 i/o 管理器（对于其启动类型为 SERVICE\_BOOT\_START）或服务控制管理器（对于其他启动类型）。

[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程在系统线程上下文中以 IRQL = 被动\_级别运行。 此例程可以是可分页的，并且应在 INIT 段中，以便丢弃。 有关如何使驱动程序代码可分页的详细信息，请参阅[**MmLockPagableCodeSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection)的 "备注" 部分。

[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程定义如下：

```cpp
NTSTATUS 
(*PDRIVER_INITIALIZE) ( 
    IN PDRIVER_OBJECT DriverObject, 
    IN PUNICODE_STRING RegistryPath 
    ); 
```

此例程有两个输入参数。 第一个是*DriverObject*，它是在加载文件系统筛选器驱动程序时创建的驱动程序对象。 第二个*RegistryPath*是一个指针，指向包含驱动程序注册表项路径的计数 Unicode 字符串。

文件系统筛选器驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程执行以下步骤：

[创建控制设备对象](creating-the-control-device-object.md)

[正在注册 IRP 调度例程](registering-irp-dispatch-routines.md)

[注册快速 i/o 调度例程](registering-fast-i-o-dispatch-routines.md)

[注册 FsFilter 回调例程](registering-fsfilter-callback-routines.md)

[执行任何其他需要的初始化](performing-any-other-needed-initialization.md)

[注册回调例程\[可选\]](-optional--registering-callback-routines.md)

[\[可选\] 保存注册表路径字符串的副本](-optional--saving-a-copy-of-the-registry-path-string.md)

[返回状态](returning-status.md)

 

 




