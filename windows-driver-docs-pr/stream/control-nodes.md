---
title: 控制节点
description: 控制节点
keywords:
- 广播接收器拓扑 WDK BDA
- 接收方拓扑 WDK BDA
- 广播驱动程序体系结构 WDK AVStream，广播接收器拓扑
- BDA WDK AVStream，接收方拓扑
- 控制节点 WDK BDA
- 节点 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea6e170263b262624f3c42e85b65bdee5469a0b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811407"
---
# <a name="control-nodes"></a>控制节点





下图显示了一个可接收数字广播内容的功能拓扑的示例。 它说明了需要执行的操作：

-   优化并 demodulate 信号。

-   捕获并 demultiplex 信号。

-   获取电子收视指南 (EPG) 信息。

-   获取音频和视频内容。

-   获取 IP 数据。

![阐释接收方拓扑的关系图](images/rcvrtopl.png)

请注意，接收内容的接收方拓扑中的某些函数（如调谐器）始终与硬件相关联。 其他功能（如 content stream demultiplexing）可通过硬件或软件组件执行。 其他人（例如传输信息筛选器 (.TIF) 和网络提供程序筛选器）始终是软件组件。

上图中的块对应于 BDA 控制节点。 每个控制节点使用标准算法将网络和特定于程序的参数数据与输入信号或信号组件组合在一起。 结果会生成新的信号组件，此信号组件对直接连接到下游的控制节点非常有用。

 

 




