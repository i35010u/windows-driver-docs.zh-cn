---
title: 使用 ECPs 在文件系统筛选器驱动程序中处理 IRP_MJ_CREATE
description: 在文件系统筛选器驱动程序中使用 ECP 处理 IRP_MJ_CREATE 操作
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3bb2f6874df41aa2aa2668927993d9f884bd1a67
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841119"
---
# <a name="using-ecps-to-process-irp_mj_create-operations-in-a-file-system-filter-driver"></a>在文件系统筛选器驱动程序中使用 ECP 处理 IRP_MJ_CREATE 操作

您可以使用文件系统筛选器驱动程序中的 ECPs 来处理 [**IRP_MJ_CREATE**](./irp-mj-create.md) 操作。 文件系统筛选器驱动程序可以调用以下部分中的例程来检索、确认、添加和删除 **IRP_MJ_CREATE** 操作的 ECPs。 还可以确定 ECPs 源自的操作系统空间。

## <a name="retrieving-ecps"></a>正在检索 ECPs

文件系统筛选器驱动程序可以按照以下步骤来检索 [**IRP_MJ_CREATE**](./irp-mj-create.md) 操作的 ECPs：

1. 调用 [**FltGetEcpListFromCallbackData**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetecplistfromcallbackdata) 或 [**FsRtlGetEcpListFromIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlgetecplistfromirp) 例程来检索指向 ECP 上下文结构列表的指针 (与创建操作关联 ECP_LIST) 。

2. 执行下列任一操作：
    - 调用 [**FltGetNextExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetnextextracreateparameter) 或 [**FsRtlGetNextExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlgetnextextracreateparameter) 例程来检索指向 ecp 列表中下一个 (或第一个) ECP 上下文结构的指针。
    - 调用 [**FltFindExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfindextracreateparameter) 或 [**FSRTLFINDEXTRACREATEPARAMETER**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfindextracreateparameter) 例程搜索 ecp 列表，查找给定类型的 ecp 上下文结构。 如果找到结构，则任何一个例程都将返回指向 ECP 上下文结构的指针。

## <a name="setting-ecps"></a>设置 ECPs

若要为 [**IRP_MJ_CREATE**](./irp-mj-create.md) 操作设置 ECPs，您的文件系统筛选器驱动程序可以首先检索现有 ECP 上下文结构列表 (与创建操作相关联的 ECP_LIST) ，或者分配 ECP_LIST 和 ecp 上下文结构，然后在 ECP_LIST 中插入 ecp 上下文结构。

### <a name="setting-ecps-in-an-existing-ecp_list"></a>在现有 ECP_LIST 中设置 ECPs

文件系统筛选器驱动程序可以按照以下步骤在与创建操作关联的现有 ECP_LIST 中设置 ECPs：

1. 调用 [**FltGetEcpListFromCallbackData**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetecplistfromcallbackdata) 或 [**FsRtlGetEcpListFromIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlgetecplistfromirp) 例程来检索指向 ECP 上下文结构列表的指针 (与创建操作关联 ECP_LIST) 。

2. 调用 [**FltAllocateExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter) 或 [**FSRTLALLOCATEEXTRACREATEPARAMETER**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameter) 例程为 ECP 上下文结构分配页面内存池，并生成指向该结构的指针。

3. 调用 [**FltInsertExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter) 或 [**FsRtlInsertExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinsertextracreateparameter) 例程，将 ECP 上下文结构插入 [ECP_LIST](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85)) 结构。

### <a name="setting-ecps-in-a-newly-created-ecp_list"></a>在新创建的 ECP_LIST 中设置 ECPs

文件系统筛选器驱动程序可以按照以下步骤在与创建操作关联的新创建 ECP_LIST 中设置 ECPs：

1. 调用 [**FltAllocateExtraCreateParameterList**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterlist) 或 [**FsRtlAllocateExtraCreateParameterList**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameterlist) 例程为 [ECP_LIST](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85)) 结构分配内存。

2. 调用 [**FltAllocateExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter) 或 [**FSRTLALLOCATEEXTRACREATEPARAMETER**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameter) 例程为 ECP 上下文结构分配页面内存池，并生成指向该结构的指针。

3. 调用 [**FltInsertExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter) 或 [**FsRtlInsertExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinsertextracreateparameter) 例程，将 ECP 上下文结构插入 [ECP_LIST](/previous-versions/windows/hardware/drivers/ff540148(v=vs.85)) 结构。

4. 调用 [**FltSetEcpListIntoCallbackData**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetecplistintocallbackdata) 或 [**FSRTLSETECPLISTINTOIRP**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlsetecplistintoirp) 例程将 ECP 列表附加到创建操作。

## <a name="removing-ecps"></a>删除 ECPs

文件系统筛选器驱动程序可以按照以下步骤删除 [**IRP_MJ_CREATE**](./irp-mj-create.md) 操作的 ECPs：

1. 调用 [**FltRemoveExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltremoveextracreateparameter) 或 [**FsRtlRemoveExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlremoveextracreateparameter) 例程搜索 ECP 上下文结构的 ecp 列表。 如果找到 ECP 上下文结构，例程将从 ECP 列表中分离 ECP 上下文结构。

2. 若要释放分离的 ECP 上下文结构的内存，请调用 [**FltFreeExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameter) 或 [**FsRtlFreeExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfreeextracreateparameter) 例程。 如果已通过下列方式之一分配内存，则可以调用这些例程来释放 ECP 上下文结构的内存：

    - 你调用了 [**FltAllocateExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter) 或 [**FsRtlAllocateExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameter) 例程来分配分页的内存池
    - 你调用了 [**FltAllocateExtraCreateParameterFromLookasideList**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterfromlookasidelist) 或 [**FsRtlAllocateExtraCreateParameterFromLookasideList**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameterfromlookasidelist) 例程来从后备链表列表分配内存池

## <a name="marking-ecps-as-acknowledged-or-determining-acknowledge-status"></a>将 ECPs 标记为已确认或确定确认状态

文件系统筛选器驱动程序可以调用以下例程，将 ECPs 标记为 "已确认" 或确定是否将 ECPs 标记为 "已确认"：

- 调用 [**FltAcknowledgeEcp**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltacknowledgeecp) 或 [**FSRTLACKNOWLEDGEECP**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlacknowledgeecp) 例程将 ECP 上下文结构标记为已确认。 可以将 ECP 标记为查看、使用、处理或 ECP 的任何其他条件。

- 调用 [**FltIsEcpAcknowledged**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisecpacknowledged) 或 [**FsRtlIsEcpAcknowledged**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlisecpacknowledged) 例程来确定 ECP 上下文结构是否被标记为已确认。

## <a name="determining-origination-mode"></a>确定始发模式

文件系统筛选器驱动程序可以调用 [**FltIsEcpFromUserMode**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisecpfromusermode) 或 [**FsRtlIsEcpFromUserMode**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlisecpfromusermode) 例程来确定 ECP 上下文结构是否源自用户模式。 文件系统筛选器驱动程序可以拒绝接受源自用户模式的 ECP 上下文结构。

## <a name="using-lookaside-lists-to-allocate-ecps"></a>使用后备链表列表分配 ECPs

文件系统筛选器驱动程序可以调用以下例程来从后备链表列表分配 ECPs 并管理后备链表列表和 ECPs：

- 调用 [**FltInitExtraCreateParameterLookasideList**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitextracreateparameterlookasidelist) 或 [**FsRtlInitExtraCreateParameterLookasideList**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitextracreateparameterlookasidelist) 例程来初始化分页或非分页池后备链表列表，该列表用于分配固定大小的一个或多个 ECP 上下文结构。

- 调用 [**FltDeleteExtraCreateParameterLookasideList**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeleteextracreateparameterlookasidelist) 或 [**FsRtlDeleteExtraCreateParameterLookasideList**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtldeleteextracreateparameterlookasidelist) 例程来释放后备链表列表。

- 调用 [**FltAllocateExtraCreateParameterFromLookasideList**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterfromlookasidelist) 或 [**FSRTLALLOCATEEXTRACREATEPARAMETERFROMLOOKASIDELIST**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlallocateextracreateparameterfromlookasidelist) 例程从 ECP 上下文结构的后备链表列表中分配内存池，并生成指向该结构的指针。

- 调用 [**FltFreeExtraCreateParameter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameter) 或 [**FsRtlFreeExtraCreateParameter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfreeextracreateparameter) 例程来释放 ECP 上下文结构的内存。
