---
title: 将 ECPs 附加到内核模式驱动程序生成的 IRP_MJ_CREATE 操作
description: 将 ECP 附加到产生内核模式驱动程序的 IRP_MJ_CREATE 操作
ms.assetid: 87daa861-b0d5-4877-bf16-fad120108de6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 229ecc8cfbf0f7c6b661ce6222dee804a9e72356
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841489"
---
# <a name="attaching-ecps-to-irp_mj_create-operations-that-a-kernel-mode-driver-originated"></a>将 ECPs 附加到 IRP\_MJ\_创建内核模式驱动程序生成的操作


必须执行以下步骤来设置 ECPs，并将 ECPs 附加到[**IRP\_MJ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)在文件上创建操作：

1.  调用[**FltAllocateExtraCreateParameterList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterlist)或[**FsRtlAllocateExtraCreateParameterList**](https://msdn.microsoft.com/library/windows/hardware/ff545632)例程为[ECP\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构分配内存。 操作系统不会自动释放 ECP\_列表结构。 相反，在分配 ECP\_列表结构后，微筛选器驱动程序必须最终调用[**FltFreeExtraCreateParameterList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist)或[**FsRtlFreeExtraCreateParameterList**](https://msdn.microsoft.com/library/windows/hardware/ff546005)例程来释放 ECP\_列表。

2.  调用[**FltAllocateExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter)或[**FSRTLALLOCATEEXTRACREATEPARAMETER**](https://msdn.microsoft.com/library/windows/hardware/ff545609)例程为 ECP 上下文结构分配页面内存池，并生成指向该结构的指针。

3.  调用[**FltInsertExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter)或[**FsRtlInsertExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546179)例程，将 Ecp 上下文结构插入[ecp\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

4.  调用[**IoInitializeDriverCreateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioinitializedrivercreatecontext)例程来初始化[**IO\_驱动程序\_创建\_的上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)结构。

5.  定义[**IO\_驱动程序\_创建\_的上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)结构。 在此定义中，将**IO\_驱动程序**的**ExtraCreateParameter**成员指向\_将\_上下文创建到[ECP\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

6.  调用[**FltCreateFileEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefileex2)或[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)例程，将 ECPs 附加到该文件上的[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作。 在此调用中，将指针传递到[**IO\_驱动程序\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context) *DRIVERCONTEXT*参数\_上下文结构。

7.  调用[**FltFreeExtraCreateParameterList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist)或[**FsRtlFreeExtraCreateParameterList**](https://msdn.microsoft.com/library/windows/hardware/ff546005)例程来释放[ECP\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

 

 




