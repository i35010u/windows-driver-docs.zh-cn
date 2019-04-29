---
title: XPSDrv 渲染器模块
description: XPSDrv 渲染器模块
ms.assetid: e844e320-bd3d-4855-bb47-fdfbdb157802
keywords:
- XPSDrv 的打印机驱动程序 WDK，呈现模块
- 呈现模块 WDK XPSDrv 有关呈现器模块
- 筛选器管道 WDK XPSDrv
- 筛选器管道管理器 WDK XPSDrv
- FPM WDK XPSDrv
- 间筛选 Communicator WDK XPSDrv
- IFC WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa259f3d7463f3336fb321b2a47b52d4a3bd561
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390232"
---
# <a name="xpsdrv-render-module"></a>XPSDrv 渲染器模块


XPSDrv 打印机驱动程序的呈现器模块包含呈现到打印机的输出 XPS 假脱机文件的内容的筛选器。 呈现筛选器驱动程序集是实例化并在筛选器管道中运行。 筛选器管道管理器 (FPM) 管理这些筛选器，并间的筛选器 Communicator (IFC) 控制筛选器之间的交互。

下图显示了筛选器管道。

![说明筛选器管道的关系图](images/xps-pipeline.png)

Microsoft 提供了以下的 XPS 驱动程序组件：

-   筛选器管道管理器

-   Communicator 间的筛选器

-   属性包

筛选器管道管理器必须：

1.  加载和初始化筛选器。

2.  管理筛选器之间的数据。

3.  打印作业完成后卸载这些筛选器。

间筛选器，并管理筛选器之间传输数据和筛选器管道管理器管理器间的筛选器，并。

以下过程描述了一组筛选器管道中会发生什么情况：

1.  筛选器管道管理器读取筛选器管道配置 (FPC) 文件。

2.  加载 FPC 指定的筛选器。

3.  初始化筛选器管道，并筛选器管道管理器启动筛选器管道。

4.  管道中的第一个筛选器中读取通过 XPS 或流接口的筛选器管道管理器提供，XPS 数据和筛选器然后处理内容。

5.  第一个筛选器使用间的筛选器 Communicator 提供的接口将已处理的 XPS 数据发送到第二个筛选器。

6.  间的筛选器 Communicator 维护中间处理结果直到第二个筛选器准备就绪。

7.  步骤 1-6 被重复筛选器筛选，直到最后一个筛选器的结果发送到端口驱动程序已定义的输出。

如果打印机是使用 XPS 作为页面描述语言 (PDL) 和所需任何其他处理，可以使用空的 （"直通"） 的管道。 如果 XPS 不是您的打印机的 PDL，需要编写所需的筛选器将 XPS 转换为您的打印机，以及任何其他处理 PDL。

若要开发的 XPS 驱动程序，必须创建以下组件：

-   [XPS 筛选器](xps-filters.md)

-   [XPS 筛选管道配置文件](filter-pipeline-configuration-file.md)

您还可以添加[XPSDrv 呈现模块的打印票证支持](print-ticket-support-in-the-xpsdrv-render-module.md)

 

 




