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
ms.openlocfilehash: 0500bc598ecc9bdc954dd92bd3e4268d787673fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841003"
---
# <a name="registering-preoperation-and-postoperation-callback-routines"></a>注册预操作和后操作回调例程


## <span id="ddk_registering_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_REGISTERING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


若要注册[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)和[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)，微筛选器驱动程序会在其**DriverEntry**例程中调用[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 。 对于**FltRegisterFilter**中的*注册*参数，微筛选器驱动程序传递指向[**FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的指针。 此结构中的**OperationRegistration**成员包含一个指向[**FLT\_\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration)的数组的指针，该数组适用于微筛选器驱动程序必须筛选的每种类型的 i/o 操作。

数组中的每个 FLT\_操作\_注册结构（最后一个除外）包含以下信息：

-   操作的主要函数代码。 请参阅[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) ，了解 i/o 操作及其特定于请求类型的参数的相关信息。

-   对于读取和写入操作（IRP\_MJ\_读取和 IRP\_MJ\_写入），这是一组标志，用于指定是否忽略缓存的 i/o 或分页 i/o，或者两者都用于基于 IRP 的 i/o 操作

-   最多一个 preoperation 回调例程和一个 postoperation 回调例程的入口点

数组中的最后一个元素必须是 {IRP\_MJ\_操作\_END}。

下面的代码示例摘自 Scanner 示例微筛选器驱动程序，其中显示了 FLT\_操作的数组\_注册结构。 Scanner 示例微筛选器驱动程序为 IRP\_MJ 注册了 preoperation 和 postoperation 回调例程\_创建和 preoperation 用于 IRP 的回调例程\_\_\_

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

 

 




