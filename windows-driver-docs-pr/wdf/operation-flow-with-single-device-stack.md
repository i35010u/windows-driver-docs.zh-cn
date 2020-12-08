---
title: 使用单设备堆栈的操作流
description: 使用单设备堆栈的操作流
keywords:
- 单个设备 stack 流 WDK UMDF
- 操作流 WDK UMDF
- I/o 请求 WDK UMDF，操作流
- 请求处理 WDK UMDF，操作流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65d7b66cb4137df454b28bc3718e7b388881f417
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795799"
---
# <a name="operation-flow-with-single-device-stack"></a>使用单设备堆栈的操作流


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

下图显示了在单个设备堆栈中与 UMDF 功能驱动程序之间发生的操作流。

![create file 后跟读取请求的 umdf 调用序列](images/umdfflow.gif)

**注意**   应用程序启动的所有 i/o 都是通过内核模式路由的，如 UMDF 部分的 [体系结构](/previous-versions/ff554461(v=vs.85)) 中所示，即使上图中没有显示这种情况。

 

仅当 UMDF 驱动程序需要与读取请求关联的文件的相关信息时，才会调用 [**IWDFIoRequest：： GetCreateParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters) 方法。 仅当 UMDF 驱动程序需要有关读取请求的详细信息时，才会调用 [**IWDFIoRequest：： GetReadParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters) 方法。

如果在读取操作中不需要指定传输的字节数，则 UMDF 驱动程序可以调用 [**IWDFIoRequest：： Complete**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete) 方法，而不是 [**IWDFIoRequest：： CompleteWithInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation) 方法。 UMDF 驱动程序将调用 **complete** 或 **CompleteWithInformation** 以指示读取操作完成;然后，应用程序可以访问读取数据。

 

