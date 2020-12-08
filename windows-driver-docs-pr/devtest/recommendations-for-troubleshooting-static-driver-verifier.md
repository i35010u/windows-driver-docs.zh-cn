---
title: 有关排查静态驱动程序验证程序问题的建议
description: 有关排查静态驱动程序验证程序问题的建议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da00998d006706b7134ec51b7086d3d5d981c75e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837309"
---
# <a name="recommendations-for-troubleshooting-static-driver-verifier"></a>有关排查静态驱动程序验证程序问题的建议


当你在驱动程序源代码上运行 (SDV) 的静态驱动程序验证程序，并且 SDV 报表超时、放弃或 Spaceout 时，请尝试执行以下操作：

-   以下建议需要更改 SDV 配置设置。 可以在 "配置" 选项卡上的 " **配置** " 选项卡、"资源" 或 [静态驱动程序验证程序选项文件](static-driver-verifier-options-file.md)中，直接在 static driver Verfier 中设置配置设置，Sdv-defaults.xml。 默认选项文件特定于驱动程序模型，可以在 \\ 工具 \\ sdv \\ 数据 \\ 模型目录中找到 \\ ，其中 model 为 WDM，WDF，NDIS，或 Storport。
    1.  如果计算机具有多核处理器，请将验证期间使用的线程数减少到1。 在 " **配置** " 选项卡上的 "资源" 组中，从下拉列表中选择 "1"。 在 SDV 默认文件中，将 SDV SlamConfig NumberOfTheads 的值更改 \_ \_ 为1。
    2.  如果 SDV 报告超时，则增加超时限制。 此值用于限制 SDV 验证规则所花费的时间。 默认值为50分钟 (3000 秒) 。 在 " **配置** " 选项卡上的 "资源" 组中，可以通过将 **最长时间** (分钟) 更改来调整设置。 在选项文件中，可以更改 SDV \_ SlamConfig \_ 超时值。 最小值为 10 (秒) ，最大值为 86400 (秒) 。 例如，你可能想要将 SDV SlamConfig Timeout 的值 \_ 翻倍 \_ 为6000。
-   如果这些建议均不能帮助解决问题，请尝试将它们一起应用。

**注意**   这些方法会增加运行的实际持续时间，但也会使 SDV 完成其工作，并 (通过或脱离) ，从而使其更易于工作。
