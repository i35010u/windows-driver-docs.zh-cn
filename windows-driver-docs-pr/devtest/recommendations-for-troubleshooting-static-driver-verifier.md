---
title: 有关排查静态驱动程序验证程序问题的建议
description: 有关排查静态驱动程序验证程序问题的建议
ms.assetid: 14c39437-12ca-4938-93bb-79bbcb192de2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67beefeaa8b9314da081fec011400c2d76402d23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323367"
---
# <a name="recommendations-for-troubleshooting-static-driver-verifier"></a>有关排查静态驱动程序验证程序问题的建议


针对驱动程序源代码和 SDV 报表超时、 放弃、 或 Spaceout 运行 Static Driver Verifier (SDV) 时，请尝试以下操作：

-   以下建议要求对 SDV 配置设置的更改。 可以在设置的配置设置直接中静态驱动程序 Verfier**配置**选项卡上，在以下资源，或在[静态驱动程序验证工具选项文件](static-driver-verifier-options-file.md)，Sdv defaults.xml。 默认选项文件是特定于驱动程序模型，可在\\工具\\sdv\\数据\\模型\\模型所在 WDM、 WDF、 NDIS 或 Storport 的目录。
    1.  如果您的计算机具有多核处理器，减少为 1 的验证过程中使用的线程数。 在上的资源组**配置**选项卡上，从下拉列表中选择 1。 在 SDV 默认值文件中，将值更改为 SDV\_SlamConfig\_NumberOfTheads 为 1。
    2.  SDV 将报告超时，如果增加超时限制。 此值限制 SDV 用于验证规则的时间量。 默认值为 50 分钟 （3000 秒为单位）。 在上的资源组**配置**选项卡上，您可以通过更改调整设置**的最长时间**（分钟）。 在选项文件中，可以更改 SDV\_SlamConfig\_超时值。 最小值是 10(Sec) 和最大值是 86400(Sec)。 例如，你可能想要的 SDV double 值\_SlamConfig\_6000 的超时。
-   如果以上建议帮助您解决问题，请尝试将它们组合在一起应用。

**请注意**这些技术增加运行的实际持续时间，但它们也更便于 SDV 完成其工作，并让有用结果 （传递或缺陷）。
