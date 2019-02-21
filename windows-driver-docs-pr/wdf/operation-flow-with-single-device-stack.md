---
title: 与单个设备堆栈操作流
description: 与单个设备堆栈操作流
ms.assetid: b7e38844-2e00-48b8-9741-3bfc38869a6d
keywords:
- 单个设备堆栈流 WDK UMDF
- 操作流 WDK UMDF
- I/O 请求 WDK UMDF，操作流
- 请求处理 WDK UMDF，操作流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f8a9f7767ab02f08483303512e5443a5cb740f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540491"
---
# <a name="operation-flow-with-single-device-stack"></a>与单个设备堆栈操作流


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下图显示了发生与单个设备堆栈中的 UMDF 功能驱动程序的操作的流。

![创建文件的读取请求后跟 umdf 调用序列](images/umdfflow.gif)

**请注意**  启动的应用程序的所有 I/O 都经过内核模式下，图形中所示[UMDF 的体系结构](https://msdn.microsoft.com/library/windows/hardware/ff554461)部分，即使前面的图不显示这种情况下也是如此.

 

UMDF 驱动程序调用[ **IWDFIoRequest::GetCreateParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559088)方法仅当它需要与读取请求相关联的文件的相关信息。 UMDF 驱动程序调用[ **IWDFIoRequest::GetReadParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559113)方法仅当需要有关读取请求的详细信息。

UMDF 驱动程序可以调用[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)方法而不是[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)如果在读取操作中指定的传输的字节数的方法不是必需的。 UMDF 驱动程序调用**完成**或**CompleteWithInformation**到读取的操作已完成的信号; 应用程序可以将读取数据的访问。

 

 





