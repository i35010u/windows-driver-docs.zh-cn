---
title: 安装约束
description: 安装约束
ms.assetid: 0adf5a6a-e9de-4bb0-bf1c-fe7eef565840
keywords:
- 安装 WDK Unidrv 约束
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6f31b8c5a1022a5ed0498f65b9f277068e59ea4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362768"
---
# <a name="installation-constraints"></a>安装约束





有时，不能同时安装某些可安装的打印机选项。 例如，它可能无法安装信封进纸器和进行双面打印单元。

若要指定不能同时安装的打印机选项的组合，请使用\*InvalidInstallableCombination 条目。

\*InvalidInstallableCombination 条目采用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* InvalidInstallableCombination:列表 (</strong><em>FeatureName</em> <strong>。</strong> <em>OptionName</em><strong>，</strong> <em>FeatureName</em> <strong>。</strong> <em>OptionName</em><strong>,</strong> ...<strong>)</strong></p></td>
</tr>
</tbody>
</table>

 

其中*FeatureName*是一项功能的名称和*OptionName*与功能相关联的选项的名称。 此列表可能在这种情况下包括功能以及所选项，段和*OptionName*不包括在内。

在单个的功能和选项列出\*InvalidInstallableCombination 条目指示一系列功能和不能结合使用的选项。 例如，以下项指定，不能同时安装信封进纸器和进行双面打印单元。

```cpp
*InvalidInstallableCombination: LIST(InputBin.ENVFEED, Duplex)
```

所有\*InvalidInstallationCombination 条目必须位于 GPD 文件的根级别 (即，不在大括号内)。 功能和项中包含的选项数不受限制。

如果某项功能或选项包含在\*InvalidInstallationCombination 条目，功能或选项的\*可安装？ 属性必须设置为**TRUE**。

 

 




