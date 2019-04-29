---
title: Pscript 功能
description: Pscript 功能
ms.assetid: 1530cb64-a1b1-4ff5-a6bf-b3634e83a225
keywords:
- PostScript 打印机驱动程序 WDK 打印，功能
- Pscript WDK 打印，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7729dfa4f62b93aaed391ed613864e31c06009d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376546"
---
# <a name="pscript-capabilities"></a>Pscript 功能





PostScript 打印机驱动程序 (Pscript) 提供了以下功能：

-   支持使用特定于打印机的所有 PostScript 打印机*PPD*-基于[Pscript 微型驱动程序](pscript-minidrivers.md)，用于描述每个打印机的特征。

-   一个[Pscript 用户界面](pscript-user-interface.md)根据树视图控件和属性表，是一致的所有打印机，而且也是可修改的每个打印机的唯一选项。

-   将单个[Pscript 呈现器](pscript-renderer.md)，GDI 图形引擎，以及 Microsoft Win32 GDI 调用将从转换成可以发送到打印后台处理程序的打印机命令的应用程序。

-   对文档结构化约定，由 Adobe Systems，Inc.发布 PostScript 语言参考手册中所述的 3.1 版本的支持

-   对打印机提供 PostScript 级别 1、 级别 2 或 3 级功能的支持。

-   字体支持以下类型：
    -   增量下载的 OpenType 字体与 PostScript 类型 1 或类型 2 的字体。
    -   增量下载 TrueType 字体作为 PostScript 类型 1、 类型 3，类型 32、 Type 42 或基于 CID 的 Type 42 字体。
    -   增量下载驻留在主机的光栅字体作为 PostScript 类型 3 或类型 32 字体。
    -   完整下载驻留在主机的 PostScript Type 1 字体。
    -   驻留在打印机中的 PostScript 类型 1、 类型 2 和 CID 字体。
    -   每个符号，打印机的字符集中存在的标志符号的字体替换。
-   支持 ICM 2.0，并允许图像颜色管理的主机系统上或打印机硬件执行。

 

 




