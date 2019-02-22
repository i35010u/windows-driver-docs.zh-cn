---
title: 生成由微筛选器驱动程序的 I/O 请求
description: 生成由微筛选器驱动程序的 I/O 请求
ms.assetid: cf06dcb9-58e2-4341-8229-8f172f37c176
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，生成的驱动程序的 I/O 请求
- I/O 请求 WDK 文件系统
- Irp WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cee420f417f842a34155f79361d96329b68c03a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519581"
---
# <a name="io-requests-generated-by-the-minifilter-driver"></a>生成由微筛选器驱动程序的 I/O 请求


微筛选器驱动程序可以生成并发送基于 IRP 的 I/O 请求，从一个微筛选器驱动程序自己的实例或另一个卷上的当前卷。 仅通过微筛选器驱动程序实例和旧的筛选器驱动程序附加在下方指定的实例，以及文件系统，则出现生成的 I/O。 这解决了与旧的筛选器驱动程序模型中的 I/O 请求生成的旧的筛选器驱动程序必须经过从最顶层的驱动程序开始在整个文件系统堆栈中的递归 I/O 相关的许多问题。

筛选器管理器不会卸载微筛选器驱动程序，直到完成所有未完成的 I/O 操作。

### <a name="span-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanspan-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanspan-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanfilter-manager-routines-for-io-requests-generated-by-the-minifilter-driver"></a><span id="Filter_Manager_Routines_for_I_O_Requests_Generated_by_the_Minifilter_Driver"></span><span id="filter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driver"></span><span id="FILTER_MANAGER_ROUTINES_FOR_I_O_REQUESTS_GENERATED_BY_THE_MINIFILTER_DRIVER"></span>用于生成由微筛选器驱动程序的 I/O 请求的筛选器管理器例程

筛选器管理器用于创建、 打开、 读取和写入文件提供以下支持例程：

[**FltClose**](https://msdn.microsoft.com/library/windows/hardware/ff541863)

[**FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)

[**FltCreateFileEx**](https://msdn.microsoft.com/library/windows/hardware/ff541937)

[**FltReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff544286)

[**FltWriteFile**](https://msdn.microsoft.com/library/windows/hardware/ff544610)

用于设置和删除重新分析点提供了以下支持例程：

[**FltTagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544589)

[**FltUntagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544608)

用于生成输入/输出请求提供了以下支持例程：

[*FltAllocateCallbackData*](https://msdn.microsoft.com/library/windows/hardware/ff541703)

[**FltFreeCallbackData**](https://msdn.microsoft.com/library/windows/hardware/ff542949)

[**FltPerformAsynchronousIo**](https://msdn.microsoft.com/library/windows/hardware/ff543420)

[*FltPerformSynchronousIo*](https://msdn.microsoft.com/library/windows/hardware/ff543421)

[**FltReuseCallbackData**](https://msdn.microsoft.com/library/windows/hardware/ff544358)

用于取消文件打开请求和重新签发的 I/O 请求提供了以下支持例程：

[**FltCancelFileOpen**](https://msdn.microsoft.com/library/windows/hardware/ff541784)

[**FltReissueSynchronousIo**](https://msdn.microsoft.com/library/windows/hardware/ff544311)

筛选器管理器还提供了以下常规用途例程：

[**FltDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542046)

[**FltFlushBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff542099)

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**FltQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff543439)

[**FltQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff543441)

[**FltQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff543446)

[**FltSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff544516)

[**FltSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff544538)

 

 




