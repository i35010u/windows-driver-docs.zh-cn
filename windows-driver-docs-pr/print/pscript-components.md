---
title: Pscript 组件
description: Pscript 组件
keywords:
- PostScript 打印机驱动程序 WDK 打印，组件
- Pscript WDK 打印，组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3eb85b35733b35915496d62eb55a9da905ba188
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807167"
---
# <a name="pscript-components"></a>Pscript 组件





Pscript 组件由 Dll、文本和二进制数据文件组成，如下图所示：

![说明 pscript 组件由 dll、文本和二进制数据文件组成的关系图](images/pscript5.png)

关系图中的组件包括：

<a href="" id="application"></a>**程序**  
为用户提供打印功能的用户应用程序，如文字处理器。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
导出 Win32 GDI 函数的用户模式 DLL。

<a href="" id="kernel-mode-graphics-engine"></a>**内核模式图形引擎**  
用于实现 GDI 功能的基于 NT 的操作系统执行代码。

<a href="" id="minidriver-text-files"></a>**微型驱动程序文本文件**  
使用 *PPD* 文件创建的基于文本的 [Pscript 微型驱动程序](pscript-minidrivers.md)。

<a href="" id="binary-data-files"></a>**二进制数据文件**  
临时文件 (的文件) 扩展名为 bpd，Pscript 在分析微型驱动程序文本文件中包含的信息之后创建。

<a href="" id="ps5ui-dll"></a>**ps5ui.dll**  
[Pscript 用户界面](pscript-user-interface.md) DLL，为所有支持 Pscript 的打印机提供通用的 UI 代码。

<a href="" id="user-interface-plug-in"></a>**用户界面插件**  
可选的、特定于打印机的 [用户界面插件](user-interface-plug-ins.md)。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md) 用于打印机的用户界面。

<a href="" id="pscript5-dll"></a>**pscript5.dll**  
[Pscript 呈现](pscript-renderer.md)器，用于处理文本输出和呈现图像，然后将文本和图像数据发送到打印后台处理程序。

<a href="" id="rendering-plug-in"></a>**呈现插件**  
可选的、特定于打印机的、 [呈现插件](rendering-plug-ins.md)。

 

 




