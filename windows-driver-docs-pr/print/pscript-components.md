---
title: Pscript 组件
description: Pscript 组件
ms.assetid: 9f3bd004-e62c-42b6-99da-045c12e088a3
keywords:
- PostScript 打印机驱动程序 WDK 打印，组件
- Pscript WDK 打印，组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93d4b7640cb477f254c967766dff0fe8251f255f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376604"
---
# <a name="pscript-components"></a>Pscript 组件





Pscript 组件中包含的 Dll，以及文本和二进制数据文件，如以下关系图中所示：

![说明该 pscript 组件的关系图包含的 dll 和文本和二进制数据文件](images/pscript5.png)

在关系图中的组件包括：

<a href="" id="application"></a>**Application**  
用户应用程序，如字处理器，该用户提供打印功能。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
导出 Win32 GDI 函数的用户模式 DLL。

<a href="" id="kernel-mode-graphics-engine"></a>**内核模式图形引擎**  
实现 GDI 功能的基于 NT 的操作系统执行代码。

<a href="" id="minidriver-text-files"></a>**微型驱动程序的文本文件**  
基于文本的 Pscript 微型驱动程序文件。

<a href="" id="binary-data-files"></a>**二进制数据文件**  
临时文件 （扩展名为.bpd） Pscript 分析包含在微型驱动程序的文本文件中的信息之后创建的。

<a href="" id="ps5ui-dll"></a>**ps5ui.dll**  
[Pscript 用户界面](pscript-user-interface.md)DLL，为所有 Pscript 支持打印机提供的常见 UI 代码。

<a href="" id="user-interface-plug-in"></a>**插件的用户界面**  
可选的打印机特定[插件的用户界面](user-interface-plug-ins.md)。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md)打印机用户界面。

<a href="" id="pscript5-dll"></a>**pscript5.dll**  
[Pscript 呈现器](pscript-renderer.md)，处理文本输出和呈现图像，然后将文本和图像数据发送到打印后台处理程序。

<a href="" id="rendering-plug-in"></a>**呈现插件**  
可选的打印机特定[呈现插件](rendering-plug-ins.md)。

 

 




