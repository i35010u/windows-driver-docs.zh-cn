---
title: 语言监视器与端口监视器的交互
description: 语言监视器与端口监视器的交互
keywords:
- 打印监视器 WDK，语言监视器
- 打印监视器 WDK，端口监视器
- 语言监视器 WDK 打印，端口监视器交互
- 端口监视 WDK 打印，语言监视器交互
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25274cf7f31616ee1066f9f4120d6aedb5f99362
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796497"
---
# <a name="language-and-port-monitor-interaction"></a>语言监视器与端口监视器的交互





下图演示了从打印处理器到打印机的打印机数据所采用的路径，其中) 具有与其关联的语言监视器;和 b) 没有与之关联的语言监视器。

![使用语言监视器和不使用语言监视器比较打印机数据路径的图](images/mon1.png)

如果在安装打印机的过程中，语言监视器与打印机相关联，则语言监视器将从后台处理程序的打印处理器接收打印机的数据流。 语言监视器修改数据流，并将其传递到打印机的端口监视器。

[打印监视器定义](functions-defined-by-print-monitors.md)的大部分功能对于[语言监视器](language-monitors.md)和[端口监视器](port-monitors.md)都是相同的。 通常情况下，如果语言监视器位于数据流路径中，则后台处理程序会调用函数的语言监视器实现，而语言监视器则调用该端口监视器对同一功能的实现。 例如，PJL 语言监视器中的 [**WritePort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport) 函数 ( # A0) 将 *PJL* 的命令添加到数据流，然后调用端口监视器的 **WritePort** 将流发送到端口驱动程序。

如果未安装语言监视器，则后台处理程序将调用该函数的端口监视器实现。

由于语言监视器和端口监视器是打印体系结构的独立组件，因此可将自定义和 Microsoft 提供的监视器一起使用。 因此，你可以提供与 Microsoft 提供的端口监视器一起工作的自定义语言监视器，反之亦然。

还可以提供由 [组合语言和端口监视器](combined-language-and-port-monitor.md)组成的单个打印监视器。

 

