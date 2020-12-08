---
title: 编写打印监视器
description: 编写打印监视器
keywords:
- 打印后台处理程序自定义 WDK，打印监视器
- 后台处理程序自定义 WDK 打印、打印监视器
- 自定义打印后台处理程序组件 WDK，打印监视器
- 打印监视器 WDK
- 编写打印监视器
- 监视 WDK 打印
- 打印监视器 WDK，关于打印监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f0a1e79ae03c864ecb46e999a4a050187faf9b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785783"
---
# <a name="writing-a-print-monitor"></a>编写打印监视器





打印监视器负责将打印数据流从打印后台处理程序定向到适当的端口驱动程序。 定义了两种类型的打印监视器：- [语言监视器](language-monitors.md) 和 [端口监视器](port-monitors.md)。 本节介绍这两种监视器类型，并提供设计和实施准则。

提供了以下主题：

[语言监视器](language-monitors.md)

[端口监视器](port-monitors.md)

[语言监视器与端口监视器的交互](language-and-port-monitor-interaction.md)

[打印监视器定义的函数](functions-defined-by-print-monitors.md)

[初始化打印监视器](initializing-a-print-monitor.md)

[打开和关闭端口](opening-and-closing-a-port.md)

[打印打印作业](printing-a-print-job.md)

[管理端口](managing-a-port.md)

[TCPMON Xcv 接口](tcpmon-xcv-interface.md)

[WSDMON 端口监视器](wsdmon-port-monitor.md)

[转换打印监视器以便与群集打印服务器配合使用](converting-print-monitors-for-use-with-clustered-print-servers.md)

[安装打印监视器](installing-a-print-monitor.md)

 

 




