---
title: 使用单设备堆栈的操作流
description: 使用单设备堆栈的操作流
ms.assetid: b7e38844-2e00-48b8-9741-3bfc38869a6d
keywords:
- 单个设备 stack 流 WDK UMDF
- 操作流 WDK UMDF
- I/o 请求 WDK UMDF，操作流
- 请求处理 WDK UMDF，操作流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 844dc17ef34f793661ab809f5c00ef78b544cc61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827259"
---
# <a name="operation-flow-with-single-device-stack"></a>使用单设备堆栈的操作流


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下图显示了在单个设备堆栈中与 UMDF 功能驱动程序之间发生的操作流。

![create file 后跟读取请求的 umdf 调用序列](images/umdfflow.gif)

  **请注意**，应用程序启动的所有 i/o 都将通过内核模式路由，如 UMDF 部分的[体系结构](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))中所示，即使上图中没有显示这种情况，也是如此。

 

仅当 UMDF 驱动程序需要与读取请求关联的文件的相关信息时，才会调用[**IWDFIoRequest：： GetCreateParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)方法。 仅当 UMDF 驱动程序需要有关读取请求的详细信息时，才会调用[**IWDFIoRequest：： GetReadParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)方法。

如果在读取操作中不需要指定传输的字节数，则 UMDF 驱动程序可以调用[**IWDFIoRequest：： Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)方法，而不是[**IWDFIoRequest：： CompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)方法。 UMDF 驱动程序将调用**complete**或**CompleteWithInformation**以指示读取操作完成;然后，应用程序可以访问读取数据。

 

 





