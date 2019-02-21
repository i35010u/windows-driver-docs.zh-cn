---
title: 处理打印作业
description: 处理打印作业
ms.assetid: c5e291d9-069c-4877-a167-862ba5794368
keywords:
- 打印处理器 WDK、 打印作业处理
- WDK 的打印作业、 处理
- 发送打印作业
- WDK 打印作业处理
- EMF 记录播放 WDK 打印处理器
- 每张多打印 WDK
- PrintDocumentOnPrintProcessor
- 输出格式 WDK 打印处理器
- 输入的格式 WDK 打印处理器
- 打印作业 WDK
- WDK 的打印作业
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4df65f64a29c56412b4a6478fb7840892b1e0aa4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521271"
---
# <a name="processing-a-print-job"></a>处理打印作业





当后台处理程序已准备好将打印作业发送到打印处理器时，它将调用打印处理器[ **OpenPrintProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff559604)函数。 此函数执行初始化活动，并返回一个句柄。

然后，后台处理程序可以调用[ **PrintDocumentOnPrintProcessor**](https://msdn.microsoft.com/library/windows/hardware/ff560724)，这是将数据流从输入格式转换为输出格式，并返回转换后的打印处理器函数流式传输到后台处理程序。

如果输入的格式为 NT 基于操作系统系统 EMF， **PrintDocumentOnPrintProcessor**函数可以通过使用中列出的函数来控制播放的 EMF 记录[打印处理器中使用 GDI 函数](using-gdi-functions-in-print-processors.md). 这些函数提供的打印处理器和打印机驱动程序之间的接口。 此接口允许打印处理器来控制打印机页的物理布局，因此有利于实现打印每个物理页面 （"每张"打印） 的多个文档页面等功能、 按相反的顺序，打印页面和打印每个页面的多个副本。

打印处理器的输出数据流必须返回到后台处理程序。 通常情况下，如果数据转换要求与打印机驱动程序的交互[打印机图形 DLL](printer-graphics-dll.md) （按原样 EMF 输入数据的大小写），图形 DLL 将流返回后台处理程序通过调用[ **EngWritePrinter**](https://msdn.microsoft.com/library/windows/hardware/ff565467)。 另一方面，如果转换不会调用打印机图形 DLL （如与原始输入数据的情况相符），然后打印处理器调用**WritePrinter** （Microsoft Windows SDK 文档中所述）。

**PrintDocumentOnPrintProcessor**函数可以通过异步调用从后台处理程序的打印处理器中断[ **ControlPrintProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff546352)函数。 此函数实现来暂停、 继续或取消打印作业的应用程序的功能。

之后**PrintDocumentOnPrintProcessor**转换的数据流并返回完成之后，后台处理程序调用打印处理器[ **ClosePrintProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff545976)函数。

 

 




