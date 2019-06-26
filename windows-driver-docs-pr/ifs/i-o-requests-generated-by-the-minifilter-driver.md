---
title: 由微筛选器驱动程序生成的 I/O 请求
description: 由微筛选器驱动程序生成的 I/O 请求
ms.assetid: cf06dcb9-58e2-4341-8229-8f172f37c176
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，生成的驱动程序的 I/O 请求
- I/O 请求 WDK 文件系统
- Irp WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dde83f45cf2c9ff7ba6bdbe0b5a328383920e9a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375706"
---
# <a name="io-requests-generated-by-the-minifilter-driver"></a>由微筛选器驱动程序生成的 I/O 请求


微筛选器驱动程序可以生成并发送基于 IRP 的 I/O 请求，从一个微筛选器驱动程序自己的实例或另一个卷上的当前卷。 仅通过微筛选器驱动程序实例和旧的筛选器驱动程序附加在下方指定的实例，以及文件系统，则出现生成的 I/O。 这解决了与旧的筛选器驱动程序模型中的 I/O 请求生成的旧的筛选器驱动程序必须经过从最顶层的驱动程序开始在整个文件系统堆栈中的递归 I/O 相关的许多问题。

筛选器管理器不会卸载微筛选器驱动程序，直到完成所有未完成的 I/O 操作。

### <a name="span-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanspan-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanspan-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanfilter-manager-routines-for-io-requests-generated-by-the-minifilter-driver"></a><span id="Filter_Manager_Routines_for_I_O_Requests_Generated_by_the_Minifilter_Driver"></span><span id="filter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driver"></span><span id="FILTER_MANAGER_ROUTINES_FOR_I_O_REQUESTS_GENERATED_BY_THE_MINIFILTER_DRIVER"></span>用于生成由微筛选器驱动程序的 I/O 请求的筛选器管理器例程

筛选器管理器用于创建、 打开、 读取和写入文件提供以下支持例程：

[**FltClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltclose)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)

[**FltCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex)

[**FltReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreadfile)

[**FltWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltwritefile)

用于设置和删除重新分析点提供了以下支持例程：

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuntagfile)

用于生成输入/输出请求提供了以下支持例程：

[*FltAllocateCallbackData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecallbackdata)

[**FltFreeCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreecallbackdata)

[**FltPerformAsynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltperformasynchronousio)

[*FltPerformSynchronousIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltperformsynchronousio)

[**FltReuseCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreusecallbackdata)

用于取消文件打开请求和重新签发的 I/O 请求提供了以下支持例程：

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreissuesynchronousio)

筛选器管理器还提供了以下常规用途例程：

[**FltDeviceIoControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeviceiocontrolfile)

[**FltFlushBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltflushbuffers)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FltQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**FltQuerySecurityObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltquerysecurityobject)

[**FltQueryVolumeInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueryvolumeinformationfile)

[**FltSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetinformationfile)

[**FltSetSecurityObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetsecurityobject)

 

 




