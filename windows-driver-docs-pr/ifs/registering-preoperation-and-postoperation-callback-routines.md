---
title: 注册预操作和后操作回调例程
description: 注册预操作和后操作回调例程
ms.assetid: 9f89ca46-8a8f-422f-9dbe-2620b944a3ae
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，注册
- postoperation 回调例程 WDK 文件系统微筛选器，注册
- 注册回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e26784ccc76f44d5af7e001502467719aa759d71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576897"
---
# <a name="registering-preoperation-and-postoperation-callback-routines"></a>注册预操作和后操作回调例程


## <span id="ddk_registering_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_REGISTERING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


若要注册[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)并[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)，微筛选器驱动程序进行单一调用向[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)中其**DriverEntry**例程。 有关*注册*中的参数**FltRegisterFilter**，微筛选器驱动程序将传递一个指向[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)结构。 **OperationRegistration**此结构的成员包含的数组的指针[ **FLT\_操作\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544668)结构，一个用于每种类型的微筛选器驱动程序必须筛选的 I/O 操作。

每个 FLT\_操作\_在数组中，除最后一个注册结构包含以下信息：

-   操作的主要函数代码。 请参阅[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)有关 I/O 操作和其请求类型特定的参数信息。

-   用于读取和写入操作 (IRP\_MJ\_IRP 读\_MJ\_编写)，一组标志，用于指定是否忽略缓存 I/O 分页 I/O 和 / 或基于 IRP 的 I/O 操作

-   最多为 1 个 preoperation 回调例程和一个 postoperation 回调例程的入口点

数组中的最后一个元素必须是 {IRP\_MJ\_操作\_最终}。

下面的代码示例摘自扫描程序示例微筛选器驱动程序，显示了一个数组 FLT\_操作\_注册结构。 扫描程序示例微筛选器驱动程序注册 preoperation 和 postoperation 回调例程 IRP\_MJ\_创建和 IRP 的 preoperation 回调例程\_MJ\_清理和 IRP\_MJ\_写入操作。

```cpp
const FLT_OPERATION_REGISTRATION Callbacks[] = {
    {IRP_MJ_CREATE,
     0,
     ScannerPreCreate,
     ScannerPostCreate},
    {IRP_MJ_CLEANUP,
     0, 
     ScannerPreCleanup,
     NULL},
    {IRP_MJ_WRITE,
     0, 
     ScannerPreWrite,
     NULL},
    {IRP_MJ_OPERATION_END}
};
```

 

 




