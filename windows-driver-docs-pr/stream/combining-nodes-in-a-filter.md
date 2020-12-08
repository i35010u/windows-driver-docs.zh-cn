---
title: 合并筛选器中的节点
description: 合并筛选器中的节点
keywords:
- 控制节点 WDK BDA
- 节点 WDK BDA
- 合并筛选器中的节点 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cce06121ed76bcaed1fe347bde2110cbeb8c84a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787141"
---
# <a name="combining-nodes-in-a-filter"></a>合并筛选器中的节点





下面的示例 DirectShow 筛选器关系图显示了一种可能的方法，在筛选器图中，控件节点可以表示为筛选器。 网络提供程序始终是自己的筛选器，并且在其他所有筛选器之前。 在此示例中，由于调谐器和解调器节点组合在同一张卡上，因此它们显示为一个筛选器。 捕获筛选器遵循调谐器/解调器筛选器。 对于这些筛选器，到目前为止，筛选器中的实际内部和外部连接与控件节点匹配。 下一个筛选器是 MPEG-2 传输流信号分离器，它由公开数据包标识符 (PID) 筛选器的单个筛选器表示，如 " [控制节点](control-nodes.md) " 部分的图所示。 实际的 MPEG-2 传输流信号分离器筛选器根据需要重现拓扑次，以处理所有基本流。

![说明在一个筛选器中组合了调谐器和解调器的 directshow 筛选器图形的示意图](images/smpdshw1.png)

 

 




