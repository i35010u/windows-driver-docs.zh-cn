---
title: INF DDInstall.Software 节
description: DDInstall 部分包含一个或多个 INF AddSoftware 指令，这些指令引用软件组件 INF 文件中其他由 INF 编写器定义的部分。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a942b1f394261f106a63363c8bb3da61b1046610
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223221"
---
# <a name="inf-ddinstallsoftware-section"></a>INF DDInstall.Software 节

每个模型*DDInstall*。**Software**节包含一个或多个[**inf AddSoftware 指令**](inf-addsoftware-directive.md)，这些指令引用软件组件 INF 文件中其他由 INF 编写器定义的部分。  Windows 10 版本1703及更高版本支持此部分。

```inf
[install-section-name.Software] |
[install-section-name.nt.Software] |
[install-section-name.ntx86.Software] |
[install-section-name.ntia64.Software] |
[install-section-name.ntamd64.Software] |
[install-section-name.ntarm.Software] |
[install-section-name.ntarm64.Software]
 
AddSoftware=SoftwareName,[flags],software-install-section
```

可以提供*DDInstall*。包含至少一个[AddSoftware 指令](inf-addsoftware-directive.md)以从软件组件安装软件的**软件**部分。

软件安装必须为非交互式。

## <a name="entries"></a>条目

**AddSoftware**=*SoftwareName，[flags]，software-安装节*

此指令在软件组件 INF 文件中的其他位置引用一个由 INF 编写器定义的*软件安装部分*。  有关详细信息，请参阅[**INF AddSoftware 指令**](inf-addsoftware-directive.md)。

## <a name="remarks"></a>备注

*DDInstall*。**软件**部分应该与相关的*DDInstall*部分具有相同的平台和操作系统修饰。  例如，*安装--名称*。**ntx86**部分会有一个相应的*安装节名称*。**ntx86。软件**部分。
    
在 INF 文件的 "每制造商"*型号*部分下，必须在特定于设备/模型的条目中引用指定的*DDInstall*部分。 在正式语法语句中显示的*安装节名称*不区分大小写的扩展可以插入到此类<em>DDInstall</em>中 **。** 跨平台 INF 文件中的软件分区名称。

有关如何使用**系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm**和**Ntarm64**扩展的详细信息，请参阅[为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

## <a name="examples"></a>示例

```inf
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
