---
title: 初始化文件系统筛选器驱动程序
description: 初始化文件系统筛选器驱动程序
ms.assetid: 8a487665-0210-49f5-af91-de78de982506
keywords:
- 初始化筛选器驱动程序
- 筛选驱动程序 WDK 文件系统中，初始化
- 文件系统筛选器驱动程序 WDK，初始化
- DriverEntry WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fdc1ff1582d1cdd3b3b3f8c81f5b35fc21d4b30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380947"
---
# <a name="initializing-a-file-system-filter-driver"></a>初始化文件系统筛选器驱动程序


## <span id="ddk_initializing_a_file_system_filter_driver_if"></span><span id="DDK_INITIALIZING_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程对于初始化文件系统筛选器驱动程序是非常类似于**DriverEntry**例程用于初始化设备驱动程序。 加载驱动程序后，加载了驱动程序的组件还可以初始化该驱动程序通过调用在驱动程序**DriverEntry**例程。 文件系统筛选器驱动程序，请加载驱动程序的组件是 I/O Manager (其启动类型为服务的筛选器\_启动\_启动) 或服务控制管理器 （适用于其他开始类型）。

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程运行在系统线程上下文在 IRQL = 被动\_级别。 此例程可以是可分页，并且应该在 INIT 段中，以便它将被放弃。 有关如何使您的驱动程序代码可分页的详细信息，请参阅备注部分[ **MmLockPagableCodeSection**](https://msdn.microsoft.com/library/windows/hardware/ff554601)。

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程定义，如下所示：

```cpp
NTSTATUS 
(*PDRIVER_INITIALIZE) ( 
    IN PDRIVER_OBJECT DriverObject, 
    IN PUNICODE_STRING RegistryPath 
    ); 
```

此例程具有两个输入的参数。 第一种*DriverObject*，是文件系统筛选器驱动程序加载时创建的驱动程序对象。 第二类是*RegistryPath*，指向包含驱动程序的注册表项的路径的计数 Unicode 字符串的指针。

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程的文件系统筛选器驱动程序将执行以下步骤：

[创建控件设备对象](creating-the-control-device-object.md)

[注册 IRP 调度例程](registering-irp-dispatch-routines.md)

[注册快速 I/O 调度例程](registering-fast-i-o-dispatch-routines.md)

[注册 FsFilter 回调例程](registering-fsfilter-callback-routines.md)

[执行所需的任何其他初始化](performing-any-other-needed-initialization.md)

[\[可选\]注册回调例程](-optional--registering-callback-routines.md)

[\[可选\]保存注册表路径字符串的副本](-optional--saving-a-copy-of-the-registry-path-string.md)

[返回状态](returning-status.md)

 

 




