---
title: Unidrv 组件
description: Unidrv 组件
ms.assetid: 358eed9e-05e3-4670-b6b1-d5413c46edf0
keywords:
- Unidrv 组件
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c6f418e7853cf03eadb19feb0fb07438128c872
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370409"
---
# <a name="unidrv-components"></a>Unidrv 组件





Unidrv 组件中包含的 Dll，以及文本和二进制数据文件，如以下关系图中所示：

![说明如何 unidrv 组件中包含的 dll，以及文本和二进制数据文件的关系图](images/unidrvcm.png)

在关系图中的组件包括：

<a href="" id="application"></a>**Application**  
用户应用程序，如字处理器，该用户提供打印功能。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
导出 Win32 GDI 函数的用户模式 DLL。

<a href="" id="kernel-mode-graphics-engine-------"></a>内核模式图形引擎   
NT 实现 GDI 功能的执行代码。

<a href="" id="minidriver-text-files"></a>**微型驱动程序的文本文件**  
基于文本的[Unidrv 微型驱动程序](unidrv-minidrivers.md)通过使用描述打印机[GPD 文件条目](gpd-file-entries.md)。

<a href="" id="binary-data-files"></a>**二进制数据文件**  
临时文件 （扩展名为.bud） Unidrv 分析包含在微型驱动程序的文本文件中的信息之后创建的。

<a href="" id="unidrvui-dll"></a>**unidrvui.dll**  
[Unidrv 用户界面](unidrv-user-interface.md)DLL，为所有 Unidrv 支持打印机提供的常见 UI 代码。

<a href="" id="user-interface-plug-in"></a>**插件的用户界面**  
可选的打印机特定[插件的用户界面](user-interface-plug-ins.md)。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md)打印机用户界面。

<a href="" id="unidrv-dll"></a>**unidrv.dll**  
[Unidrv 呈现器](unidrv-renderer.md)，其呈现图像并将图像数据流发送到打印后台处理程序。

<a href="" id="rendering-plug-in"></a>**呈现插件**  
可选的打印机特定[呈现插件](rendering-plug-ins.md)。

 

 




