---
title: INF AddComponent 指令
description: AddComponent 指令在当前设备下创建软件组件设备。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 758f80d1d19bb9830b16254d409b9df20ec1cb54
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223201"
---
# <a name="inf-addcomponent-directive"></a>INF AddComponent 指令

在 INF DDInstall 中使用**AddComponent**指令[**。 *DDInstall***](inf-ddinstall-components-section.md)[扩展 INF 文件](using-an-extension-inf-file.md)的 "组件" 部分。  它在当前设备下为软件组件创建虚拟子设备。 Windows 10 版本1703及更高版本支持此指令。 

```inf
[DDInstall.Components]

AddComponent=ComponentName,[flags],component-install-section
```

## <a name="entries"></a>条目

*ComponentName*

指定要创建的软件组件的名称。  INF 文件中的每个**AddComponent**指令必须具有唯一的值。

*flag*

指定一个或多个（运算）标志，当前未定义，但保留供将来使用。

*组件安装-部分*

引用由 INF 写入方定义的部分，其中包含为此设备创建命名软件组件的信息。  

## <a name="remarks"></a>备注

在 INF 文件中，每个 INF 编写器创建的节名称必须唯一，并且必须遵循用于定义节名称的常规规则。  有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

**AddComponent**指令必须在 INF 文件中的其他位置引用命名*组件安装部分*。  每个此类部分都具有以下形式：

```inf
[component-install-section]

ComponentIDs=component-id[,component-id] …
[Description=description]
```

每个*组件安装部分*必须至少具有**componentid**条目，如下所示。 但是，其余条目是可选的。

请注意， **componentid**是[HardwareIDs](hardware-ids.md)，这意味着它们是由硬件开发人员定义的字符串。  为了确保这些 Id 的唯一性，在大多数情况下，我们建议遵循用于[PCI 设备](identifiers-for-pci-devices.md)的标识符架构。  供应商可能想要使用不同的架构，但这取决于方案。

例如，在单个设备上具有多个组件的供应商可能想要将该组件的硬件 Id 与父对象相关联。  在这种情况下，他们可以通过将由四个字符组成的供应商定义的组件标识符追加到父级的硬件**ID 来创建一个组件**id。

## <a name="component-install-section-entries-and-values"></a>组件-安装节项和值
    
**Componentid**=*id1 [，id2] .。。[，idN]*

指定软件组件的组件标识符。  组件 Id 的工作方式与硬件 Id 的工作方式相同，并且应遵循[类似的格式设置](hardware-ids.md)。 对于软件组件，系统会在前面加`SWC\`上 INF 提供的值，以创建硬件 id。  例如，的**componentid**值为的`VID0001&PID0001`硬件 ID `SWC\VID0001&PID0001`。

**说明**=*描述*

（可选）指定描述软件组件的字符串，通常用于本地化，表示为在[INF 字符串部分](inf-strings-section.md)中定义的% strkey% 令牌。
    
如果说明字符串包含任何% strkey% 令牌，则每个令牌最多可以表示511个字符。 所有字符串标记替换后的总字符串不应超过1024个字符。

## <a name="see-also"></a>另请参阅

[使用组件 INF 文件](using-a-component-inf-file.md)。

[*DDInstall*。**组件**](inf-ddinstall-components-section.md)

[INF AddSoftware 指令](inf-addsoftware-directive.md)
