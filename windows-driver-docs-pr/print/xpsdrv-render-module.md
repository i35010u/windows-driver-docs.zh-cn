---
title: XPSDrv 渲染器模块
description: XPSDrv 渲染器模块
keywords:
- XPSDrv 打印机驱动程序 WDK，呈现模块
- 渲染模块 WDK XPSDrv，关于渲染模块
- 筛选管道 WDK XPSDrv
- 筛选器管道管理器 WDK XPSDrv
- PHP-FPM WDK XPSDrv
- Inter-Filter Communicator WDK XPSDrv
- IFC WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4846977f5b926eb3a21ffc7ef2ea5835236aefbd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785689"
---
# <a name="xpsdrv-render-module"></a>XPSDrv 渲染器模块


XPSDrv 打印机驱动程序的渲染模块包含用于呈现 XPS 假脱机文件内容的筛选器，用于输出到打印机。 驱动程序的一组呈现筛选器将实例化并在筛选器管道中运行。 筛选器管道管理器 (PHP-FPM) 管理筛选器，Inter-Filter Communicator (IFC) 控制筛选器之间的交互。

下图显示了一个筛选器管道。

![阐释筛选器管道的关系图](images/xps-pipeline.png)

Microsoft 提供以下 XPS 驱动程序组件：

-   筛选器管道管理器

-   Inter-Filter Communicator

-   属性包

筛选器管道管理器必须：

1.  加载和初始化筛选器。

2.  管理筛选器之间的数据。

3.  打印作业完成后，请卸载筛选器。

Inter-Filter Tls 管理筛选器之间的数据传输，筛选器管道管理器管理 Inter-Filter Tls。

下面的过程说明管道中的一组筛选器会发生什么情况：

1.  筛选器管道管理器 (FPC) 文件读取筛选器管道配置。

2.  加载 FPC 指定的筛选器。

3.  筛选器管道已初始化，筛选器管道管理器启动筛选器管道。

4.  管道中的第一个筛选器通过筛选器管道管理器提供的 XPS 或流接口读取 XPS 数据，然后筛选器将处理内容。

5.  第一个筛选器使用 Inter-Filter Communicator 提供的接口将已处理的 XPS 数据发送到第二个筛选器。

6.  Inter-Filter Communicator 维护中间处理结果，直到第二个筛选器准备就绪。

7.  步骤1-6 将从筛选器重复到筛选器，直到最后一个筛选器的结果发送到驱动程序为输出定义的端口。

如果打印机使用 XPS 作为页面描述语言 (PDL) ，而不需要进行其他处理，则可以使用空 ( "传递" ) 管道。 如果 XPS 不是打印机的 PDL，则需要编写一个将 XPS 转换为打印机的 PDL 以及所需的任何其他处理的筛选器。

若要开发 XPS 驱动程序，必须创建以下组件：

-   [XPS 筛选器](xps-filters.md)

-   [XPS 筛选器管道配置文件](filter-pipeline-configuration-file.md)

你还可以将 [打印票证支持添加到 XPSDrv 呈现模块](print-ticket-support-in-the-xpsdrv-render-module.md)

 

 




