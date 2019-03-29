---
title: 使用双设备堆栈的操作流
description: 使用双设备堆栈的操作流
ms.assetid: a717b9c0-b24a-4347-8b0a-254a17238b5f
keywords:
- 操作流 WDK UMDF
- I/O 请求 WDK UMDF，操作流
- 请求处理 WDK UMDF，操作流
- 双精度设备堆栈流 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ef4cb237dbc35d99d7111c8b7ba40f9f66eeda7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564922"
---
# <a name="operation-flow-with-double-device-stack"></a>使用双设备堆栈的操作流


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下图显示了发生在 UMDF 筛选器和 double 设备堆栈中的功能驱动程序的操作的流。

![umdf i/o 调用序列 umdf 筛选器驱动程序和 umdf 函数驱动程序](images/umdfflow2.gif)

**请注意**  启动的应用程序的所有 I/O 都经过内核模式下，图形中所示[UMDF 的体系结构](https://msdn.microsoft.com/library/windows/hardware/ff554461)部分，即使前面的图不显示这种情况下也是如此.

 

UMDF 筛选器和函数驱动程序还可能会调用[ **IWDFIoRequest::GetCreateParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559088)如果它们需要与读取请求相关联的文件信息的方法。 UMDF 筛选器和函数驱动程序还可能会调用[ **IWDFIoRequest::GetReadParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559113)方法如果他们需要读取请求有关的详细信息。

UMDF 功能驱动程序调用[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)或[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)方法向发出信号，筛选器驱动程序，它通过读取操作。 UMDF 筛选器驱动程序还可能调用的方法[IWDFIoRequestCompletionParams](https://msdn.microsoft.com/library/windows/hardware/ff559055)接口是否需要完成读取的请求的详细信息。 UMDF 筛选驱动程序调用**完成**或**CompleteWithInformation**到读取的操作已完成的信号; 应用程序可以将读取数据的访问。

 

 





