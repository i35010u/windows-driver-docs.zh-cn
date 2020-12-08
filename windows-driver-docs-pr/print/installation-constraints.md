---
title: 安装约束
description: 安装约束
keywords:
- 安装约束 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44411205fce2c7d98b372055d2e3d9572a952822
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835691"
---
# <a name="installation-constraints"></a>安装约束





有时，某些可安装的打印机选项不能同时安装。 例如，可能无法安装信封进纸器和双面打印单元。

若要指定不能同时安装的打印机选项组合，请使用 \* InvalidInstallableCombination 项。

\*InvalidInstallableCombination 条目采用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* InvalidInstallableCombination：列出 (功能列表</strong> <em>FeatureName</em> <strong>。</strong> <em>OptionName</em><strong>，</strong> <em>FeatureName</em>功能名<strong>。</strong> <em>OptionName</em><strong>，</strong> .。。<strong>) </strong></p></td>
</tr>
</tbody>
</table>

 

其中，"功能名称" 是功能的名称，" *OptionName* *" 是与* 该功能关联的选项的名称。 此列表可以包含功能以及选项，在这种情况下，不包括句点和 *OptionName* 。

单个 InvalidInstallableCombination 条目中列出的功能和选项 \* 指示不能组合使用的一组功能和选项。 例如，以下条目指定无法同时安装信封进纸器和双面打印单元。

```cpp
*InvalidInstallableCombination: LIST(InputBin.ENVFEED, Duplex)
```

所有 \* InvalidInstallationCombination 条目都必须位于 GPD 文件的根级别 (即，不在大括号) 内。 条目中包含的功能和选项的数目不受限制。

如果某个功能或选项包含在 \* InvalidInstallationCombination 项中，则功能或选项的 \* 可安装？特性必须设置为 **TRUE**。

 

 




