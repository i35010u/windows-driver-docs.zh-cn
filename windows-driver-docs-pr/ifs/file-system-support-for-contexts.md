---
title: 用于上下文的文件系统支持
description: 用于上下文的文件系统支持
ms.assetid: 661ee3ff-3171-4d1e-a8fe-8d1852c5e990
keywords:
- 上下文 WDK 文件系统微筛选器的文件系统支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b4b007414586d130a5df91204fbf19dce08fc1f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369254"
---
# <a name="file-system-support-for-contexts"></a>用于上下文的文件系统支持

若要支持文件上下文 （如果适用）、 流式处理上下文，并且文件对象 （流句柄） 上下文、 文件系统必须使用[ **FSRTL\_高级\_FCB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)结构。 所有 Microsoft Windows 文件系统都使用此结构，并且所有第三方文件系统开发人员是强烈建议执行此操作。 有关详细信息，请参阅[ **FsRtlSetupAdvancedHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff547257)并**FSRTL\_高级\_FCB\_标头**。

NTFS 和 FAT 文件系统不支持文件、 流或文件对象上下文上分页文件，以 pre-create 或后关闭路径，或出于[ **IRP\_MJ\_网络\_查询\_打开**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-network-query-open)操作。

微筛选器驱动程序可以确定是否文件系统支持流的上下文和文件对象上下文为某个给定的文件的对象通过调用[ **FltSupportsStreamContexts** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)和[ **FltSupportsStreamHandleContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)分别。

文件上下文是适用于 Windows Vista 及更高版本。

对于支持的单个数据流将每个文件的文件系统 （如 FAT)，文件上下文是等效于流上下文。 通常，此类文件系统支持流上下文，但不是支持文件上下文。 相反，筛选器管理器提供此支持，使用文件系统的现有支持的流上下文。 附加到这些文件系统微筛选器驱动程序实例[ **FltSupportsFileContexts** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsfilecontexts)返回**FALSE**，而[ **FltSupportsFileContextsEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsfilecontextsex)返回**TRUE** (时有效非**NULL**为传递值*实例*参数）。

如果文件不支持上下文类型，则微筛选器不能将该类型的上下文附加到该文件。

若要支持文件上下文，文件系统必须：

* 嵌入**FileContextSupportPointer**类型 PVOID 其文件上下文结构通常文件上下文块 (FCB) 中的成员。 文件系统必须初始化为此成员**NULL**。

* 使用**FsRtlSetupAdvancedHeaderEx** (而不是[ **FsRtlSetupAdvancedHeader**](https://msdn.microsoft.com/library/windows/hardware/ff547257)) 初始化其流上下文结构，将有效指针传递给**FileContextSupportPointer**的成员 （嵌入在相应的文件上下文结构） *FileContextSupportPointer*参数。 有关详细信息，请参阅**FsRtlSetupAdvancedHeaderEx**并[ **FSRTL\_高级\_FCB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)。

* 调用**FsRtlTeardownPerFileContexts**来释放所有筛选器和微筛选器驱动程序已关联到一个文件时文件系统中删除它的文件的文件上下文结构的文件上下文结构。