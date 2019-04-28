---
title: 用于测试驱动程序是否支持多个处理器组的启动参数
description: 用于测试驱动程序是否支持多个处理器组的启动参数
ms.assetid: 8ce311d6-a182-4d04-a453-81f6abe2043b
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: c8b605a0430e60956392ffbcea88bd3d58300293
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344913"
---
# <a name="boot-parameters-to-test-drivers-for-multiple-processor-group-support"></a>用于测试驱动程序是否支持多个处理器组的启动参数


Windows 7 和 Windows Server 2008 R2 具有超过 64 个处理器的计算机提供支持。 这种支持通过实现简介[处理器组](https://go.microsoft.com/fwlink/p/?linkid=155063)。 出于测试目的，可以配置具有多个逻辑处理器，通过限制组大小具有多个处理器组的任何计算机。 这意味着您可以测试驱动程序和多个处理器组的兼容性具有 64 或更少的逻辑处理器的计算机上的组件。

**请注意**  这一概念*处理器组*，引入了 Windows 7，允许现有 Api 和 DDIs 以继续使用超过 64 个逻辑处理器的计算机上工作。 通常情况下，由长度是 64 位关联掩码表示组的处理器。 具有超过 64 个逻辑处理器的任何计算机都必须多个组。
创建一个过程后，该过程分配给特定组。 默认情况下，此进程线程可以运行的所有逻辑处理器的同一组中，尽管可以显式更改线程关联。 调用任何 API 或 DDI 采用的关联掩码或处理器编号作为参数，但不是组数字、 仅限于影响或报告调用线程的组中的处理器。 这同样适用的 Api 或返回相关性掩码或处理器编号，例如 DDIs **GetSystemInfo**。

从 Windows 7 开始，应用程序或驱动程序可以进行扩展的旧 Api 的函数的使用。 这些新组感知函数接受组号自变量来明确地限定处理器数或关联掩码，并因此可以操作调用线程的组之外的处理器。 当涉及到旧的 Api 或 DDIs 时，驱动程序和运行在计算机中的不同组中的组件之间的交互引入 bug 的可能性。 在 Windows 7 和 Windows Server 2008 R2 上，可以使用传统的非可识别组的 Api。 但是，驱动程序要求是更严格。 必须将任何 DDI 的处理器数或蒙板接受作为没有随附的处理器组参数或返回处理器数或掩码而无需为具有多个处理器组的计算机上的驱动程序的功能是否正确，随附的处理器组。 这些旧的非可识别组的 DDIs 可以具有多个进程组，因为推断出的组可能会不同于适用哪个调用线程的计算机上后无法正常执行。 因此，使用这些旧 DDIs 和针对 Windows Server 2008 R2 驱动程序必须更新为使用新的扩展的版本的界面。 驱动程序不调用任何函数，使用处理器关联掩码或处理器编号将正常运行，而不考虑的处理器数。 调用新 DDIs 的驱动程序可以通过包含 procgrp.h 标头，运行以前版本的 Windows 上调用[ **WdmlibProcgrpInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff565629)，并针对[处理器组兼容性库](https://msdn.microsoft.com/library/windows/hardware/ff559909)(procgrp.lib)。

可识别组的新 Api 和 DDIs 的详细信息，请下载白皮书[具有超过 64 个逻辑处理器的支持系统：面向开发人员准则](https://go.microsoft.com/fwlink/p/?linkid=147914)。

 

若要帮助确定潜在处理器与组相关的问题在驱动程序和组件中，可以使用[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)选项。 两个 BCD 启动配置设置， **groupsize**并**maxgroup**，可以配置具有多个逻辑处理器，支持多个处理器组的任何计算机。 **Groupaware**选项修改某些 DDIs 的行为和操作组环境以进行测试。

### <a name="span-idcreatemultipleprocessorgroupsbychangingthegroupsizespanspan-idcreatemultipleprocessorgroupsbychangingthegroupsizespancreate-multiple-processor-groups-by-changing-the-group-size"></a><span id="create_multiple_processor_groups_by_changing_the_group_size"></span><span id="CREATE_MULTIPLE_PROCESSOR_GROUPS_BY_CHANGING_THE_GROUP_SIZE"></span>通过更改组大小来创建多个处理器组

**Groupsize**选项在组中指定的最大逻辑处理器数。 默认情况下**groupsize**未设置选项，并具有 64 或更少的逻辑处理器的任何计算机都有一个组，这是组 0。

**请注意**  物理处理器或处理器包可以有一个或多个内核或处理器单元，其中每个可以包含一个或多个逻辑处理器。 在操作系统认为逻辑处理器作为一种逻辑计算引擎。

 

若要创建多个处理器组，请运行[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)在提升的命令提示符窗口，并指定新*maxsize*值**groupsize** ，它是少于逻辑处理器的总数。 请注意组大小设置用于测试，不应使用此设置配置传送系统。 *Maxsize*值可以设置为 1 到 64 （含) 之间的 2 的任意次幂。 该命令使用以下语法：

```
bcdedit.exe /set groupsize maxsize
```

例如，以下命令设置的最大处理器数为 2 组中。

```
bcdedit.exe /set groupsize 2
```

如果非 NUMA 计算机有 8 个逻辑处理器，则将设置**groupsize** 2 使用 2 个逻辑处理器每个创建 4 个处理器组。

组 0:1 包含 1 个包的 2 个逻辑处理器的 NUMA 节点

组 1:1 包含 1 个包的 2 个逻辑处理器的 NUMA 节点

组 2:1 包含 1 个包的 2 个逻辑处理器的 NUMA 节点

组 3:1 包含 1 个包的 2 个逻辑处理器的 NUMA 节点

根据设计，在非 NUMA 计算机被视为具有一个 NUMA 节点。 NUMA 节点不能跨组，因为系统会创建每个组的节点后重新启动计算机。

如果**groupsize**设置为小于其概念包后重新启动，包不跨越一组系统一些专门选出中物理处理器包 （套接字），逻辑处理器数的值。 这意味着，不是实际存在的更多包报告的处理器拓扑 Api。 这也意味着许可限制的 Windows （包级别） 处理器可能会阻止某些处理器包启动时**groupsize**设置。

处理器包可以跨组，如果它在其中定义的多个 NUMA 节点，系统将这些节点分配给不同的组。

Windows 限制受支持的组的数。 用新版本的 Windows 或 service pack 版本中，可以更改此数字。 驱动程序或组件不应依赖于 Windows 支持为常量的组数。 组数的限制可以限制允许启动时用于值较小的逻辑处理器数**groupsize**启动选项。

若要删除**groupsize**设置您用于测试并返回到 64 个逻辑处理器每个组的默认设置，请使用以下 BCDEdit 命令。

```
bcdedit.exe /deletevalue groupsize
```

此命令是设置的等效**groupsize**为 64。

### <a name="span-idmaximizethenumberofprocessorgroupsspanspan-idmaximizethenumberofprocessorgroupsspanmaximize-the-number-of-processor-groups"></a><span id="maximize_the_number_of_processor_groups"></span><span id="MAXIMIZE_THE_NUMBER_OF_PROCESSOR_GROUPS"></span>最大化处理器组的数

**Maxgroup**选项是另一种方法来创建具有多个逻辑处理器和 NUMA 节点的计算机上的处理器组。 **Maxgroup**启动选项没有任何影响非 NUMA 的计算机上。

若要最大化的组数，请运行[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令，在提升的命令提示符窗口。 该命令使用以下语法：

```
bcdedit.exe /set maxgroup on
```

例如，考虑具有 2 个 NUMA 节点、 1 个处理器包每个节点，以及每个包，共 8 个逻辑处理器的 4 个处理器核心的计算机。

默认组配置为：

组 0:8 个逻辑处理器，2 个包，2 个 NUMA 节点

如果输入**bcdedt.exe/上设置 maxgroup**命令并后接一次重启，该命令将生成下面的组配置：

组 0:4 个逻辑处理器、 1 个包、 1 个 NUMA 节点

组 1:4 个逻辑处理器、 1 个包、 1 个 NUMA 节点

请注意，NUMA 节点分配到组中最大化的组数的方式。

若要更改回默认设置，请使用以下**BCDEdit**命令。

```
bcdedit.exe /set maxgroup off
```

### <a name="span-idtestmultiplegroupcompatibilitybysettingthegroupawarebootoptispanspan-idtestmultiplegroupcompatibilitybysettingthegroupawarebootoptispantest-multiple-group-compatibility-by-setting-the-group-aware-boot-option"></a><span id="test_multiple_group_compatibility_by_setting_the_group_aware_boot_opti"></span><span id="TEST_MULTIPLE_GROUP_COMPATIBILITY_BY_SETTING_THE_GROUP_AWARE_BOOT_OPTI"></span>通过设置组注意启动选项测试多个组的兼容性

Windows 7 和 Windows Server 2008 R2 引入了新的 BCD 选项 (**groupaware**)，会强制驱动程序和组件需要注意的多个处理器组环境中的多个组。 **Groupaware**选项更改设备驱动程序函数，以帮助公开在驱动程序和组件中的跨组不兼容的一组的行为。 可以使用**groupaware**启动选项连同**groupsize**并**maxgroup**选项，可测试具有多个组的驱动程序兼容性时的计算机具有 64 或较少活动的逻辑处理器。

当**groupaware**设置启动选项，则操作系统可确保组 0 以外的组中启动了进程。 这会增加驱动程序和组件之间的跨组交互的机会。 该选项还会修改为不支持组的旧版功能的行为**KeSetTargetProcessorDpc**， **KeSetSystemAffinityThreadEx**，和**KeRevertToUserAffinityThreadEx**，以便它们始终在最高编号组包含活动的逻辑处理器上执行。 应更改驱动程序调用这些旧的函数的任何调用对应的可识别组 (**KeSetTargetProcessorDpcEx**， **KeSetSystemGroupAffinityThread**，和**KeRevertToUserGroupAffinityThread**)，

若要测试兼容性，请使用以下[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令。

```
bcdedit.exe /set groupaware on
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旧的非组注意函数</th>
<th align="left">Windows 7 可识别组替换</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KeSetTargetProcessorDpc</p></td>
<td align="left"><p>KeSetTargetProcessorDpcEx</p></td>
</tr>
<tr class="even">
<td align="left"><p>KeSetSystemAffinityThreadEx</p></td>
<td align="left"><p>KeSetSystemGroupAffinityThread</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KeRevertToUserAffinityThreadEx</p></td>
<td align="left"><p>KeRevertToUserGroupAffinityThread</p></td>
</tr>
</tbody>
</table>

 

若要将计算机重置为默认设置，请使用以下**BCDEdit**命令。

```
bcdedit.exe /set groupaware off
```

 

 





