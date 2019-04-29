---
title: 使用 Wmimofck.exe
description: 使用 Wmimofck.exe
ms.assetid: cbf735c4-1c0d-4ff3-8a5c-b9d1de84bca4
keywords:
- WMI WDK 内核，Wmimofck.exe 实用程序
- Wmimofck.exe 实用程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1733c154eb9cd68e167d352bd414149c73315412
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363101"
---
# <a name="using-wmimofckexe"></a>使用 Wmimofck.exe





包含使用 Windows Driver Kit (WDK) 是 Wmimofck.exe 实用程序。 此应用程序将作为输入二进制的 MOF 文件 (.bmf file)，这由生成[MOF 编译器](compiling-a-driver-s-mof-file.md)(mofcomp.exe)。 Wmimofck.exe 将检查的类、 属性、 方法和事件.bmf 文件中指定它们可用于 WMI。 Wmimofck.exe 也是能够生成以下文件：

-   C 语言头文件 （.h 文件），然后可用于使标头文件与 MOF 定义保持同步。

-   C 语言源文件包含 WMI 驱动程序代码的存根。

-   十六进制.bmf 数据可以提供动态 MOF 数据在运行时的驱动程序源中包含的版本。

-   在 VBScript 或 HTML 中测试应用程序模板。

若要运行**wmimofck**实用程序，请使用以下语法：

**wmimofck** \[  **-h * * * filename* \[ **-m** \] \[ **-u** \] \] \[* *-c * * * 文件名*\] \[ **-x * **filename* \] \[** -t***文件名 *\] \[* *-w***目录*\] \[* -yfilename*\] \[*-zfilename *\]

如果 **-h**指定参数，用于定义 Guid、 数据结构和 MOF 文件中指定的方法索引创建 C 语言头文件。 如果调用方指定 **-m**标志，则标头文件会包含输入和输出的每个 WMI 方法的结构定义。 默认情况下*wmimofck*不会生成包含可变长度属性的 WMI 类的成员定义。 如果调用方指定 **-u**，然后*wmimofck*将生成具有固定的大小，包括字符串属性指定的每个属性的成员定义**MaxLen**限定符。 如果 **-t**指定参数时，VBScript 程序将创建一个将查询所有数据块和 MOF 文件中指定的属性。

如果 **-x**指定参数创建一个文本文件，其中包含的文本表示形式的二进制 MOF 数据。 这可以包括在驱动程序源中如果驱动程序支持报告通过 WMI 查询而不是上的驱动程序图像文件的资源的二进制 MOF。

如果 **-c**指定参数时，会生成包含一个模板，用于在设备驱动程序中实现的 WMI 代码 C 语言源文件。

如果 **-w**指定参数，则会生成一组 HTML 文件，该创建可用于访问 WMI 数据块的基本 UI。

**-Y**并**z**标志只能在一起。 **-Y**指定包含独立于语言的 WMI 类声明中，文件和**z**指定某个特定的语言类修正。 该命令*wmimofck localizedfile* **-y * * * mof* **-z * * * mfl*合并*mof*和*mfl*文件以形成完整的本地化的版本的 MOF 文件。 请参阅[构建和部署本地化 MOF 文件](building-and-deploying-the-localized-mof-file.md)有关详细信息。

 

 




