---
title: Unidrv 组件
description: Unidrv 组件
keywords:
- Unidrv，组件
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abb841f2057e3c484e6ad0d63355dc2c74e81f54
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802229"
---
# <a name="unidrv-components"></a>Unidrv 组件





Unidrv 组件由 Dll、文本和二进制数据文件组成，如下图所示：

![阐释 unidrv 组件如何包含 dll 的关系图，以及文本和二进制数据文件](images/unidrvcm.png)

关系图中的组件包括：

<a href="" id="application"></a>**程序**  
为用户提供打印功能的用户应用程序，如文字处理器。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
导出 Win32 GDI 函数的用户模式 DLL。

<a href="" id="kernel-mode-graphics-engine-------"></a>内核模式图形引擎   
实现 GDI 功能的 NT 执行代码。

<a href="" id="minidriver-text-files"></a>**微型驱动程序文本文件**  
基于文本的 [Unidrv 微型驱动程序](unidrv-minidrivers.md) ，使用 [GPD 文件项](gpd-file-entries.md)描述打印机。

<a href="" id="binary-data-files"></a>**二进制数据文件**  
临时文件 (的文件) 扩展名为 bud，Unidrv 在分析微型驱动程序文本文件中包含的信息之后创建。

<a href="" id="unidrvui-dll"></a>**unidrvui.dll**  
[Unidrv 用户界面](unidrv-user-interface.md) DLL，为所有支持 Unidrv 的打印机提供通用的 UI 代码。

<a href="" id="user-interface-plug-in"></a>**用户界面插件**  
可选的、特定于打印机的 [用户界面插件](user-interface-plug-ins.md)。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md) 用于打印机的用户界面。

<a href="" id="unidrv-dll"></a>**unidrv.dll**  
[Unidrv](unidrv-renderer.md)呈现器，呈现图像并将图像数据流发送到打印后台处理程序。

<a href="" id="rendering-plug-in"></a>**呈现插件**  
可选的、特定于打印机的、 [呈现插件](rendering-plug-ins.md)。

 

 




