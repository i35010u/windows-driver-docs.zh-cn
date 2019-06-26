---
title: 使用单设备堆栈的操作流
description: 使用单设备堆栈的操作流
ms.assetid: b7e38844-2e00-48b8-9741-3bfc38869a6d
keywords:
- 单个设备堆栈流 WDK UMDF
- 操作流 WDK UMDF
- I/O 请求 WDK UMDF，操作流
- 请求处理 WDK UMDF，操作流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be9e629f9a11b5ac09c684e6810209ac9f518431
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375055"
---
# <a name="operation-flow-with-single-device-stack"></a>使用单设备堆栈的操作流


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下图显示了发生与单个设备堆栈中的 UMDF 功能驱动程序的操作的流。

![创建文件的读取请求后跟 umdf 调用序列](images/umdfflow.gif)

**请注意**  启动的应用程序的所有 I/O 都经过内核模式下，图形中所示[UMDF 的体系结构](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))部分，即使前面的图不显示这种情况下也是如此.

 

UMDF 驱动程序调用[ **IWDFIoRequest::GetCreateParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)方法仅当它需要与读取请求相关联的文件的相关信息。 UMDF 驱动程序调用[ **IWDFIoRequest::GetReadParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)方法仅当需要有关读取请求的详细信息。

UMDF 驱动程序可以调用[ **IWDFIoRequest::Complete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-complete)方法而不是[ **IWDFIoRequest::CompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)如果在读取操作中指定的传输的字节数的方法不是必需的。 UMDF 驱动程序调用**完成**或**CompleteWithInformation**到读取的操作已完成的信号; 应用程序可以将读取数据的访问。

 

 





