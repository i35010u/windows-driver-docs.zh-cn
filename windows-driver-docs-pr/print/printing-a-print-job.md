---
title: 打印打印作业
description: 打印打印作业
ms.assetid: 2e881f99-9dbe-4e89-8628-feb05137c9b0
keywords:
- 打印监视器 WDK，打印打印作业
- WDK 的打印作业打印
- 打印作业 WDK 打印
- WritePort
- ReadPort
- GetPrinterDataFromPort
- 双向通信 WDK 打印
- 双向通信 WDK 打印
- 打印打印作业 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef56613fab90d24c0806bd9a5b23b700f5ab6acd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356027"
---
# <a name="printing-a-print-job"></a>打印打印作业





后一个端口已打开，如中所述[打开和关闭端口](opening-and-closing-a-port.md)，后台处理程序可以将打印作业发送到端口。

通过语言或端口监视器的后台处理程序调用分隔每个打印作业[ **StartDocPort** ](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85))并[ **EndDocPort** ](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85))函数。 打印处理器调用的后台处理程序时，后台处理程序调用这些函数**StartDocPrinter**并**EndDocPrinter**函数，Microsoft Windows SDK 文档中所述。 一组范围内**StartDocPort**并**EndDocPort**函数，对监视器的不受限制后台处理程序调用[ **WritePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-writeport)，[ **ReadPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-readport)，并[ **GetPrinterDataFromPort** ](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85))函数可能发生。

每个函数要求返回的端口句柄[ **OpenPortEx** ](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85)) (或[ **OpenPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-openport)) 如下所示输入参数指定。 通常情况下，语言监视器实现每个函数的调用中其关联的端口监视器的名称类似的函数。

当后台处理程序调用的语言监视器**WritePort**函数将数据流发送到端口，该函数通常添加特定于语言的信息，如*PJL*命令，将收到的数据然后再将它传递到关联的端口监视器的流**WritePort**函数。

**ReadPort**函数用于获取状态信息从语言监视器可能会通过调用发送到后台处理程序的双向打印机硬件**SetPort**Windows 中所述SDK 文档。 后台处理程序不会调用**ReadPort**函数。

如果打印硬件是双向的应支持其语言监视器和其端口监视器**GetPrinterDataFromPort**函数。 语言监视器**GetPrinterDataFromPort**函数应接受注册表值名称作为输入，获取该名称的值 (通常通过调用相关联的端口监视器**WritePort**并**ReadPort**函数)，并将值返回给调用方。 端口监视器**GetPrinterDataFromPort**函数应接受作为输入，调用到 I/O 的控制代码[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) （Windows SDK 文档中所述）若要将控制代码传递给端口驱动程序，并返回结果。

 

 




