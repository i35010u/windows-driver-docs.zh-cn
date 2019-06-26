---
title: 编写微筛选器驱动程序的 DriverEntry 例程
description: 编写微筛选器驱动程序的 DriverEntry 例程
ms.assetid: 949b4087-47de-4145-87dd-d618db44a15b
keywords:
- 文件系统微筛选器驱动程序 WDK，DriverEntry 例程
- 微筛选器驱动程序 WDK，DriverEntry 例程
- DriverEntry WDK 的文件系统
- 全局初始化 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4730883cc7668e781af09d90a675e62d6c37744e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371285"
---
# <a name="writing-a-driverentry-routine-for-a-minifilter-driver"></a>编写微筛选器驱动程序的 DriverEntry 例程


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


每个文件系统微筛选器驱动程序必须具有[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。 **DriverEntry**微筛选器驱动程序加载时调用例程。

**DriverEntry**例程执行全局初始化、 注册微筛选器驱动程序，并启动筛选。 此例程在 IRQL 被动系统线程上下文中运行\_级别。

**DriverEntry**例程定义，如下所示：

```cpp
NTSTATUS 
(*PDRIVER_INITIALIZE) ( 
    IN PDRIVER_OBJECT DriverObject, 
    IN PUNICODE_STRING RegistryPath 
    ); 
```

**DriverEntry**具有两个输入参数。 第一种*DriverObject*，是微筛选器驱动程序加载时创建的驱动程序对象。 第二类是*RegistryPath*，指向包含微筛选器驱动程序的注册表项的路径的计数 Unicode 字符串的指针。

微筛选器驱动程序**DriverEntry**例程必须按顺序执行以下步骤：

1.  微筛选器驱动程序执行任何所需的全局初始化。

2.  通过调用注册微筛选器驱动程序[ **FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)。

3.  启动筛选通过调用[ **FltStartFiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)。

4.  返回适当的 NTSTATUS 值。

本部分包括：

[注册微筛选器驱动程序](registering-the-minifilter-driver.md)

[启动筛选](initiating-filtering.md)

[从一个微筛选器 DriverEntry 例程返回状态](returning-status.md)

 

 




