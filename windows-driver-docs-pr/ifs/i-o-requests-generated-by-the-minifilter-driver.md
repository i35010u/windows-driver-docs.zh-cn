---
title: 由微筛选器驱动程序生成的 I/O 请求
description: 由微筛选器驱动程序生成的 I/O 请求
ms.assetid: cf06dcb9-58e2-4341-8229-8f172f37c176
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，由驱动程序生成的 i/o 请求
- I/o 请求 WDK 文件系统
- Irp WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2919e578e336e6ba01ab36e2d032c7c6d0e55444
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065946"
---
# <a name="io-requests-generated-by-the-minifilter-driver"></a>由微筛选器驱动程序生成的 I/O 请求


微筛选器驱动程序可以根据当前卷或其他卷上的一个微筛选器驱动程序的实例生成和发送基于 IRP 的 i/o 请求。 仅在指定实例下附加的微筛选器驱动程序实例和旧筛选器驱动程序以及文件系统会看到生成的 i/o。 这解决了旧版筛选器驱动程序模型中与递归 i/o 相关的许多问题，在这种情况下，旧筛选器驱动程序生成的 i/o 请求必须从最顶层的驱动程序开始，遍历整个文件系统堆栈。

在完成所有未完成的 i/o 操作之前，筛选器管理器不会卸载微筛选器驱动程序。

### <a name="span-idfilter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driverspanspan-idfilter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driverspanspan-idfilter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driverspanfilter-manager-routines-for-io-requests-generated-by-the-minifilter-driver"></a><span id="Filter_Manager_Routines_for_I_O_Requests_Generated_by_the_Minifilter_Driver"></span><span id="filter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driver"></span><span id="FILTER_MANAGER_ROUTINES_FOR_I_O_REQUESTS_GENERATED_BY_THE_MINIFILTER_DRIVER"></span>微筛选器驱动程序生成的 i/o 请求的筛选器管理器例程

筛选器管理器提供以下用于创建、打开、读取和写入文件的支持例程：

[**FltClose**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclose)

[**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[**FltCreateFileEx**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefileex)

[**FltReadFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreadfile)

[**FltWriteFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltwritefile)

提供以下支持例程用于设置和删除重新分析点：

[**FltTagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

提供以下支持例程用于生成 i/o 请求：

[*FltAllocateCallbackData*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecallbackdata)

[**FltFreeCallbackData**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreecallbackdata)

[**FltPerformAsynchronousIo**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltperformasynchronousio)

[*FltPerformSynchronousIo*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltperformsynchronousio)

[**FltReuseCallbackData**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreusecallbackdata)

提供以下支持例程用于取消文件打开请求和重新发出 i/o 请求：

[**FltCancelFileOpen**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreissuesynchronousio)

筛选器管理器还提供以下常规用途例程：

[**FltDeviceIoControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeviceiocontrolfile)

[**FltFlushBuffers**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltflushbuffers)

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FltQueryInformationFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**FltQuerySecurityObject**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltquerysecurityobject)

[**FltQueryVolumeInformationFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryvolumeinformationfile)

[**FltSetInformationFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinformationfile)

[**FltSetSecurityObject**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetsecurityobject)

 

