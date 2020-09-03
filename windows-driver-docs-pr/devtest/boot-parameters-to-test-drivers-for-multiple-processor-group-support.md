---
title: 用于测试驱动程序是否支持多个处理器组的启动参数
description: 用于测试驱动程序是否支持多个处理器组的启动参数
ms.assetid: 8ce311d6-a182-4d04-a453-81f6abe2043b
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: a84a965e87f0c1c8f774e226be7be49d5f8028b0
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384351"
---
# <a name="boot-parameters-to-test-drivers-for-multiple-processor-group-support"></a>用于测试驱动程序是否支持多个处理器组的启动参数


Windows 7 和 Windows Server 2008 R2 为具有超过64个处理器的计算机提供支持。 这种支持是通过引入 [处理器组](/windows/win32/procthread/processor-groups)来实现的。 出于测试目的，可以将具有多个逻辑处理器的任何计算机配置为具有多个处理器组，方法是限制组大小。 这意味着，可以在具有64个或更少逻辑处理器的计算机上测试多个处理器组兼容性的驱动程序和组件。

**注意**   Windows 7 中引入的*处理器组*的概念使现有 Api 和 DDIs 能够在超过64个逻辑处理器的计算机上继续工作。 通常，组的处理器由关联掩码表示，后者长度为64位。 具有超过64个逻辑处理器的任何计算机都必须有多个组。
创建进程时，该进程将分配给特定组。 默认情况下，进程的线程可以在同一组的所有逻辑处理器上运行，尽管可以显式更改线程关联。 对使用关联掩码或处理器编号作为参数而不是组号的任何 API 或 DDI 的调用，只能影响调用线程组中这些处理器上的或报告。 这同样适用于返回关联掩码或处理器编号（如 **GetSystemInfo**）的 Api 或 DDIs。

从 Windows 7 开始，应用程序或驱动程序可以使用扩展旧版 Api 的函数。 这些新的组感知函数接受组号参数以明确限定处理器编号或关联掩码，因此可以操作调用线程的组以外的处理器。 在计算机中的不同组中运行的驱动程序和组件之间的交互会在涉及到旧 Api 或 DDIs 时引入 bug。 可以在 Windows 7 和 Windows Server 2008 R2 上使用旧版的非组感知 Api。 但是，驱动程序要求更为严格。 对于具有多个处理器组的计算机上的驱动程序的功能是否正确，你必须将接受处理器号或掩码的任何 DDI 替换为不带随附处理器组的参数，或者返回不带随附处理器组的处理器号或掩码。 这些旧式的非组感知 DDIs 在具有多个进程组的计算机上可能不稳定，因为推断组可能不同于调用线程所需的组。 因此，使用这些旧式 DDIs 的驱动程序和面向 Windows Server 2008 R2 的驱动程序必须更新为使用新的扩展版本的接口。 不调用任何使用处理器关联掩码或处理器编号的函数的驱动程序将正常运行，而不考虑处理器的数量。 调用新 DDIs 的驱动程序可在以前版本的 Windows 上运行，方法是：包括 procgrp 标头、调用 [**WdmlibProcgrpInitialize**](/windows-hardware/drivers/ddi/procgrp/nf-procgrp-wdmlibprocgrpinitialize)，并链接到 [处理器组兼容性库](/windows-hardware/drivers/ddi/index) (procgrp) 。

有关新的组感知 Api 和 DDIs 的详细信息，请下载 [支持超过64个逻辑处理器的系统的白皮书：面向开发人员的准则](https://download.microsoft.com/download/a/d/f/adf1347d-08dc-41a4-9084-623b1194d4b2/MoreThan64proc.docx)。

 

若要帮助确定驱动程序和组件中与处理器组相关的潜在问题，可以使用 [**BCDEdit/set**](./bcdedit--set.md) 选项。 这两个 BCD 启动配置设置 **groupsize** 和 **maxgroup**可以配置具有多个逻辑处理器的任何计算机，以支持多个处理器组。 **Groupaware**选项会修改特定 DDIs 的行为，并出于测试目的操作组环境。

### <a name="span-idcreate_multiple_processor_groups_by_changing_the_group_sizespanspan-idcreate_multiple_processor_groups_by_changing_the_group_sizespancreate-multiple-processor-groups-by-changing-the-group-size"></a><span id="create_multiple_processor_groups_by_changing_the_group_size"></span><span id="CREATE_MULTIPLE_PROCESSOR_GROUPS_BY_CHANGING_THE_GROUP_SIZE"></span>通过更改组大小来创建多个处理器组

**Groupsize**选项指定组中的逻辑处理器的最大数量。 默认情况下，未设置 **groupsize** 选项，并且具有64或更少逻辑处理器的任何计算机都有一个组0。

**注意**   物理处理器或处理器包可以有一个或多个核心或处理器单元，其中每个都可以包含一个或多个逻辑处理器。 操作系统将逻辑处理器视为一个逻辑计算引擎。

 

若要创建多个处理器组，请在提升的命令提示符窗口中运行[**BCDEdit/set**](./bcdedit--set.md) ，并为**groupsize**指定一个小于逻辑处理器总数的新*maxsize*值。 请注意，"组大小" 设置用于测试，不应配置带有此设置的 "发运系统"。 *Maxsize*值可以设置为1到64之间的任何2次幂。 该命令使用以下语法：

```
bcdedit.exe /set groupsize maxsize
```

例如，以下命令将组中的最大处理器数设置为2。

```
bcdedit.exe /set groupsize 2
```

如果非 NUMA 计算机有8个逻辑处理器，则将 **groupsize** 设置为2将创建4个处理器组，每个处理器组有2个逻辑处理器。

包含2个逻辑处理器的1个包的组 0: 1 NUMA 节点

包含2个逻辑处理器的1个包的组 1: 1 NUMA 节点

包含2个逻辑处理器的1个包的组 2: 1 NUMA 节点

包含2个逻辑处理器的1个包的组 3: 1 NUMA 节点

按照设计，非 NUMA 计算机被视为具有一个 NUMA 节点。 由于 NUMA 节点不能跨组，系统会在重新启动计算机后为每个组创建一个节点。

如果 **groupsize** 的值小于物理处理器包 (插槽) 中的逻辑处理器数，则系统会在重新启动时重新定义包的概念，以便包不会跨组。 这意味着处理器拓扑 Api 会报告比实际存在的包多的包。 这也意味着，在设置 **groupsize** 时，Windows (包级) 处理器授权限制可能会阻止某些处理器包的启动。

如果处理器包中定义了多个 NUMA 节点，并且系统将这些节点分配给不同的组，则它可以跨组。

Windows 限制了支持的组数。 在新版本的 Windows 或 Service Pack 版本中，此数字可能会发生变化。 驱动程序或组件不应依赖于 Windows 支持的组数。 当使用小值作为 **groupsize** boot 选项时，对组数的限制可能会限制允许启动的逻辑处理器的数量。

若要删除用于测试的 **groupsize** 设置并返回每个组64逻辑处理器的默认设置，请使用以下 BCDEdit 命令。

```
bcdedit.exe /deletevalue groupsize
```

此命令等效于将 **groupsize** 设置为64。

### <a name="span-idmaximize_the_number_of_processor_groupsspanspan-idmaximize_the_number_of_processor_groupsspanmaximize-the-number-of-processor-groups"></a><span id="maximize_the_number_of_processor_groups"></span><span id="MAXIMIZE_THE_NUMBER_OF_PROCESSOR_GROUPS"></span>最大化处理器组的数目

**Maxgroup**选项是在具有多个逻辑处理器和 NUMA 节点的计算机上创建处理器组的另一种方法。 **Maxgroup** boot 选项在非 NUMA 计算机上不起作用。

若要最大程度地增加组数，请在提升的命令提示符窗口中运行 [**BCDEdit/set**](./bcdedit--set.md) 命令。 该命令使用以下语法：

```
bcdedit.exe /set maxgroup on
```

例如，假设有一个具有2个 NUMA 节点的计算机，每个节点1个处理器包，每个包4个处理器核心，总共8个逻辑处理器。

默认组配置是：

组 0: 8 逻辑处理器，2个包，2个 NUMA 节点

如果在命令后输入 **bcdedt.exe/set maxgroup** ，然后重新启动，则该命令将生成以下组配置：

组 0: 4 逻辑处理器，1个包，1个 NUMA 节点

组 1: 4 逻辑处理器，1个包，1个 NUMA 节点

请注意，NUMA 节点以最大化组数的方式分配给组。

若要更改回默认设置，请使用以下 **BCDEdit** 命令。

```
bcdedit.exe /set maxgroup off
```

### <a name="span-idtest_multiple_group_compatibility_by_setting_the_group_aware_boot_optispanspan-idtest_multiple_group_compatibility_by_setting_the_group_aware_boot_optispantest-multiple-group-compatibility-by-setting-the-group-aware-boot-option"></a><span id="test_multiple_group_compatibility_by_setting_the_group_aware_boot_opti"></span><span id="TEST_MULTIPLE_GROUP_COMPATIBILITY_BY_SETTING_THE_GROUP_AWARE_BOOT_OPTI"></span>通过设置 "感知启动" 选项来测试多组兼容性

Windows 7 和 Windows Server 2008 R2 引入了一个 (**groupaware**) 的新 BCD 选项，该选项强制驱动程序和组件了解多处理器组环境中的多个组。 **Groupaware**选项更改一组设备驱动程序功能的行为，以帮助在驱动程序和组件中公开跨组不兼容问题。 可以结合使用 **groupaware** boot 选项和 **groupsize** 和 **maxgroup** 选项，在计算机具有64或更低的活动逻辑处理器时，与多个组测试驱动程序的兼容性。

设置 **groupaware** boot 选项后，操作系统将确保在组0以外的组中启动进程。 这增加了驱动程序和组件之间跨组交互的机会。 选项还会修改不是组感知、 **KeSetTargetProcessorDpc**、 **KeSetSystemAffinityThreadEx**和 **KeRevertToUserAffinityThreadEx**的旧函数的行为，以便它们始终对包含活动逻辑处理器的最高编号组进行操作。 应更改调用这些旧函数的驱动程序，以便 (**KeSetTargetProcessorDpcEx**、 **KeSetSystemGroupAffinityThread**和 **KeRevertToUserGroupAffinityThread**) 调用其组感知对应项。

若要测试兼容性，请使用以下 [**BCDEdit/set**](./bcdedit--set.md) 命令。

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
<th align="left">旧的非组感知函数</th>
<th align="left">Windows 7 组感知替换</th>
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

 

若要将计算机重置为默认设置，请使用以下 **BCDEdit** 命令。

```
bcdedit.exe /set groupaware off
```

 

