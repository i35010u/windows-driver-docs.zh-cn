---
title: GDI 打印机驱动程序
description: GDI 打印机驱动程序
keywords:
- GDI 打印机驱动程序 WDK
- 打印机驱动程序 WDK，GDI
- GDI 打印机驱动程序 WDK，关于 GDI 打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed8aaa334aca76c2d74b76e56e8ea23c4c69851c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797055"
---
# <a name="gdi-printer-drivers"></a>GDI 打印机驱动程序





所有 Windows 2000 和更高版本的打印机驱动程序包含以下组件：

-   在呈现打印作业时帮助 GDI 的 [打印机图形 DLL](printer-graphics-dll.md) ，并将呈现的数据流发送到打印后台处理程序。

-   为驱动程序的配置参数提供用户界面的 [打印机接口 DLL](printer-interface-dll.md) ，以及后台处理程序可以调用以通知驱动程序与打印相关的系统事件的接口。

此外，Microsoft 提供的打印机驱动程序使用 [打印机数据文件](printer-data-files.md)。

 

 




