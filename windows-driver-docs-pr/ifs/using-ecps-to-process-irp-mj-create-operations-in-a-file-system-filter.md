---
title: 使用 ECPs 处理 IRP_MJ_CREATE 在文件系统筛选器驱动程序
description: 在文件系统筛选器驱动程序中使用 ECP 处理 IRP_MJ_CREATE 操作
ms.assetid: 969709a9-cdca-4a1a-95a0-0bb89cd17693
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a05d82d4e6ba4e5fe1be8c36973ca95bb7fe034c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379436"
---
# <a name="using-ecps-to-process-irpmjcreate-operations-in-a-file-system-filter-driver"></a>使用 ECPs 处理 IRP\_MJ\_中的文件系统筛选器驱动程序的创建操作


可以在文件系统筛选器驱动程序中使用 ECPs 来处理[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)操作。 在文件系统筛选器驱动程序可以调用例程在以下部分来检索、 确认、 添加和删除的 ECPs **IRP\_MJ\_创建**操作。 您还可以确定 ECPs 所源自的操作系统空间。

### <a name="span-idretrievingecpsspanspan-idretrievingecpsspanspan-idretrievingecpsspanretrieving-ecps"></a><span id="Retrieving_ECPs"></span><span id="retrieving_ecps"></span><span id="RETRIEVING_ECPS"></span>检索 ECPs

在文件系统筛选器驱动程序可以按照以下步骤检索的 ECPs [ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)操作：

1.  调用[ **FltGetEcpListFromCallbackData** ](https://msdn.microsoft.com/library/windows/hardware/ff543016)或[ **FsRtlGetEcpListFromIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff546015)例程，以检索一个指向 ECP 上下文结构列表 (ECP\_列表) 创建操作与该键相关联。

2.  执行以下操作之一：
    -   调用[ **FltGetNextExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff543104)或[ **FsRtlGetNextExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546028)例程，以检索指向的指针下一个 （或第一个） ECP 上下文结构 ECP 列表中。
    -   调用[ **FltFindExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff542094)或[ **FsRtlFindExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545968)例程，以搜索 ECP ECP 列表上下文将给定类型的结构。 如果找到该结构，任一例程返回指向 ECP 上下文结构的指针。

### <a name="span-idsettingecpsspanspan-idsettingecpsspanspan-idsettingecpsspansetting-ecps"></a><span id="Setting_ECPs"></span><span id="setting_ecps"></span><span id="SETTING_ECPS"></span>设置 ECPs

若要设置为 ECPs [ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)操作，在文件系统筛选器驱动程序可以首先请检索现有 ECP 上下文结构列表 (ECP\_列出），它是使用创建操作时，关联或分配 ECP\_ECP 上下文和列表结构，并在 ECP 中插入 ECP 上下文结构\_列表。

在文件系统筛选器驱动程序可以按照以下步骤在现有 ECP 中设置 ECPs\_与创建操作相关联的列表：

1.  调用[ **FltGetEcpListFromCallbackData** ](https://msdn.microsoft.com/library/windows/hardware/ff543016)或[ **FsRtlGetEcpListFromIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff546015)例程，以检索一个指向 ECP 上下文结构列表 (ECP\_列表) 创建操作与该键相关联。

2.  调用[ **FltAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff541728)或[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)例程分配分页的内存池为 ECP 上下文结构，并生成指向该结构的指针。

3.  调用[ **FltInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff543305)或[ **FsRtlInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546179)例程，以插入 ECP 上下文结构到[ECP\_列表](https://msdn.microsoft.com/library/windows/hardware/ff540148)结构。

在文件系统筛选器驱动程序可以按照以下步骤在新创建的 ECP 中设置 ECPs\_与创建操作相关联的列表：

1.  调用[ **FltAllocateExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff541741)或[ **FsRtlAllocateExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff545632)例程来分配内存有关[ECP\_列表](https://msdn.microsoft.com/library/windows/hardware/ff540148)结构。

2.  调用[ **FltAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff541728)或[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)例程分配分页的内存池为 ECP 上下文结构，并生成指向该结构的指针。

3.  调用[ **FltInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff543305)或[ **FsRtlInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546179)例程，以插入 ECP 上下文结构到[ECP\_列表](https://msdn.microsoft.com/library/windows/hardware/ff540148)结构。

4.  调用[ **FltSetEcpListIntoCallbackData** ](https://msdn.microsoft.com/library/windows/hardware/ff544510)或[ **FsRtlSetEcpListIntoIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff547250)例程，以将 ECP 列表附加到创建操作.

### <a name="span-idremovingecpsspanspan-idremovingecpsspanspan-idremovingecpsspanremoving-ecps"></a><span id="Removing_ECPs"></span><span id="removing_ecps"></span><span id="REMOVING_ECPS"></span>删除 ECPs

在文件系统筛选器驱动程序可以按照以下步骤以删除有关 ECPs [ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)操作：

1.  调用[ **FltRemoveExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff544339)或[ **FsRtlRemoveExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff547203)例程，以搜索 ECP ECP 列表上下文结构。 如果找到 ECP 上下文结构，则例程将分离 ECP 上下文结构从 ECP 列表。

2.  若要释放的已分离的 ECP 上下文结构的内存，调用[ **FltFreeExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff542957)或[ **FsRtlFreeExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545989)例程。 您可以调用这些例程来释放内存 ECP 上下文结构，如果你已分配内存中的以下方法之一：
    -   你调用[ **FltAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff541728)或[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)例程来分配分页内存池
    -   你调用[ **FltAllocateExtraCreateParameterFromLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff541734)或[ **FsRtlAllocateExtraCreateParameterFromLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545616)例程，以从后备链列表分配内存池

### <a name="span-idmarkingecpsasacknowledgedordeterminingacknowledgestatusspanspan-idmarkingecpsasacknowledgedordeterminingacknowledgestatusspanspan-idmarkingecpsasacknowledgedordeterminingacknowledgestatusspanmarking-ecps-as-acknowledged-or-determining-acknowledge-status"></a><span id="Marking_ECPs_as_Acknowledged__or_Determining_Acknowledge_Status"></span><span id="marking_ecps_as_acknowledged__or_determining_acknowledge_status"></span><span id="MARKING_ECPS_AS_ACKNOWLEDGED__OR_DETERMINING_ACKNOWLEDGE_STATUS"></span>将 ECPs 标记为已确认，或确定确认状态

在文件系统筛选器驱动程序可以调用以下例程将 ECPs 标记为已确认或确定 ECPs 是否标记为已确认：

-   调用[ **FltAcknowledgeEcp** ](https://msdn.microsoft.com/library/windows/hardware/ff541661)或[ **FsRtlAcknowledgeEcp** ](https://msdn.microsoft.com/library/windows/hardware/ff545574)例程，以将 ECP 上下文结构标记为已确认。 在 ECP 可以标记为探讨在 ECP 的使用、 已处理，或任何其他条件。

-   调用[ **FltIsEcpAcknowledged** ](https://msdn.microsoft.com/library/windows/hardware/ff543321)或[ **FsRtlIsEcpAcknowledged** ](https://msdn.microsoft.com/library/windows/hardware/ff546808)例程，以确定是否为 ECP 上下文结构标记为已确认。

### <a name="span-iddeterminingoriginationmodespanspan-iddeterminingoriginationmodespanspan-iddeterminingoriginationmodespandetermining-origination-mode"></a><span id="Determining_Origination_Mode"></span><span id="determining_origination_mode"></span><span id="DETERMINING_ORIGINATION_MODE"></span>确定资助创始费模式

在文件系统筛选器驱动程序可以调用[ **FltIsEcpFromUserMode** ](https://msdn.microsoft.com/library/windows/hardware/ff543325)或[ **FsRtlIsEcpFromUserMode** ](https://msdn.microsoft.com/library/windows/hardware/ff546813)例程，以确定是否从用户模式下，源自 ECP 上下文结构。 文件系统筛选器驱动程序可以拒绝接受源自用户模式下的 ECP 上下文结构。

### <a name="span-idusinglookasideliststoallocateecpsspanspan-idusinglookasideliststoallocateecpsspanspan-idusinglookasideliststoallocateecpsspanusing-lookaside-lists-to-allocate-ecps"></a><span id="Using_Lookaside_Lists_to_Allocate_ECPs"></span><span id="using_lookaside_lists_to_allocate_ecps"></span><span id="USING_LOOKASIDE_LISTS_TO_ALLOCATE_ECPS"></span>要分配 ECPs 使用后备链列表

在文件系统筛选器驱动程序可以调用以下例程来分配 ECPs 从后备链列表以及管理旁视列表和 ECPs:

-   调用[ **FltInitExtraCreateParameterLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff543261)或[ **FsRtlInitExtraCreateParameterLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff546102)到例程初始化用于固定大小的一个或多个 ECP 上下文结构分配的分页或非分页池后备链列表。

-   调用[ **FltDeleteExtraCreateParameterLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff541973)或[ **FsRtlDeleteExtraCreateParameterLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545849)到例程释放后备链列表。

-   调用[ **FltAllocateExtraCreateParameterFromLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff541734)或[ **FsRtlAllocateExtraCreateParameterFromLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545616)例程内存池分配从后备链列表中为 ECP 上下文结构并生成指向该结构的指针。

-   调用[ **FltFreeExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff542957)或[ **FsRtlFreeExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545989)例程来释放 ECP 上下文的内存结构。

 

 




