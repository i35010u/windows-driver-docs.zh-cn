---
title: 无法加载的模块的图形分析
description: 无法加载的模块的图形分析
keywords:
- 内核流调试，无法加载模块
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ceb75497501c4001f52954d3928926065ec99a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813261"
---
# <a name="graph-analysis-with-unloadable-modules"></a>无法加载的模块的图形分析


本部分介绍了在使用无法加载的模块（如 KMixer）时可能会影响你的方案。

加载后，扩展模块在第一次使用命令时进行初始化。 在初始化时，扩展模块会检查是否每个模块都已加载并且具有正确的符号。 如果卸载了任何单个模块或加载了错误的符号，则扩展会禁用用于处理该模块的标识、转储等的库扩展。 在这种情况下，你需要手动重新启用已禁用的模块。

如果在启动时加载扩展，则可能发生上述情况。 具体而言，如果你加载 Ks.dll 然后发出一个，则可能会遇到这种情况 [**。**](-reboot--reboot-target-computer-.md) 或者，如果在 Ks.dll 启动期间中断到调试器，则会发生这种情况。

在下面的示例中，我们将从电传 u 麦克风捕获 (sndrec32) 的两个流。 中断 **拆分器！** 拆分器的筛选器上的 FilterProcess 和运行 [**！ ks**](-ks-graph.md) 生成：

```dbgcmd
kd> !graph ffa0c6d4 7
Attempting a graph build on ffa0c6d4...  Please be patient...
Graph With Starting Point ffa0c6d4:
"usbaudio" Filter ffaaa768, Child Factories 2
    Output Factory 0:
        Pin ffb1caf0 (File 811deeb8, -> "splitter" ffa8b008) Irps(q/p) = 7, 1
"splitter" Filter ffa0c660, Child Factories 2
    Output Factory 0:
        Pin 81250008 (File ffb10028) Irps(q/p) = 3, 0
        Pin 811df9c0 (File ffaaf2f0) Irps(q/p) = 3, 0
    Input Factory 1:
        Pin ffa8b008 (File ffb26d68, <- "usbaudio" ffb1caf0) Irps(q/p) = 1, 7
```

在此示例中，KMixer 已加载并连接到拆分器，但 Kmixer 不显示在图形中。 已将 Irp 排队到拆分器的输出插针，但 **！ ks. graph** 命令无法 backtrace 和发现 KMixer。 发出 [**libexts 详细信息**](-ks-libexts.md) 命令以进行进一步调查：

```dbgcmd
kd> !libexts details
## LibExt Details:
--------------------------------------------------
LibExt "portcls!" :
    Status :  ACTIVE
    This is the port class library extension to the KS DLL.  It supports
    dumping wave cyclic, wave pci, irp streams, and several other upper
    level structures.
    Commands Exported: pciaudio
    Help : pchelp
    Hooks : dump dumpqueue dumpcircuit conv(file) conv(device) graph
LibExt "STREAM!" :
    Status :  ACTIVE
    This is the stream class library extension to the KS DLL.  It supports
    dumping device extensions, filters, streams, and SRBs.
    Hooks : dump enumdevobj graph
LibExt "kmixer!" :
    Status :  INACTIVE
    This is the KMIXER extension to the KS DLL.  It supports
    virtually nothing at this point!
    Hooks : dump graph
```

根据上面的输出，扩展的 KMixer 部分当前被禁用 (状态：非活动) 。 由于扩展模块第一次用于未加载 KMixer 的上下文中，因此 Ks.dll 禁用了扩展的 KMixer 部分，以防止对已卸载模块进行耗时的引用。

若要显式启用 KMixer，可以将 [**！ libexts**](-ks-libexts.md) 与 **enable** 参数一起使用，如下所示：

```dbgcmd
kd> !libexts enable kmixer
LibExt "kmixer" has been enabled.

kd> !graph ffa0c6d4 7
Attempting a graph build on ffa0c6d4...  Please be patient...
Graph With Starting Point ffa0c6d4:
"usbaudio" Filter ffaaa768, Child Factories 2
    Output Factory 0:
        Pin ffb1caf0 (File 811deeb8, -> "splitter" ffa8b008) Irps(q/p) = 7, 1
"splitter" Filter ffa0c660, Child Factories 2
    Output Factory 0:
        Pin 81250008 (File ffb10028, -> "kmixer" 8123c000) Irps(q/p) = 3, 0
        Pin 811df9c0 (File ffaaf2f0, -> "kmixer" 81236000) Irps(q/p) = 3, 0
    Input Factory 1:
        Pin ffa8b008 (File ffb26d68, <- "usbaudio" ffb1caf0) Irps(q/p) = 1, 7
"kmixer" Filter ffa65b70, Child Factories 4
    Input Factory 2:
        Pin 81236000 (File ffaaf7d0, <- "splitter" 811df9c0) Irps(q/p) = 0, 0
    Output Factory 3:
        Pin 81252d00 (File 811df1d8) Irps(q/p) = 10, 0
"kmixer" Filter ffb03808, Child Factories 4
    Input Factory 2:
        Pin 8123c000 (File ffb10130, <- "splitter" 81250008) Irps(q/p) = 0, 0
    Output Factory 3:
        Pin ffa1e9c0 (File 81253468) Irps(q/p) = 10, 0
```

KMixer 现在会按预期显示在捕获关系图中。

 

 





