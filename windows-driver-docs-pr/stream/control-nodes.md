---
title: 控制节点
description: 控制节点
ms.assetid: e1ab522e-089e-4508-aef4-5b2a65f50bb5
keywords:
- 广播的接收器拓扑 WDK BDA
- 接收方拓扑 WDK BDA
- 广播驱动程序体系结构 WDK AVStream，广播的接收器拓扑
- BDA WDK AVStream，接收方拓扑
- 控制节点 WDK BDA
- 节点 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89b778c8273434b6df90d5dc478c1e6beafde211
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546997"
---
# <a name="control-nodes"></a>控制节点





下图显示了一种可能的功能拓扑接收数字广播的内容的示例。 它说明了所需的操作：

-   优化和解调信号。

-   捕获并逐层信号。

-   获取电子版收视指南 (EPG) 信息。

-   获取音频和视频内容。

-   获取 IP 数据。

![关系图演示如何接收方拓扑](images/rcvrtopl.png)

请注意，接收方拓扑中获取内容，例如该调谐器的一些函数始终与硬件相关联。 其他函数，如多路分解内容流，可以执行与硬件或软件组件。 还有一些业务负责人，例如传输的信息筛选器 (TIF) 和网络提供程序筛选器，始终是软件组件。

在上图块对应于 BDA 控制节点。 每个控制节点与输入的信号或信号组件，使用标准算法结合网络和特定于程序的参数数据。 结果将生成可连接到的控件节点的新信号组件立即下游。

 

 




