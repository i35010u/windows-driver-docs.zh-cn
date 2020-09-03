---
title: 用于配置 DEP 和 PAE 的启动参数
description: 用于配置 DEP 和 PAE 的启动参数
ms.assetid: cb8b6298-e679-4ca3-8b94-4f0c6af23a3f
keywords:
- 启动参数 WDK
- 启动项参数 WDK
- DEP WDK 启动参数
- 数据执行保护 WDK 启动参数
- 物理地址扩展 WDK 启动参数
- PAE WDK 启动参数
- 硬件强制执行 DEP 启动参数
- 软件强制 DEP 启动参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3c952d5b3649d43322ee3c084379dfe72f4a605
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384369"
---
# <a name="boot-parameters-to-configure-dep-and-pae"></a>用于配置 DEP 和 PAE 的启动参数


本主题说明如何使用启动参数在支持这些功能的操作系统上启用、禁用和配置数据执行保护 (DEP) 和物理地址扩展 (PAE) 。

有关 DEP 和 PAE 的启动参数的信息，请参阅 [**BCDEdit/set**](./bcdedit--set.md) 命令和 **nx** 和 **PAE** 选项。

**重要提示**   DEP 是一种非常有效的安全功能，除非您没有替代方法，否则不应禁用此功能。 DEP 和 PAE 的默认设置对于大多数系统是最佳的。 请勿更改默认设置，除非它们干扰重要处理任务。 本部分包含的内容说明如何配置这些功能，但不应将其解释为更改默认设置的建议。

 

### <a name="span-iddep_and_pae_boot_parametersspanspan-iddep_and_pae_boot_parametersspandep-and-pae-boot-parameters"></a><span id="dep_and_pae_boot_parameters"></span><span id="DEP_AND_PAE_BOOT_PARAMETERS"></span>DEP 和 PAE 启动参数

在启动时启用 DEP 和 PAE，并通过使用[**BCDEdit/set**](./bcdedit--set.md)命令设置**nx**和**pae**参数的值进行配置。

这些启动参数具有冲突的影响。 若要配置 DEP 和 PAE，请仅使用每个参数的文档中描述的参数组合，并在本主题中进行讨论。 不要试验冲突参数，特别是在生产系统中。

### <a name="span-idthe_interaction_of_dep_and_pae_boot_parametersspanspan-idthe_interaction_of_dep_and_pae_boot_parametersspanthe-interaction-of-dep-and-pae-boot-parameters"></a><span id="the_interaction_of_dep_and_pae_boot_parameters"></span><span id="THE_INTERACTION_OF_DEP_AND_PAE_BOOT_PARAMETERS"></span>DEP 和 PAE 启动参数的交互

有两种类型的 DEP：

-   *硬件强制 dep* 为内核模式和用户模式进程启用 dep。 处理器和操作系统必须支持此方法。

<!-- -->

-   *软件强制 dep* 仅对用户模式进程启用 dep。 它必须受操作系统支持。

在32位版本的 Windows 上， *硬件强制 DEP* 需要 PAE，这受支持 DEP 的所有 Windows 操作系统支持。 如果在具有支持硬件强制 DEP 的处理器的计算机上启用 DEP，Windows 会自动启用 PAE，并忽略禁用它的启动参数值。

下一节对每个 Windows 操作系统的参数组合进行了总结。

### <a name="span-iddep_and_pae_parameter_combinationsspanspan-iddep_and_pae_parameter_combinationsspandep-and-pae-parameter-combinations"></a><span id="dep_and_pae_parameter_combinations"></span><span id="DEP_AND_PAE_PARAMETER_COMBINATIONS"></span>DEP 和 PAE 参数组合

以下列表描述了可用于配置 DEP 和 PAE 的启动参数组合。

**注意**   可选的 **{**<em>ID</em>**}** 是要配置的特定 Windows 启动加载程序启动项的 GUID。 如果未指定 **{**<em>ID</em>**}**，则该命令将修改当前的操作系统启动项。 有关详细信息，请参阅 [**BCDEdit/set**](./bcdedit--set.md) 命令。

 

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
<td align="left"><p><strong>启用 DEP</strong></p>
<p> (选择一个参数组合) </p>
<p>如果在支持硬件强制 DEP 的计算机上启用 DEP，则这些参数组合还会启用 PAE。</p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptIn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx 选择</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>在具有软件强制 DEP 的系统上启用 DEP 和 PAE</strong></p>
<p> (选择一个参数组合) </p>
<p>在支持硬件强制 DEP 的计算机上，当启用 DEP 时，将自动启用 PAE。</p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae 默认值</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptIn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae 默认值</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx 选择</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae 默认值</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>禁用 DEP 但启用 PAE</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceEnable</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>禁用 DEP 但启用 PAE</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceEnable</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>禁用 DEP 和 PAE</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceDisable</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>禁用 DEP 和 PAE</strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

