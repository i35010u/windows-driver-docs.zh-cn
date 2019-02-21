---
title: 无法加载模块的图形分析
description: 无法加载模块的图形分析
ms.assetid: 12441fa1-3d19-4485-815c-546367f31567
keywords:
- 流式处理调试，无法加载模块的内核
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22993d158783a7661bb55bf0c24dc275b2a390c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547492"
---
# <a name="graph-analysis-with-unloadable-modules"></a>无法加载模块的图形分析


本部分介绍可能影响您，如果你正在使用如 KMixer 无法加载模块的方案。

在加载后，扩展模块初始化在第一个命令的用法。 在初始化时，扩展模块检查每个模块是否已加载并且具有正确的符号。 如果任何单个模块卸载或错误的符号加载，该扩展将禁用库扩展插件用于处理标识、 转储，等等。 对于该模块。 在这种情况下，需要手动重新启用已禁用的模块。

如果在启动时加载扩展插件，则可能会出现上述情况。 如果加载 Ks.dll，然后发出具体而言，可能会遇到这种情况下[ **.reboot** ](-reboot--reboot-target-computer-.md)命令。 或者，如果在启动期间进入调试器此时加载 Ks.dll 可能发生。

在以下示例中，我们捕获来自电报 USB 麦克风的两个流 (sndrec32)。 中断**拆分器 ！FilterProcess**并运行[ **！ ks.graph** ](-ks-graph.md)拆分器的筛选器将生成：

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

在此示例中，KMixer 已加载并连接到拆分器，但 Kmixer 不会出现在关系图。 有 Irp 排队到拆分器的输出插针，但在 **！ ks.graph**命令无法反向跟踪，并发现 KMixer。 问题[ **！ ks.libexts 详细信息**](-ks-libexts.md)命令以进行进一步的调查：

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

根据上面的输出，该扩展的 KMixer 部分当前已禁用 (状态：非活动）。 由于扩展模块首先 KMixer 未在其中加载的上下文中使用 Ks.dll 已禁用的扩展，以防止对已卸载的模块的耗时引用 KMixer 部分。

若要显式启用 KMixer，可以使用[ **！ ks.libexts** ](-ks-libexts.md)与**启用**参数，按如下所示：

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

KMixer 现在显示按预期方式捕获图形中。

 

 





