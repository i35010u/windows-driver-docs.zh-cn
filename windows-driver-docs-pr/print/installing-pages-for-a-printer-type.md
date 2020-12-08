---
title: 安装打印机类型的页面
description: 安装打印机类型的页面
keywords:
- 安装自定义的打印网页 WDK
- 自定义的打印网页 WDK，安装
- 特定于打印机的安装 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b256054456f6cfa83679672bd678912c6387b707
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796699"
---
# <a name="installing-pages-for-a-printer-type"></a>安装打印机类型的页面





如果打印机使用的是标准 TCP/IP 端口监视器，则可以安装特定于打印机类型的打印机详细信息页。 为此，请在打印机类型的 [打印机 INF 文件](printer-inf-files.md) 中包含该页的 ASP 文件以及所有从属文件 (如用于链接页的 .gif 文件或 ASP 文件) 。 下面是打印机 INF 文件的示例部分：

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

-   创建设置为 " &lt; 根 &gt; \\ &lt; 制造商 &gt; \\ &lt; 打印机类型 &gt; " 的目录。 在此示例中，将创建以下子目录：

    ..\\ACME \\ Acme 万像素激光

-   将 Acml1、Asml2 和 Acgf001.gif 复制到子目录中。

-   将 Acml1 重命名为 ACML1WEB) 部分中的第一个语句导致的 Page1 (。

请注意，你必须通过在第一个 ASP 文件的前面加上 Page1 文件名称来确定要查看的第一个 ASP 文件，如示例中所示。 安装程序将此文件重命名为目标目录中的 Page1。

Microsoft 保留所有格式为 Page *n.*.ASP 的 asp 文件名，其中 *N* 为1、2、3等。

示例 INF 文件随 Windows 驱动程序工具包中的 [示例 ASP 文件](sample-asp-files.md) 一起提供。

 

 




