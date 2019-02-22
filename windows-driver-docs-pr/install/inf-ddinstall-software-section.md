---
title: INF DDInstall.Software 部分
description: DDInstall.Software 部分包含一个或多个引用的软件组件 INF 文件中的其他 INF 编写器定义部分的 INF AddSoftware 指令。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 834120ca5ae4fc2c96f1e0f7ea0d30ffafe36340
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554196"
---
# <a name="inf-ddinstallsoftware-section"></a>INF DDInstall.Software 部分

每个每个模型*DDInstall*。**软件**部分包含一个或多个[ **INF AddSoftware 指令**](inf-addsoftware-directive.md)引用的软件组件 INF 文件中的其他 INF 编写器定义部分。  本部分被支持 Windows 10 版本 1703年及更高版本。

```ini
[install-section-name.Software] |
[install-section-name.nt.Software] |
[install-section-name.ntx86.Software] |
[install-section-name.ntia64.Software] |
[install-section-name.ntamd64.Software] |
[install-section-name.ntarm.Software] |
[install-section-name.ntarm64.Software]
 
AddSoftware=SoftwareName,[flags],software-install-section
```

你可以提供*DDInstall*。**软件**上至少有一个部分[AddSoftware 指令](inf-addsoftware-directive.md)从软件组件安装软件。

软件安装必须为非交互式。

## <a name="entries"></a>条目

**AddSoftware**=*SoftwareName,[flags],software-install-section*

此指令引用 INF 编写器的定义*软件安装部分*软件组件 INF 文件中的其他位置。  有关详细信息，请参阅[ **INF AddSoftware 指令**](inf-addsoftware-directive.md)。

## <a name="remarks"></a>备注

*DDInstall*。**软件**部分应具有其相关的相同平台和操作系统修饰*DDInstall*部分。  例如，*安装的部分名称*。**ntx86**部分中将具有相应*安装的部分名称*。**ntx86。软件**部分。
    
指定*DDInstall*部分必须在每个制造商下的特定于设备/模型的项中引用*模型*INF 文件部分。 不区分大小写的扩展*安装的部分名称*所示在正式语法语句可插入到此类<em>DDInstall</em>**。软件**跨平台 INF 文件中的节名称。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

## <a name="examples"></a>示例

```ini
[ContosoCtrlPnl.NT.Software]
AddSoftware = ContosoGrfx1CtrlPnl,, Software_Inst

[Software_Inst]
SoftwareType = 1
SoftwareBinary =  %13%\ContosoCtrlPnl.exe
SoftwareArguments = <<DeviceInstanceID>>
SoftwareVersion = 1.0.0.0
```

## <a name="see-also"></a>另请参阅

[使用组件 INF 文件](using-a-component-inf-file.md)。

[INF AddSoftware 指令](inf-addsoftware-directive.md)
