---
title: 安装自定义的驱动程序组件
description: 安装自定义的驱动程序组件
ms.assetid: 88f189bd-97f5-4bc6-ba3e-3d9da18e2102
keywords:
- 打印机驱动程序自定义 WDK，安装组件
- 自定义打印机驱动程序 WDK，安装组件
- 安装自定义打印机驱动程序组件 WDK
- INF 文件 WDK 打印，自定义驱动程序组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d4922070b54540cad1e482d17915172ca744e2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210597"
---
# <a name="installing-customized-driver-components"></a>安装自定义的驱动程序组件





为 Microsoft 的打印机驱动程序提供自定义组件时，还必须提供用于安装该组件的 .ini 文件。  (如果 ntprint.inf 不支持打印机，还必须提供 [打印机 inf 文件](printer-inf-files.md)。 ) 

.Ini 文件必须包含 OEMFiles 部分。 在本部分中，将使用以下条目之一描述每个自定义组件：

<a href="" id="oemdriverfilen"></a>OEMDriverFile*n*  
命名呈现插件。

<a href="" id="oemconfigfilen"></a>OEMConfigFile*n*  
命名用户界面插件。

其中 *n* 指定安装程序安装文件的顺序。 对于这两种类型的插件，为 *n* 指定的数字必须是连续的（从1开始）。

例如，如果您提供两个呈现插件和一个用户界面插件，并且您的打印机型号是 XYZ，则您的 .ini 文件可能如下所示：

```cpp
[OEMFiles]
OEMDriverFile1=XYZDRV1.DLL
OEMConfigFile1=XYZUI1.DLL
OEMDriverFile2=XYZDRV2.DLL
```

在等号 (=) 之前或之后不允许使用空格。 文件名不能包含路径规范。

在此示例中，指定了两个呈现插件。 根据 OEMDriverFile*n*的*n*值，在 xyzdrv2.dll 之前安装 xyzdrv1.dll。 Unidrv 和 Pscript5 驱动程序会按照其安装顺序调用插件，因此，以后当驱动程序需要调用图形 DDI 挂钩函数和这些插件提供的 COM 方法时，将在 xyzdrv2.dll 之前调用 xyzdrv1.dll。

.Ini 文件名应反映打印机产品名称。 .Ini 文件名应与其他打印机的 .ini 文件名称不同，以避免名称冲突。 请注意，如果你要将呈现插件或用户界面插件反向移植到 Windows NT 4.0，则你的 .ini 文件名必须与你的 gpd 或 ppd 文件名匹配。  (即，xyz.ini 必须用于 gpd 或 xyz。 ) 此限制不适用于 Windows 2000 或更高版本的 Windows 操作系统。

一个 .ini 文件可以包含 ANSI 或 Unicode 文本，但建议使用 Unicode 文本。 在 .ini 文件中，以井号开始的行 (\#) 是注释。

有关详细信息，请参阅 INF 文件和[安装 Unidrv 微型驱动程序](installing-a-unidrv-minidriver.md)的[一般准则](../install/general-guidelines-for-inf-files.md)。

如果提供打印机 INF 文件，安装和注册自定义组件的一种简便方法是使该组件成为打印机驱动程序的 *相关文件* 。 此外，可以将关联的 .inf 文件作为依赖文件安装。 有关打印机驱动程序的依赖文件的详细信息，请参阅 [打印机 INF 文件条目](printer-inf-file-entries.md)。

或者，你可以通过使组件成为另一个打印组件（例如端口监视器或状态应用程序）的依赖文件来安装自定义组件。 但是，此方法可能会导致出现问题，因为 [点和打印](introduction-to-point-and-print.md) 操作仅在客户端上安装与驱动程序和驱动程序相关的文件。 如果自定义组件未作为打印机驱动程序的相关文件列出，则必须以某种方式在客户端上安装该组件，而不是作为 "点和打印" 操作的一部分进行安装。

 

