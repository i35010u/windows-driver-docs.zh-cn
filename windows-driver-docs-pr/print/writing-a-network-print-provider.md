---
title: 编写网络打印提供程序
description: 编写网络打印提供程序
keywords:
- 打印后台处理程序自定义 WDK，打印提供程序
- 后台处理程序自定义 WDK 打印、打印提供程序
- 自定义打印后台处理程序组件 WDK，打印提供程序
- 打印提供商 WDK，编写
- 网络打印提供程序 WDK
- 编写打印提供程序
- 打印提供程序 WDK，关于网络打印提供程序
- 网络打印提供程序 WDK，关于网络打印提供程序
- 提供程序 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc860736feedac5445e1a208821dc7c093be91be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785785"
---
# <a name="writing-a-network-print-provider"></a>编写网络打印提供程序





有时，供应商可能希望提供 [打印提供程序](print-providers.md) 来支持新的网络体系结构。 提供新的打印提供程序功能的一种可行方法是创建一个替换 [本地打印提供](local-print-provider.md)程序的全新打印提供程序。 但事实上，这是一个非常困难且可能不必要的任务。 一种替代方法是创建与本地打印提供程序一起工作的部分打印提供程序。

本部分提供下列主题：

[不完整打印提供程序的概述](overview-of-partial-print-providers.md)

[支持打印机更改通知](supporting-printer-change-notifications.md)

[安装网络打印提供程序](installing-a-network-print-provider.md)

 

 




