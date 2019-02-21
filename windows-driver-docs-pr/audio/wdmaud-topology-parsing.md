---
title: 分析 WDMAud 拓扑
description: 分析 WDMAud 拓扑
ms.assetid: 8aa3e2e8-c9a2-4c3e-94b1-44a0dc218bf3
keywords:
- WDMAud 拓扑分析 WDK 音频
- 拓扑分析 WDK 音频
- 源 mixer 行 WDK 音频
- 目标 mixer 行 WDK 音频
- 分析目标混音器行
- 虚拟的 sum WDK 音频
- 转换节点 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ae2a5d872f693c90d805c2adfacecd9fbc3de52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526886"
---
# <a name="wdmaud-topology-parsing"></a>分析 WDMAud 拓扑


## <span id="wdmaud_topology_parsing"></span><span id="WDMAUD_TOPOLOGY_PARSING"></span>


[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)分析首先之前分析源混音器行目标混音器行。 在其中 WDMAud 分析目标行的顺序是相反的顺序 SysAudio 发现行。 例如，首先分析更高版本带编号的 pin。 分析开始的直接父级的 pin，会向上游方向移动。 分析器检测到以下终止条件之一之前，将根据这些规则转换每个节点：

-   正在分析的当前节点是 SUM 节点。

-   当前节点是 MUX 节点。

-   当前节点具有多个父级。

SUM 和 MUX 节点均*经典终止符*的目标行。 SUM 节点不会生成任何控件。 MUX 节点中包含对每个由 MUX 控制的源行的引用的目标行生成 MUX 控件。

如果发现多个父级，则立即终止分析。 Mixer 行驱动程序将解释为"虚拟总和"通过将多个输入在一起形成的这种情况。

目标行的名称来自从返回的名称[ **KSPROPERTY\_PIN\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff565203)上该 pin 的属性。

目标行的所有控件均已都转换后，WDMAud 开始转换的源行。 同样，在其中 WDMAud 分析这些行的顺序是顺序的 SysAudio 查询它们相反。 此外，在其中进行分析的源行的方向是相比于在其中分析目标行的容量。 WDMAud 解析每一行从 pin 开始，直到它检测到下列终止情况之一，在下游方向继续操作：

-   分析器发现目标行。

-   要转换的当前节点所属的目标行。

-   当前节点是 SUM 节点。

-   当前节点是 MUX 节点。

在源行属于目标行的分析过程中遇到 MUX 时, 它将转换为一个控件。 但是，它仅用作占位符以更新 MUX 更高版本存储在目标行中的行号。 最后一个行号尚不可用，因此需要一个占位符。

MUX 和 SUM 节点终止源行;因此，未转换的总和或 MUX 和另一个总和或 MUX 之间的任何节点。

## <a name="span-idnotesspanspan-idnotesspanspan-idnotesspannotes"></a><span id="Notes"></span><span id="notes"></span><span id="NOTES"></span>说明


1.  MUX 中的行名称被派生自行，pin 名除外，当行送入 MUX 的总和或 MUX 节点。 在这种情况下，线的名称是 MUX 或 SUM 节点的名称。 时混音器驱动程序发现此功能，它能够构建一个虚拟 mixer 行，其中求和或 MUX 节点的名称，然后会将转换之间或 MUX 和 MUX 之和的所有控件。

2.  一个*拆分*拓扑中为其中一个节点有多个子级的用例。 如果单个 pin 将路由到两个单独的目标，但是共享一些公共控件，如音量或静音，这很有用。 遇到拆分时，任何时候 WDMAud 驱动程序创建一个新行和所有控件都分析截至拆分的重复项。 发生这种情况无条件地每当遇到拆分时，即使遇到终止源行的总和节点。

 

 




