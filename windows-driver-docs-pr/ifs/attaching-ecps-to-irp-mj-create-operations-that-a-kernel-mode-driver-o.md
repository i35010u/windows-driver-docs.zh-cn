---
title: 将 ECPs 附加到 Kernel-Mode 驱动程序产生 IRP_MJ_CREATE 操作
description: 将 ECP 附加到产生内核模式驱动程序的 IRP_MJ_CREATE 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7d827d4315402b92bce204d6204d3b81a9cab66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803565"
---
# <a name="attaching-ecps-to-irp_mj_create-operations-that-a-kernel-mode-driver-originated"></a>将 ECPs 附加到 \_ \_ Kernel-Mode 驱动程序生成的 IRP MJ CREATE 操作


必须按照以下步骤设置 ECPs，并将 ECPs 附加到文件的 [**IRP \_ MJ \_ CREATE**](./irp-mj-create.md) 操作：

1.  调用 [**FltAllocateExtraCreateParameterList**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterlist) 或 [**FsRtlAllocateExtraCreateParameterList**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameterlist) 例程为 [ECP \_ 列表](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85)) 结构分配内存。 操作系统不会自动释放 ECP \_ 列表结构。 相反，在分配 ECP \_ 列表结构后，微筛选器驱动程序必须最终调用 [**FltFreeExtraCreateParameterList**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist) 或 [**FSRTLFREEEXTRACREATEPARAMETERLIST**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfreeextracreateparameterlist) 例程来释放 ecp \_ 列表。

2.  调用 [**FltAllocateExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter) 或 [**FSRTLALLOCATEEXTRACREATEPARAMETER**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameter) 例程为 ECP 上下文结构分配页面内存池，并生成指向该结构的指针。

3.  调用 [**FltInsertExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter) 或 [**FsRtlInsertExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinsertextracreateparameter) 例程，将 Ecp 上下文结构插入 [ecp \_ 列表](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85)) 结构。

4.  调用 [**IoInitializeDriverCreateContext**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioinitializedrivercreatecontext) 例程以初始化 [**IO \_ 驱动程序 \_ 创建 \_ 上下文**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context) 结构。

5.  定义 [**IO \_ 驱动程序 \_ 创建 \_ 上下文**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context) 结构。 在此定义中，将 **IO \_ 驱动程序 \_ \_** 的 **ExtraCreateParameter** 成员指向 [ECP \_ 列表](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

6.  调用 [**FltCreateFileEx2**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefileex2) 或 [**IoCreateFileEx**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex) 例程，将 ECPs 附加到该文件上的 [**IRP \_ MJ \_ CREATE**](./irp-mj-create.md) 操作。 在此调用中，向 *DriverContext* 参数传递一个指向 [**IO \_ 驱动程序 \_ CREATE \_ 上下文**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)结构的指针。

7.  调用 [**FltFreeExtraCreateParameterList**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameterlist) 或 [**FsRtlFreeExtraCreateParameterList**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfreeextracreateparameterlist) 例程来释放 [ECP \_ 列表](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85)) 结构。

 

