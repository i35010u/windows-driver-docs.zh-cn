---
title: 处理打印作业
description: 处理打印作业
keywords:
- 打印处理器 WDK，打印作业处理
- 打印作业 WDK，处理
- 发送打印作业
- 作业 WDK 打印，处理
- EMF 记录播放 WDK 打印处理器
- N 个打印 WDK
- PrintDocumentOnPrintProcessor
- 输出格式 WDK 打印处理器
- 输入格式 WDK 打印处理器
- 作业 WDK 打印
- 打印作业 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2819d1a8d46504af605f4d5f3ba26b210039ad34
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807203"
---
# <a name="processing-a-print-job"></a>处理打印作业





当后台处理程序准备好将打印作业发送到打印处理器时，它将调用打印处理器的 [**OpenPrintProcessor**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openprintprocessor) 函数。 此函数执行初始化活动并返回一个句柄。

然后，后台处理程序可以调用 [**PrintDocumentOnPrintProcessor**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor)，这是打印处理器函数，它将数据流从输入格式转换为输出格式，并将转换后的流返回到后台处理程序。

如果输入格式是基于 NT 的操作系统 EMF， **PrintDocumentOnPrintProcessor** 函数可以使用在 [打印处理器中使用 GDI 函数](using-gdi-functions-in-print-processors.md)中列出的函数来控制 EMF 记录的播放。 这些函数在打印处理器和打印机驱动程序之间提供了一个接口。 此接口允许打印处理器控制打印机页面的物理布局，从而有助于实现这样的功能：打印每个物理页面的多个文档页面 ( "N 向上" 打印) ，按逆序打印页面，打印每个页面的多个副本。

打印处理器的输出数据流必须返回到后台处理程序。 通常情况下，如果数据转换需要与打印机驱动程序的 [打印机图形 DLL](printer-graphics-dll.md) 交互 (与 EMF 输入数据) 的情况相同，则图形 DLL 会通过调用 [**EngWritePrinter**](/windows/win32/api/winddi/nf-winddi-engwriteprinter)将流返回到后台处理程序。 另一方面，如果转换未调用打印机图形 DLL (与) 原始输入数据的情况相同，则打印处理器会调用 Microsoft Windows SDK 文档) 中所述的 **WritePrinter** (。

可以通过从后台处理程序到打印处理器的 [**ControlPrintProcessor**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-controlprintprocessor)函数的异步调用中断 **PrintDocumentOnPrintProcessor** 函数。 此函数可实现应用程序暂停、恢复或取消打印作业的功能。

在 **PrintDocumentOnPrintProcessor** 完成转换数据流并返回后，后台处理程序将调用打印处理器的 [**ClosePrintProcessor**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeprintprocessor) 函数。

 

