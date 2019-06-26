---
title: 将 ECPs 附加到内核模式驱动程序产生的 IRP_MJ_CREATE 操作
description: 将 ECP 附加到产生内核模式驱动程序的 IRP_MJ_CREATE 操作
ms.assetid: 87daa861-b0d5-4877-bf16-fad120108de6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47446a0bbe085f18e9ec9ce816d12f96b6a39e2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385324"
---
# <a name="attaching-ecps-to-irpmjcreate-operations-that-a-kernel-mode-driver-originated"></a>将 ECPs 附加到 IRP\_MJ\_内核模式驱动程序产生的创建操作


必须执行以下步骤来设置 ECPs 和附加到 ECPs [ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)文件中的操作：

1.  调用[ **FltAllocateExtraCreateParameterList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocateextracreateparameterlist)或[ **FsRtlAllocateExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff545632)例程来分配内存有关[ECP\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。 操作系统不会自动释放 ECP\_列表结构。 相反之后在 ECP,\_分配列表结构，微筛选器驱动程序最终必须调用[ **FltFreeExtraCreateParameterList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist)或[ **FsRtlFreeExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff546005)例程来释放 ECP\_列表。

2.  调用[ **FltAllocateExtraCreateParameter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocateextracreateparameter)或[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)例程分配分页的内存池为 ECP 上下文结构，并生成指向该结构的指针。

3.  调用[ **FltInsertExtraCreateParameter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinsertextracreateparameter)或[ **FsRtlInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546179)例程，以插入 ECP 上下文结构到[ECP\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

4.  调用[ **IoInitializeDriverCreateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioinitializedrivercreatecontext)例程来初始化[ **IO\_驱动程序\_创建\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_io_driver_create_context)结构。

5.  定义[ **IO\_驱动程序\_创建\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_io_driver_create_context)结构。 在此定义中，依次**ExtraCreateParameter**的成员**IO\_驱动程序\_创建\_上下文**到[ECP\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

6.  调用[ **FltCreateFileEx2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex2)或[ **IoCreateFileEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)例程，以将附加到 ECPs [ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)文件上的操作。 在此调用将传递一个指向[ **IO\_驱动程序\_创建\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_io_driver_create_context)结构*DriverContext*参数。

7.  调用[ **FltFreeExtraCreateParameterList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist)或[ **FsRtlFreeExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff546005)例程来释放[ECP\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

 

 




