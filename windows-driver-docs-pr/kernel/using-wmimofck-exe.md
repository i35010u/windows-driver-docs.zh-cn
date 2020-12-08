---
title: 使用 Wmimofck.exe
description: 使用 Wmimofck.exe
keywords:
- WMI WDK 内核，Wmimofck.exe 实用工具
- Wmimofck.exe 实用工具
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e1eb88e06620fc4de75634a435449e7833ea04e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803725"
---
# <a name="using-wmimofckexe"></a>使用 Wmimofck.exe





Windows 驱动程序工具包附带 (WDK) 是 Wmimofck.exe 实用工具。 此应用程序会将二进制 MOF 文件作为输入 (在 [MOF 编译器](compiling-a-driver-s-mof-file.md) 生成的 bmf 文件)  ( # A0) 。 Wmimofck.exe 将检查在 bmf 文件中指定的类、属性、方法和事件对于 WMI 使用是否有效。 Wmimofck.exe 还可以生成以下文件：

-   C 语言头文件 ( .h 文件) 然后可用于使标头文件与 MOF 定义保持同步。

-   C 语言源文件，其中包含用于 WMI 驱动程序代码的存根。

-   Bmf 数据的 Hex 版本，可包含在驱动程序源中，以便在运行时提供动态 MOF 数据。

-   测试 VBScript 或 HTML 格式的应用程序模板。

若要运行 **wmimofck** 实用程序，请使用以下语法：

**wmimofck** \[**-h**_filename_ \[ **-m** \] \[ **-u** \] \] \[ **-c**_filename_ - \] \[ **x**_filename_ \] \[ **-t**_filename_ \] \[ **-w**_directory_ \] \[ *yfilename* \] \[ *-zfilename*\]

如果指定了 **-h** 参数，则将创建一个 C 语言标头文件，用于定义在 MOF 文件中指定的 guid、数据结构和方法索引。 如果调用方还指定了 **-m** 标志，则标头文件将包括每个 WMI 方法的输入和输出的结构定义。 默认情况下， *wmimofck* 不会为包含可变长度属性的 WMI 类生成成员定义。 如果调用方指定 **-u**，则 *wmimofck* 将为具有固定大小的每个属性生成成员定义，其中包括指定 **MaxLen** 限定符的字符串属性。 如果指定 **-t** 参数，则将创建一个 VBScript 程序，该程序将查询 MOF 文件中指定的所有数据块和属性。

如果指定 **-x** 参数，则将创建包含二进制 MOF 数据的文本表示形式的文本文件。 如果驱动程序支持通过 WMI 查询（而不是驱动程序映像文件上的资源）报告二进制 MOF，则可以将其包含在驱动程序源中。

如果指定了 **-c** 参数，则会生成一个 c 语言源文件，其中包含用于在设备驱动程序中实现 WMI 代码的模板。

如果指定 **-w** 参数，则将生成一组 HTML 文件，用于创建可用于访问 WMI 数据块的基本 UI。

**-Y** 和 **-z** 标志只能一起使用。 **-Y** 指定包含与语言无关的 WMI 类声明的文件， **-z** 为特定语言指定类修正。 命令 *wmimofck localizedfile* **-y**_mof_ **-z**_mfl_ 合并 *mof* 和 *mfl* 文件，形成 mof 文件的完整本地化版本。 有关详细信息，请参阅 [生成和部署本地化的 MOF 文件](building-and-deploying-the-localized-mof-file.md) 。

 

 




