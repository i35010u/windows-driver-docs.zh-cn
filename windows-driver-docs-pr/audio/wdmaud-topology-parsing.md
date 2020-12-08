---
title: WDMAud 拓扑分析
description: WDMAud 拓扑分析
keywords:
- WDMAud 拓扑分析 WDK 音频
- 分析 WDK 音频的拓扑
- 源混合器线条 WDK 音频
- 目标混音器线条 WDK 音频
- 分析目标混合器行
- 虚拟和 WDK 音频
- 翻译节点 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9346b84b249c5b5a2ce82a7077bf9eb472a8fe2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798733"
---
# <a name="wdmaud-topology-parsing"></a>WDMAud 拓扑分析


## <span id="wdmaud_topology_parsing"></span><span id="WDMAUD_TOPOLOGY_PARSING"></span>


[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)首先分析目标混音器行，然后再分析源混合器行。 WDMAud 分析目标行的顺序与 SysAudio 发现行的顺序相反。 例如，首先分析编号较高的 pin。 分析从 pin 的直接父项开始，并沿上游方向移动。 每个节点都根据这些规则进行转换，直到分析器检测到以下终止条件之一：

-   正在分析的当前节点是一个 SUM 节点。

-   当前节点是一个 MUX 节点。

-   当前节点有多个父节点。

SUM 和 MUX 节点是目标行的 *经典终结* 器。 SUM 节点不会生成任何控件。 MUX 节点在目标行中生成一个 MUX 控件，该控件包含对 MUX 控制的每个源行的引用。

如果发现多个父项，分析将立即终止。 混音器驱动程序将此条件解释为 "虚拟求和"，它通过将多个输入组合在一起形成。

目标行的名称来自该 pin 上的 [**KSPROPERTY \_ 引脚 \_ name**](../stream/ksproperty-pin-name.md) 属性返回的名称。

所有目标行控件都已转换后，WDMAud 开始转换源行。 同样，WDMAud 分析这些行的顺序与 SysAudio 查询它们的顺序相反。 另外，分析源行的方向与分析目标行的方向相反。 WDMAud 分析从 pin 开始的每行并在下游方向继续，直到它检测到以下终止条件之一：

-   分析器查找目标行。

-   正在转换的当前节点属于目标行。

-   当前节点是一个 SUM 节点。

-   当前节点是一个 MUX 节点。

如果在分析属于目标行的源行的过程中遇到 MUX，则会将其转换为控件。 但是，它仅用作占位符，以便在以后更新存储在目标行中的行号。 最终行号目前尚不可用，因此需要一个占位符。

MUX 和 SUM 节点均终止源行;因此，不会转换 SUM 或 MUX 与其他 SUM 或 MUX 之间的任何节点。

## <a name="span-idnotesspanspan-idnotesspanspan-idnotesspannotes"></a><span id="Notes"></span><span id="notes"></span><span id="NOTES"></span>本票


1.  MUX 中的行名称是从行的 pin 名称派生而来的，但从 SUM 或 MUX 节点送到 MUX 的行除外。 在这种情况下，行的名称是 MUX 或 SUM 节点的名称。 当混音器驱动程序发现这一点时，它将生成一个具有 SUM 或 MUX 节点名称的虚拟混音器行，然后在 SUM 或 MUX 与 MUX 之间转换所有控件。

2.  拓扑中的 *拆分* 是指一个节点具有多个子节点的情况。 当单个 pin 路由到两个不同的目标但共享某些公共控件，如卷或静音时，这非常有用。 任何时候只要发生拆分，WDMAud 驱动程序就会创建一个新行，并复制所有分析到拆分的控件。 只要遇到拆分，就会发生这种情况，即使在遇到终止源行的 SUM 节点之后也是如此。

 

