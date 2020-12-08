---
title: 打印机接口 DLL 简介
description: 打印机接口 DLL 简介
keywords:
- 打印机接口 DLL WDK，关于打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f31ac259a8098deb8c741ef35770a0c75555a906
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835619"
---
# <a name="introduction-to-printer-interface-dlls"></a>打印机接口 DLL 简介





打印机通常为用户提供大量可修改的配置选项，这些选项可为打印的每个文档更改。 诸如纸张、纸盒和字体选择以及图像分辨率、大小、颜色等选项，都必须可通过应用程序可以调用的用户界面进行访问。

打印机驱动程序的 *打印机接口 DLL*（在用户模式下执行）负责将用户界面导出到打印机的配置选项。 提供此接口涉及到 [为打印机创建属性表页](creating-property-sheet-pages-for-printers.md)。 应用程序 (如打印文件夹) 通过调用打印后台处理程序导出的 Win32 函数来显示接口，而后台处理程序则调用 [由打印机接口 dll 定义的函数](functions-defined-by-printer-interface-dlls.md)。

提供配置选项的用户界面不是打印机接口 DLL 的唯一责任。 DLL 还会导出后台处理程序可以调用的函数，以通知驱动程序与打印相关的系统事件（如驱动程序安装和升级，或者打印机添加和连接）的驱动程序。

 

 




