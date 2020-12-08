---
title: 分隔单个筛选器中的节点
description: 分隔单个筛选器中的节点
keywords:
- 控制节点 WDK BDA
- 节点 WDK BDA
- 分隔筛选器中的节点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23f9a61afbef96d403a035ba70aad366aee62786
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796433"
---
# <a name="separating-nodes-in-individual-filters"></a>分隔单个筛选器中的节点





下面的示例 DirectShow 筛选器关系图显示了另一种方法，在该方法中，控件节点可以表示为筛选器关系图中的筛选器。 在此示例中，将 "调谐器" 和 "解调器" 控制节点分成单独的筛选器。 所有其他控件节点均如 "筛选器" 部分的 " [合并节点](combining-nodes-in-a-filter.md) " 中所述。

![用单独的调谐器和解调器筛选器说明 directshow 筛选器图形的示意图](images/smpdshw2.png)

 

 




