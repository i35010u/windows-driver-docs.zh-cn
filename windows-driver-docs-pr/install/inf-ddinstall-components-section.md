---
title: INF DDInstall.Components 部分
description: DDInstall.Components 部分包含一个或多个 INF AddComponent 指令引用驱动程序包 INF 文件中的其他 INF 编写器定义部分。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7aadabb3e1d97e76e18196290a20eb37a87278f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525015"
---
# <a name="inf-ddinstallcomponents-section"></a>INF DDInstall.Components 部分

此可选部分包含一个或多个[ **INF AddComponent 指令**](inf-addcomponent-directive.md)引用驱动程序包 INF 文件中的其他 INF 编写器定义部分。  本部分被支持 Windows 10 版本 1703年及更高版本。

```ini
[install-section-name.Components] |
[install-section-name.nt.Components] |
[install-section-name.ntx86.Components] |
[install-section-name.ntia64.Components] |
[install-section-name.ntamd64.Components] |
[install-section-name.ntarm.Components] |
[install-section-name.ntarm64.Components] |
 
AddComponent=ComponentName,[flags],component-install-section
```

你可以提供*DDInstall*。**组件**与一个或多部分**AddComponent**指令来创建驱动程序包和任意数量的软件组件之间的符号关系。

## <a name="entries"></a>条目

**AddComponent**=*ComponentName,[flags],component-install-section*

此指令引用 INF 编写器定义组件的安装-部分涵盖此设备的驱动程序的 INF 文件中的其他位置*DDInstall*部分。  有关详细信息，请参阅[ **INF AddComponent 指令**](inf-addcomponent-directive.md)。

## <a name="remarks"></a>备注

*DDInstall*。**组件**部分应具有其相关的相同平台和操作系统修饰*DDInstall*部分。  例如，*安装的部分名称*。**ntx86**部分中将具有相应*安装的部分名称*。**ntx86.Components**部分。

指定*DDInstall*部分必须在每个制造商下的特定于设备/模型的项中引用*模型*INF 文件部分。  不区分大小写的扩展*安装的部分名称*所示在正式语法语句可插入到此类*DDInstall*。**组件**跨平台 INF 文件中的节名称。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

## <a name="examples"></a>示例

```ini
[ContosoGrfx.NT.Components]
AddComponent = ContosoControlPanel,,Component_Inst

[Component_Inst]
ComponentIDs = VID0001&PID0001&SID0001
DisplayName = %ContosoControlPanelDisplayName%
```

## <a name="see-also"></a>另请参阅

[使用组件 INF 文件](using-a-component-inf-file.md)

[INF AddComponent 指令](inf-addcomponent-directive.md)
