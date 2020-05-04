---
title: INF DDInstall.Components 节
description: DDInstall 部分包含一个或多个 INF AddComponent 指令，这些指令引用驱动程序包 INF 文件中其他由 INF 编写器定义的部分。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26b6169180d49a7d1a43d0eedacbe79a54758c1d
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223257"
---
# <a name="inf-ddinstallcomponents-section"></a>INF DDInstall.Components 节

此可选部分包含一个或多个[**Inf AddComponent 指令**](inf-addcomponent-directive.md)，这些指令引用驱动程序包 inf 文件中其他由 INF 编写器定义的部分。  Windows 10 版本1703及更高版本支持此部分。

```inf
[install-section-name.Components] |
[install-section-name.nt.Components] |
[install-section-name.ntx86.Components] |
[install-section-name.ntia64.Components] |
[install-section-name.ntamd64.Components] |
[install-section-name.ntarm.Components] |
[install-section-name.ntarm64.Components] |
 
AddComponent=ComponentName,[flags],component-install-section
```

可以提供*DDInstall*。使用一个或多个**AddComponent**指令创建驱动程序包和任意数量软件组件之间的符号关系的**组件**部分。

## <a name="entries"></a>条目

**AddComponent**=*ComponentName，[flags]，组件安装-部分*

此指令在 INF 文件中的其他位置引用由 INF 编写器定义的 DDInstall 节，其中包含此*DDInstall*部分涵盖的设备的驱动程序。  有关详细信息，请参阅[**INF AddComponent 指令**](inf-addcomponent-directive.md)。

## <a name="remarks"></a>备注

*DDInstall*。**组件**部分应该与相关的*DDInstall*部分具有相同的平台和操作系统修饰。  例如，*安装--名称*。**ntx86**部分会有一个相应的*安装节名称*。**ntx86**部分。

在 INF 文件的 "每制造商"*型号*部分下，必须在特定于设备/模型的条目中引用指定的*DDInstall*部分。  在正式语法语句中显示的*安装节名称*不区分大小写的扩展可以插入到此类*DDInstall*中。跨平台 INF 文件中的**组件**部分名称。

有关如何使用**系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm**和**Ntarm64**扩展的详细信息，请参阅[为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

## <a name="examples"></a>示例

```inf
[ContosoGrfx.NT.Components]
AddComponent = ContosoControlPanel,,Component_Inst

[Component_Inst]
ComponentIDs = VID0001&PID0001&SID0001
DisplayName = %ContosoControlPanelDisplayName%
```

## <a name="see-also"></a>另请参阅

[使用组件 INF 文件](using-a-component-inf-file.md)

[INF AddComponent 指令](inf-addcomponent-directive.md)
