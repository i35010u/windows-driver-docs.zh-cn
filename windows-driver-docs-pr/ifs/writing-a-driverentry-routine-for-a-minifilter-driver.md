---
title: 编写微筛选器驱动程序的 DriverEntry 例程
description: 编写微筛选器驱动程序的 DriverEntry 例程
ms.assetid: 949b4087-47de-4145-87dd-d618db44a15b
keywords:
- 文件系统微筛选器驱动程序 WDK，DriverEntry 例程
- 微筛选器驱动程序 WDK，DriverEntry 例程
- DriverEntry WDK 文件系统
- 全局初始化 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 330c135c03d1df800900d2f29ebfe2c34838b88d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067350"
---
# <a name="writing-a-driverentry-routine-for-a-minifilter-driver"></a>编写微筛选器驱动程序的 DriverEntry 例程


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


每个文件系统微筛选器驱动程序必须具有 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程。 加载微筛选器驱动程序时，将调用 **DriverEntry** 例程。

**DriverEntry**例程执行全局初始化，注册微筛选器驱动程序，并启动筛选。 此例程在具有 IRQL 被动级别的系统线程上下文中运行 \_ 。

**DriverEntry**例程定义如下：

```cpp
NTSTATUS 
(*PDRIVER_INITIALIZE) ( 
    IN PDRIVER_OBJECT DriverObject, 
    IN PUNICODE_STRING RegistryPath 
    ); 
```

**DriverEntry** 有两个输入参数。 第一个是 *DriverObject*，它是在加载微筛选器驱动程序时创建的驱动程序对象。 第二个 *RegistryPath*是一个指针，指向包含微筛选器驱动程序的注册表项的路径的计数 Unicode 字符串。

微筛选器驱动程序的 **DriverEntry** 例程必须按顺序执行以下步骤：

1.  对微筛选器驱动程序执行任何所需的全局初始化。

2.  通过调用 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)注册微筛选器驱动程序。

3.  通过调用 [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)启动筛选。

4.  返回相应的 NTSTATUS 值。

本节包括：

[注册微筛选器驱动程序](registering-the-minifilter-driver.md)

[发起筛选](initiating-filtering.md)

[从微筛选器 DriverEntry 例程返回状态](returning-status.md)

 

