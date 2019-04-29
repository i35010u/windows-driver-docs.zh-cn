---
title: 安装打印机类型的页面
description: 安装打印机类型的页面
ms.assetid: 6c878612-d490-4791-a284-c48f1db0cde8
keywords:
- 安装自定义打印网页 WDK
- 自定义打印网页 WDK，安装
- 特定于打印机的安装 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09d0e18e5b38f8469feecd934b0f6620a7b69ec0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366791"
---
# <a name="installing-pages-for-a-printer-type"></a>安装打印机类型的页面





如果与打印机一起使用的标准 TCP/IP 端口监视器，则可以安装特定于打印机类型的打印机详细信息页。 若要执行此操作，包括页面的 ASP 文件，以及 （如.gif 文件或链接的网页的 ASP 文件） 的所有从属文件中[打印机 INF 文件](printer-inf-files.md)打印机类型。 下面是示例部分中的打印机 INF 文件：

```cpp
[Manufacturer]
"ACME"
 
[ACME]
"ACME Mega Laser" = ACML01.PPD
 
[ACML01.PPD]
CopyFiles=@ACML01.PPD,PSCRIPT,ACML1WEB
DataSection=PSCRIPT_DATA
 
[ACML1WEB]
PAGE1.ASP, ACML1.ASP ;ACML1.ASP renamed to PAGE1.ASP during installation
ACML2.ASP
ACGF001.GIF
 
[DestinationDirs]
DefaultDestiDir=66000
ACML1WEB=66004
```

当打印机类安装程序遇到此 INF 文件部分时，它将执行以下操作：

-   创建格式化为一个目录&lt;根&gt;\\&lt;制造商&gt;\\&lt;打印机类型&gt;。 例如，应创建以下子目录：

    ..\\ACME\\ACME 庞大激光

-   将 Acml1.asp、 Asml2.asp 和 Acgf001.gif 复制到子目录中。

-   将 Acml1.asp 重命名为 Page1.asp （引起 ACML1WEB 部分中的第一个语句）。

请注意，必须识别第一个 ASP 文件，您可以通过在行前 Page1.asp 文件名称，如示例所示。 安装程序将重命名此文件为 Page1.asp 目标目录中。

所有 ASP 文件的名称格式为页*N*.asp，其中*N*是 1、 2、 3，依此类推，microsoft 保留。

示例 INF 文件随附[示例 ASP 文件](sample-asp-files.md)Windows 驱动程序工具包中。

 

 




