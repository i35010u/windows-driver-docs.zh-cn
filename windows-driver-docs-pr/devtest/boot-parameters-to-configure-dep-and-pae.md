---
title: 用于配置 DEP 和 PAE 的启动参数
description: 用于配置 DEP 和 PAE 的启动参数
ms.assetid: cb8b6298-e679-4ca3-8b94-4f0c6af23a3f
keywords:
- 引导参数 WDK
- 启动入口参数 WDK
- DEP WDK 引导参数
- 数据执行保护 WDK 引导参数
- 物理地址扩展 WDK 引导参数
- PAE WDK 引导参数
- 硬件强制执行 DEP WDK 引导参数
- 强制执行软件的 DEP WDK 引导参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac10907d10d41c66b677f8090e3c1251bde3f8d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360412"
---
# <a name="boot-parameters-to-configure-dep-and-pae"></a>用于配置 DEP 和 PAE 的启动参数


本主题说明如何使用引导参数来启用、 禁用和配置支持这些功能的操作系统上的数据执行保护 (DEP) 和物理地址扩展 (PAE)。

有关用于 DEP 和 PAE 信息的启动参数，请参阅[ **BCDEdit /set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)命令并**nx**并**pae**选项。

**重要**  DEP 是一项高度有效的安全功能，除非您别无选择，否则不应禁用。 DEP 和 PAE 的默认设置是最适合于大多数系统。 不要更改默认设置，除非它们会干扰基本处理任务。 本部分包括在内，以演示如何配置这些功能，但它不应当被解释为建议更改默认设置。

 

### <a name="span-iddepandpaebootparametersspanspan-iddepandpaebootparametersspandep-and-pae-boot-parameters"></a><span id="dep_and_pae_boot_parameters"></span><span id="DEP_AND_PAE_BOOT_PARAMETERS"></span>DEP 和 PAE 引导参数

在启动时启用并配置的设置的值的 DEP 项和 PAE **nx**并**pae**使用的参数[ **BCDEdit /set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)命令。

这些启动参数具有冲突的作用。 若要配置 DEP 和 PAE，使用仅为每个参数的文档中所述和本主题中讨论的参数组合。 不着有冲突的参数，尤其是在生产系统上。

### <a name="span-idtheinteractionofdepandpaebootparametersspanspan-idtheinteractionofdepandpaebootparametersspanthe-interaction-of-dep-and-pae-boot-parameters"></a><span id="the_interaction_of_dep_and_pae_boot_parameters"></span><span id="THE_INTERACTION_OF_DEP_AND_PAE_BOOT_PARAMETERS"></span>DEP 和 PAE 引导参数的交互

有两种类型的 DEP:

-   *硬件强制实施 DEP*为内核模式和用户模式进程启用 DEP。 它必须受处理器和操作系统。

<!-- -->

-   *软件实施 DEP*仅在用户模式进程启用 DEP。 它必须由操作系统支持。

在 32 位版本的 Windows，*硬件强制实施 DEP*需要 PAE，这受支持的所有 Windows 操作系统支持 dep。 具有支持硬件强制实施的 DEP 的处理器的计算机上启用 DEP 时，Windows 将自动启用 PAE 并忽略禁用它的启动参数值。

下一节中总结了每个 Windows 操作系统的参数组合。

### <a name="span-iddepandpaeparametercombinationsspanspan-iddepandpaeparametercombinationsspandep-and-pae-parameter-combinations"></a><span id="dep_and_pae_parameter_combinations"></span><span id="DEP_AND_PAE_PARAMETER_COMBINATIONS"></span>DEP 和 PAE 参数组合

以下列表介绍可以用于配置 DEP 和 PAE 的启动参数组合。

**请注意**可选 **{** <em>ID</em> **}** 是特定 Windows 引导加载程序启动项，你想要配置的 GUID。 如果未指定 **{** <em>ID</em> **}** ，命令将修改当前操作系统启动项目。 有关详细信息，请参阅[ **BCDEdit /set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)命令。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left"></th>
<th align="left">Windows Vista 及更高版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>若要启用 DEP</strong></p>
<p>（选择一个参数组合）</p>
<p>支持硬件强制执行 DEP 的计算机上启用 DEP 时，这些参数组合还启用 PAE。</p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptIn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptOut</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>若要启用 DEP 和 PAE 具有软件强制实施的 DEP 的系统上</strong></p>
<p>（选择一个参数组合）</p>
<p>在计算机上支持硬件强制实施的 DEP，PAE 会自动启用时启用 dep。</p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae default</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptIn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae default</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptOut</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae default</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>若要禁用 DEP，但启用 PAE</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceEnable</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>若要禁用 DEP，但启用 PAE</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceEnable</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>若要禁用 DEP 和 PAE</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceDisable</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>若要禁用 DEP 和 PAE</strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 





