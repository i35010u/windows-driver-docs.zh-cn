---
title: 合并筛选器中的节点
description: 合并筛选器中的节点
ms.assetid: ebceb42a-966d-4c03-b4f5-8666284fc871
keywords:
- 控制节点 WDK BDA
- 节点 WDK BDA
- 合并筛选器 WDK BDA 中的节点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0853494988f4e05c653b504c6b7e179a820e58c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545216"
---
# <a name="combining-nodes-in-a-filter"></a>合并筛选器中的节点





下图示例 DirectShow 筛选器关系图的演示了一种在其中控制节点可表示为筛选器关系图中的筛选器。 网络提供程序始终是自己的筛选器，位于所有其他筛选器。 在此示例中，由于调谐器和解调器节点组合在同一个线路卡，它们显示为一个筛选器。 捕获筛选器遵循调谐器/解调器筛选器。 对于所有这些筛选器到目前为止，在筛选器中的实际内部和外部连接匹配的控件节点。 下游的下一个筛选器是 mpeg-2 传输流信号分离器，由在图中所示公开数据包标识符 (PID) 筛选器有单个筛选器表示[控制节点](control-nodes.md)部分。 实际的 mpeg-2 传输流信号分离器筛选重现尽可能多地处理所有基本流所需的拓扑。

![说明具有调谐器和解调器组合在一个筛选器的 directshow 筛选器关系图的关系图](images/smpdshw1.png)

 

 




