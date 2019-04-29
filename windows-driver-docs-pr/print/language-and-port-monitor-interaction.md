---
title: 语言监视器与端口监视器的交互
description: 语言监视器与端口监视器的交互
ms.assetid: 6c3c55fc-40f3-43d7-b8a2-20fed8d28813
keywords:
- 打印监视器 WDK，语言监视器
- 打印监视器 WDK，端口监视器
- 语言监视 WDK 打印，端口监视器交互
- 端口监视 WDK 打印，语言监视器交互
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a37d379ac0f27b470248f56ba3130cec8109f322
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388107"
---
# <a name="language-and-port-monitor-interaction"></a>语言监视器与端口监视器的交互





下图演示了打印处理器到打印机的打印机数据所采用的路径的) 具有与之; 关联的语言监视器和 b） 不具有与之关联的语言监视器。

![将打印机数据路径使用的语言监视器和语言监视器不进行比较的图形](images/mon1.png)

如果在打印机的安装过程与打印机相关联的语言监视器，语言监视器从后台处理程序的打印处理器接收打印机的数据流。 语言监视器修改数据流，并将其传递给打印机的端口监视器。

大部分打印监视器所定义的函数到数据流的命令，然后调用端口监视器**WritePort**将流发送到端口驱动程序。

如果未安装的语言监视器，后台处理程序调用的函数的端口监视器的实现。

由于语言监视器和端口监视器是离散的打印体系结构、 自定义组件并且可以一起使用 Microsoft 提供的监视器。 因此，您可以提供自定义的语言监视器结合使用该工作原理与 Microsoft 提供的端口监视器，反之亦然。

您还可以提供单个打印监控器组成[组合的语言和端口监视器](combined-language-and-port-monitor.md)。

 

 




