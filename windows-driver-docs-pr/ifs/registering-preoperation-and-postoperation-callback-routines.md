---
title: 注册预操作和后操作回调例程
description: 注册预操作和后操作回调例程
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，注册
- postoperation 回调例程 WDK 文件系统微筛选器，注册
- 注册回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04c13cead82631be2ea9d36d4d9b0cc9a47aff58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840723"
---
# <a name="registering-preoperation-and-postoperation-callback-routines"></a>注册预操作和后操作回调例程


## <span id="ddk_registering_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_REGISTERING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


若要注册 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)和 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)，微筛选器驱动程序会在其 **DriverEntry** 例程中调用 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 。 对于 **FltRegisterFilter** 中的 *注册* 参数，微筛选器驱动程序将指针传递到 [**FLT \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构。 此结构的 **OperationRegistration** 成员包含一个指向 [**FLT \_ 操作 \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration) 结构数组的指针，该指针用于微筛选器驱动程序必须筛选的每种类型的 i/o 操作。

数组中的每个 FLT \_ 操作 \_ 注册结构（最后一个）都包含以下信息：

-   操作的主要函数代码。 有关 i/o 操作的信息以及特定于请求类型的参数，请参阅 [FLT_PARAMETERS](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 。

-   对于读取和写入操作 (IRP \_ mj \_ 读取和 IRP \_ mj \_ 写入) ，这是一组标志，用于指定是否忽略缓存的 i/o 或分页 i/o，或者两者都用于基于 IRP 的 i/o 操作

-   最多一个 preoperation 回调例程和一个 postoperation 回调例程的入口点

数组中的最后一个元素必须为 {IRP \_ MJ \_ 操作 \_ 结束}。

下面的代码示例来自扫描仪示例微筛选器驱动程序，它显示 FLT \_ 操作注册结构的数组 \_ 。 扫描器示例微筛选器驱动程序为 irp mj \_ \_ CREATE 和 preoperation 回调例程注册 irp mj CREATE 和 irp \_ \_ \_ mj \_ 写入操作的 preoperation 和 postoperation 回调例程。

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

 

