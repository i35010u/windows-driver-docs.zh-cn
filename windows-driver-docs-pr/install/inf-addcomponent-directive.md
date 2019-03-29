---
title: INF AddComponent 指令
description: AddComponent 指令会创建下当前设备的软件组件设备。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 71e769c511b985f28a6a9494331e45edfaead520
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563889"
---
# <a name="inf-addcomponent-directive"></a>INF AddComponent 指令

**AddComponent**中使用指令[ **INF *DDInstall*。组件**](inf-ddinstall-components-section.md)一部分[扩展 INF 文件](using-an-extension-inf-file.md)。  它将创建当前设备下的软件组件的虚拟子设备。 适用于 Windows 10 版本 1703年及更高版本支持此指令。 

```ini
[DDInstall.Components]

AddComponent=ComponentName,[flags],component-install-section
```

## <a name="entries"></a>条目

*ComponentName*

指定要创建的软件组件的名称。  每个**AddComponent** INF 文件中的指令必须具有唯一值。

*flags*

指定一个或多个 （或运算） 标志，目前未定义的但保留供将来使用。

*component-install-section*

引用了一个 INF 编写器定义的部分，其中包含用于创建此设备的已命名的软件组件的信息。  

## <a name="remarks"></a>备注

每个 INF 编写器创建的部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。  有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

**AddComponent**指令必须引用一个已命名*组件安装部分*INF 文件中的其他位置。  每个此类部分具有以下形式：

```ini
[component-install-section]

ComponentIDs=component-id[,component-id] …
[Description=description]
```

每个*组件安装部分*必须具有至少**Componentid**条目如下所示。 但是，剩余的条目是可选的。

请注意， **Componentid**都[HardwareIDs](hardware-ids.md)，这意味着它们是由硬件开发人员定义的字符串。  若要确保唯一性的这些 Id，在大多数情况下，我们建议遵循有关标识符架构用于[PCI 设备](identifiers-for-pci-devices.md)。  可能的供应商可能想要使用不同的架构，但这取决于方案。

例如，使用单个设备上的多个组件的供应商可能想要使用的父对象关联的硬件组件的 Id。  在这种情况下，它们可以创建**ComponentID**通过将四个字符供应商定义的组件标识符附加到父级的硬件 ID。

## <a name="component-install-section-entries-and-values"></a>组件安装节条目和值
    
**ComponentIDs**=*id1[, id2] … [, idN]*

指定的软件组件的组件标识符。  组件 Id 的工作方式相同方式的硬件 Id 执行操作，并应遵循[类似的格式设置](hardware-ids.md)。 有关软件组件，系统前面添加的 INF 提供的值与`SWC\`创建硬件 Id。  例如， **Componentid**的值`VID0001&PID0001`结果中的硬件 ID `SWC\VID0001&PID0001`。

**描述**=*说明*

（可选） 指定一个字符串，描述软件组件，通常用于本地化，表示为 %strkey%令牌中定义[INF 字符串部分](inf-strings-section.md)。
    
如果描述字符串中包含任何 %strkey%令牌，每个标记可以表示 511 个字符最大值。 字符串的总后任何字符串令牌替换，不应超过 1024年个字符。

## <a name="see-also"></a>请参阅

[使用组件 INF 文件](using-a-component-inf-file.md)。

[*DDInstall*。**组件**](inf-ddinstall-components-section.md)

[INF AddSoftware 指令](inf-addsoftware-directive.md)
