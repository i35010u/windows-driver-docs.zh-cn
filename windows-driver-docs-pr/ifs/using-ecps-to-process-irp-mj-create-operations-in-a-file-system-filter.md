---
title: 使用 ECPs 处理文件系统筛选器驱动程序中的 IRP_MJ_CREATE
description: 使用 ECPs 在文件系统筛选器驱动程序中处理 IRP_MJ_CREATE 操作
ms.assetid: 969709a9-cdca-4a1a-95a0-0bb89cd17693
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 763995726a6553b3a458a8bce1214a37d5ead892
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840941"
---
# <a name="using-ecps-to-process-irp_mj_create-operations-in-a-file-system-filter-driver"></a>使用 ECPs 在文件系统筛选器驱动程序中处理 IRP\_MJ\_创建操作


您可以使用文件系统筛选器驱动程序中的 ECPs 来处理[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作。 文件系统筛选器驱动程序可以调用以下部分中的例程，为**IRP\_MJ\_创建**操作检索、确认、添加和删除 ECPs。 还可以确定 ECPs 源自的操作系统空间。

### <a name="span-idretrieving_ecpsspanspan-idretrieving_ecpsspanspan-idretrieving_ecpsspanretrieving-ecps"></a><span id="Retrieving_ECPs"></span><span id="retrieving_ecps"></span><span id="RETRIEVING_ECPS"></span>正在检索 ECPs

文件系统筛选器驱动程序可以按照以下步骤为[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作检索 ECPs：

1.  调用[**FltGetEcpListFromCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetecplistfromcallbackdata)或[**FsRtlGetEcpListFromIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546015)例程来检索指向与创建操作相关联的 ecp 上下文结构列表（ecp\_列表）的指针。

2.  执行下列任一操作：
    -   调用[**FltGetNextExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetnextextracreateparameter)或[**FsRtlGetNextExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546028)例程来检索指向 ecp 列表中的下一个（或第一个） ecp 上下文结构的指针。
    -   调用[**FltFindExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfindextracreateparameter)或[**FSRTLFINDEXTRACREATEPARAMETER**](https://msdn.microsoft.com/library/windows/hardware/ff545968)例程搜索 ecp 列表，查找给定类型的 ecp 上下文结构。 如果找到结构，则任何一个例程都将返回指向 ECP 上下文结构的指针。

### <a name="span-idsetting_ecpsspanspan-idsetting_ecpsspanspan-idsetting_ecpsspansetting-ecps"></a><span id="Setting_ECPs"></span><span id="setting_ecps"></span><span id="SETTING_ECPS"></span>设置 ECPs

若要为[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作设置 ECPs，您的文件系统筛选器驱动程序可以先检索与创建操作相关联的现有 ECP 上下文结构列表（ECP\_列表），或分配 ECP\_列出和 ECP 上下文结构，并将 ECP 上下文结构插入 ECP\_列表。

文件系统筛选器驱动程序可以按照以下步骤在与创建操作相关联的现有 ECP\_列表中设置 ECPs：

1.  调用[**FltGetEcpListFromCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetecplistfromcallbackdata)或[**FsRtlGetEcpListFromIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546015)例程来检索指向与创建操作相关联的 ecp 上下文结构列表（ecp\_列表）的指针。

2.  调用[**FltAllocateExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter)或[**FSRTLALLOCATEEXTRACREATEPARAMETER**](https://msdn.microsoft.com/library/windows/hardware/ff545609)例程为 ECP 上下文结构分配页面内存池，并生成指向该结构的指针。

3.  调用[**FltInsertExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter)或[**FsRtlInsertExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546179)例程，将 Ecp 上下文结构插入[ecp\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

文件系统筛选器驱动程序可以按照以下步骤在与创建操作关联的新创建的 ECP\_列表中设置 ECPs：

1.  调用[**FltAllocateExtraCreateParameterList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterlist)或[**FsRtlAllocateExtraCreateParameterList**](https://msdn.microsoft.com/library/windows/hardware/ff545632)例程为[ECP\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构分配内存。

2.  调用[**FltAllocateExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter)或[**FSRTLALLOCATEEXTRACREATEPARAMETER**](https://msdn.microsoft.com/library/windows/hardware/ff545609)例程为 ECP 上下文结构分配页面内存池，并生成指向该结构的指针。

3.  调用[**FltInsertExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinsertextracreateparameter)或[**FsRtlInsertExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546179)例程，将 Ecp 上下文结构插入[ecp\_列表](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))结构。

4.  调用[**FltSetEcpListIntoCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetecplistintocallbackdata)或[**FSRTLSETECPLISTINTOIRP**](https://msdn.microsoft.com/library/windows/hardware/ff547250)例程将 ECP 列表附加到创建操作。

### <a name="span-idremoving_ecpsspanspan-idremoving_ecpsspanspan-idremoving_ecpsspanremoving-ecps"></a><span id="Removing_ECPs"></span><span id="removing_ecps"></span><span id="REMOVING_ECPS"></span>删除 ECPs

文件系统筛选器驱动程序可以按照以下步骤删除[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作的 ECPs：

1.  调用[**FltRemoveExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltremoveextracreateparameter)或[**FsRtlRemoveExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff547203)例程搜索 ECP 上下文结构的 ecp 列表。 如果找到 ECP 上下文结构，例程将从 ECP 列表中分离 ECP 上下文结构。

2.  若要释放分离的 ECP 上下文结构的内存，请调用[**FltFreeExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameter)或[**FsRtlFreeExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545989)例程。 如果已通过下列方式之一分配内存，则可以调用这些例程来释放 ECP 上下文结构的内存：
    -   你调用了[**FltAllocateExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameter)或[**FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)例程来分配分页的内存池
    -   你调用了[**FltAllocateExtraCreateParameterFromLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterfromlookasidelist)或[**FsRtlAllocateExtraCreateParameterFromLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545616)例程来从后备链表列表分配内存池

### <a name="span-idmarking_ecps_as_acknowledged__or_determining_acknowledge_statusspanspan-idmarking_ecps_as_acknowledged__or_determining_acknowledge_statusspanspan-idmarking_ecps_as_acknowledged__or_determining_acknowledge_statusspanmarking-ecps-as-acknowledged-or-determining-acknowledge-status"></a><span id="Marking_ECPs_as_Acknowledged__or_Determining_Acknowledge_Status"></span><span id="marking_ecps_as_acknowledged__or_determining_acknowledge_status"></span><span id="MARKING_ECPS_AS_ACKNOWLEDGED__OR_DETERMINING_ACKNOWLEDGE_STATUS"></span>将 ECPs 标记为已确认或确定确认状态

文件系统筛选器驱动程序可以调用以下例程，将 ECPs 标记为 "已确认" 或确定是否将 ECPs 标记为 "已确认"：

-   调用[**FltAcknowledgeEcp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltacknowledgeecp)或[**FSRTLACKNOWLEDGEECP**](https://msdn.microsoft.com/library/windows/hardware/ff545574)例程将 ECP 上下文结构标记为已确认。 可以将 ECP 标记为查看、使用、处理或 ECP 的任何其他条件。

-   调用[**FltIsEcpAcknowledged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisecpacknowledged)或[**FsRtlIsEcpAcknowledged**](https://msdn.microsoft.com/library/windows/hardware/ff546808)例程来确定 ECP 上下文结构是否被标记为已确认。

### <a name="span-iddetermining_origination_modespanspan-iddetermining_origination_modespanspan-iddetermining_origination_modespandetermining-origination-mode"></a><span id="Determining_Origination_Mode"></span><span id="determining_origination_mode"></span><span id="DETERMINING_ORIGINATION_MODE"></span>确定始发模式

文件系统筛选器驱动程序可以调用[**FltIsEcpFromUserMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisecpfromusermode)或[**FsRtlIsEcpFromUserMode**](https://msdn.microsoft.com/library/windows/hardware/ff546813)例程来确定 ECP 上下文结构是否源自用户模式。 文件系统筛选器驱动程序可以拒绝接受源自用户模式的 ECP 上下文结构。

### <a name="span-idusing_lookaside_lists_to_allocate_ecpsspanspan-idusing_lookaside_lists_to_allocate_ecpsspanspan-idusing_lookaside_lists_to_allocate_ecpsspanusing-lookaside-lists-to-allocate-ecps"></a><span id="Using_Lookaside_Lists_to_Allocate_ECPs"></span><span id="using_lookaside_lists_to_allocate_ecps"></span><span id="USING_LOOKASIDE_LISTS_TO_ALLOCATE_ECPS"></span>使用后备链表列表分配 ECPs

文件系统筛选器驱动程序可以调用以下例程来从后备链表列表分配 ECPs 并管理后备链表列表和 ECPs：

-   调用[**FltInitExtraCreateParameterLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitextracreateparameterlookasidelist)或[**FsRtlInitExtraCreateParameterLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff546102)例程来初始化分页或非分页池后备链表列表，该列表用于分配已修复的一个或多个 ECP 上下文结构规格.

-   调用[**FltDeleteExtraCreateParameterLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeleteextracreateparameterlookasidelist)或[**FsRtlDeleteExtraCreateParameterLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545849)例程来释放后备链表列表。

-   调用[**FltAllocateExtraCreateParameterFromLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocateextracreateparameterfromlookasidelist)或[**FSRTLALLOCATEEXTRACREATEPARAMETERFROMLOOKASIDELIST**](https://msdn.microsoft.com/library/windows/hardware/ff545616)例程从 ECP 上下文结构的后备链表列表中分配内存池，并生成指向该构造.

-   调用[**FltFreeExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreeextracreateparameter)或[**FsRtlFreeExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545989)例程来释放 ECP 上下文结构的内存。

 

 




