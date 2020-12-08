---
title: Pscript 功能
description: Pscript 功能
keywords:
- PostScript 打印机驱动程序 WDK 打印，功能
- Pscript WDK 打印，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab158c7845e2b848128dc71ed489ee8e41bd0de8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807173"
---
# <a name="pscript-capabilities"></a>Pscript 功能





PostScript 打印机驱动程序 (Pscript) 提供以下功能：

-   支持所有 PostScript 打印机，使用特定于打印机的基于 *PPD* 的 [Pscript 微型驱动程序](pscript-minidrivers.md) 描述每个打印机的特征。

-   基于 TreeView 控件和属性表的 [Pscript 用户界面](pscript-user-interface.md)，对所有打印机都是一致的，但对于每个打印机的唯一选项也是可修改的。

-   单个 [Pscript 呈现](pscript-renderer.md) 器，与 GDI 图形引擎一起，将应用程序中的 MICROSOFT Win32 GDI 调用转换为可发送到打印后台处理程序的打印机命令。

-   支持3.1 版本的文档结构约定，详见 Adobe Systems，Inc. 发布的 PostScript 语言参考手册。

-   支持提供 PostScript 级别1、级别2或3级功能的打印机。

-   以下类型的字体支持：
    -   以 PostScript 类型1或类型2字体增量下载 OpenType 字体。
    -   增量下载 TrueType 字体作为 PostScript 类型1、类型3、类型32、类型42或基于 CID 的类型42字体。
    -   将宿主驻留的光栅字体作为 PostScript 类型3增量下载或键入32字体。
    -   完全下载主机驻留 PostScript 类型1字体。
    -   打印机驻留 PostScript 类型1、类型2和 CID 字体。
    -   对于打印机字符集中存在的标志符号，每个字形的字体替换。
-   支持 ICM 2.0，并允许在主机系统或打印机硬件上执行图像颜色管理。

 

 




