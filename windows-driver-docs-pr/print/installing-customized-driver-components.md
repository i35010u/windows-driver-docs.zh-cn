---
title: 安装自定义的驱动程序组件
description: 安装自定义的驱动程序组件
ms.assetid: 88f189bd-97f5-4bc6-ba3e-3d9da18e2102
keywords:
- 自定义 WDK、 安装组件的打印机驱动程序
- 自定义打印机驱动程序 WDK、 安装组件
- 安装自定义打印机驱动程序组件 WDK
- INF 文件 WDK 打印、 自定义驱动程序组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0e2c9c35a053b92a8e941e843a955f91334bc6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385971"
---
# <a name="installing-customized-driver-components"></a>安装自定义的驱动程序组件





当你对 Microsoft 的打印机驱动程序提供自定义的组件时，还必须提供用于安装的组件的.ini 文件。 (如果 ntprint.inf 不支持您的打印机，还必须提供[打印机 INF 文件](printer-inf-files.md)。)

.Ini 文件必须包含 OEMFiles 部分。 在本部分中，使用以下项之一描述每个自定义的组件：

<a href="" id="oemdriverfilen"></a>OEMDriverFile*n*  
命名插件的呈现。

<a href="" id="oemconfigfilen"></a>OEMConfigFile*n*  
命名插件的用户界面。

其中*n*指定在其中安装程序安装文件的顺序。 为指定的数字*n*必须是连续的以两种类型的插件 1 开始。

例如，如果你要提供两个呈现插件和插件，一个用户界面和您的打印机型号是 XYZ，您的.ini 文件可能会出现，如下所示：

```cpp
[OEMFiles]
OEMDriverFile1=XYZDRV1.DLL
OEMConfigFile1=XYZUI1.DLL
OEMDriverFile2=XYZDRV2.DLL
```

之前或之后等号 （=） 不允许有空格。 文件的名称不能包含路径规范。

在示例中，指定两个呈现插件。 基于*n*值 OEMDriverFile*n*，xyzdrv1.dll xyzdrv2.dll 之前确保已安装。 Unidrv 和 Pscript5 驱动程序时将其安装，因此更高版本，驱动程序需要调用图形 DDI 的顺序调用插件挂钩函数和由这些插件提供的 COM 方法，xyzdrv1.dll 之前，将调用 xyzdrv2.dll。

.Ini 文件名称应反映打印机产品名称。 .Ini 文件名称应为不同于其他打印机，以避免名称冲突的.ini 文件的名称。 请注意，是否要将后的迁移插件呈现或插件，Windows NT 4.0 的用户界面，您的.ini 文件名称必须匹配你.gpd 或.ppd 的文件名称。 （即，xyz.ini 必须用于 xyz.gpd 或 xyz.ppd。）此限制不适用于 Windows 2000 或更高版本的 Windows 操作系统。

在.ini 文件可以包含 ANSI 或 Unicode 文本，但建议使用 Unicode 文本。 在.ini 文件中，行开头的井号 (\#) 条评论。

有关详细信息，请参阅[INF 文件的一般准则](https://docs.microsoft.com/windows-hardware/drivers/install/general-guidelines-for-inf-files)并[安装 Unidrv 微型驱动程序](installing-a-unidrv-minidriver.md)。

如果你提供打印机 INF 文件，方便地安装和注册自定义的组件是使组件*依赖文件*的打印机驱动程序。 此外，可以作为依赖文件安装关联的.inf 文件。 有关对打印机驱动程序的依赖文件的详细信息，请参阅[打印机 INF 文件条目](printer-inf-file-entries.md)。

或者，可以通过该组件用于如端口监视器或状态应用程序的另一个打印组件的依赖文件来安装自定义的组件。 但是，此方法可能会创建困难，因为[点--打印](introduction-to-point-and-print.md)操作安装的驱动程序和驱动程序相关的客户端上的文件。 如果未作为打印机驱动程序的依赖文件列出自定义的组件，必须以点--打印操作的一部分以外的其他某种方式在客户端上安装组件。

 

 




