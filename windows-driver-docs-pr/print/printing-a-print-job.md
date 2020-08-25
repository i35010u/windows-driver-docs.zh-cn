---
title: 打印打印作业
description: 打印打印作业
ms.assetid: 2e881f99-9dbe-4e89-8628-feb05137c9b0
keywords:
- 打印监视器 WDK，打印打印作业
- 打印作业 WDK，打印
- 作业 WDK 打印，打印
- WritePort
- ReadPort
- GetPrinterDataFromPort
- 双向通信 WDK 打印
- 双向通信 WDK 打印
- 打印打印作业 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 861089542061d63afc1fc085c23092824fa82559
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802408"
---
# <a name="printing-a-print-job"></a>打印打印作业





打开端口后，如 [打开和关闭端口](opening-and-closing-a-port.md)中所述，后台处理程序可以将打印作业发送到端口。

每个打印作业由后台处理程序对语言或端口监视器的 [**StartDocPort**](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85)) 和 [**EndDocPort**](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85)) 函数的调用分隔。 当打印处理器调用后台处理程序的 **StartDocPrinter** 和 **EndDocPrinter** 函数时，后台处理程序将调用这些函数，如 Microsoft Windows SDK 文档中所述。 在一组 **StartDocPort** 和 **EndDocPort** 函数的作用域内，可能会对监视器的 [**WritePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)、 [**ReadPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)和 [**GetPrinterDataFromPort**](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85)) 函数进行无限制的后台处理程序调用。

其中每个函数都需要在输入参数中指定 [**OpenPortEx**](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85)) (或 [**OpenPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport)) 返回的端口句柄。 通常，语言监视器通过在其关联的端口监视器中调用命名函数，来实现每个函数。

当后台处理程序调用语言监视器的 **WritePort** 函数以将数据流发送到端口时，该函数通常会将特定语言的信息（如 *PJL* 命令）添加到接收的数据流中，然后再将其传递给关联的端口监视器的 **WritePort** 函数。

**ReadPort**函数用于从双向打印机硬件获取状态信息，语言监视器可以通过调用**SetPort**将其发送到后台处理程序，如 Windows SDK 文档中所述。 后台处理程序不会调用 **ReadPort** 函数。

如果打印硬件是双向的，则其语言监视器及其端口监视器都应支持 **GetPrinterDataFromPort** 函数。 语言监视器的 **GetPrinterDataFromPort** 函数应接受注册表值名称作为输入，并 (通常通过调用关联的端口监视器的 **WritePort** 和 **ReadPort** 函数) ，获取该名称的值，并将值返回给调用方。 端口监视器的 **GetPrinterDataFromPort** 函数应接受 i/o 控制代码作为输入，调用 Windows SDK 文档中所述的 [**DeviceIoControl**](https://docs.microsoft.com/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) () ，将控制代码传递到端口驱动程序并返回结果。

 

 




