---
title: 全局和本地选项文件
description: 全局和本地选项文件
keywords:
- 选项文件 WDK 静态驱动程序验证程序
- 全局选项文件 WDK 静态驱动程序验证程序
- 本地选项文件 WDK 静态驱动程序验证程序
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1445a42cc010ed8cad8ef7352beffe3bf542e4e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831579"
---
# <a name="global-and-local-options-files"></a>全局和本地选项文件


您可以在系统上拥有 sdv-default.xml 文件的多个副本，并且您可以编辑该文件的任何副本中的值。

有两种类型的选项文件：

-   *全局选项文件* 是 SDV 在 \\ WDK 的 tools \\ SDV \\ data \\ *&lt; &gt; drivermodel* 子目录中安装的 sdv-default.xml 文件。 这些文件中的值适用于所有 SDV 验证，具体取决于驱动程序模型 (WDM、WDF、NDIS 或 Storport) ，但其源目录中具有本地选项文件的驱动程序验证除外。

-   *本地选项文件* 是位于驱动程序源目录中 sdv-default.xml 的副本。 该副本必须具有 sdv-default.xml 文件名。 本地选项文件值仅适用于该驱动程序的验证。 当 SDV 在驱动程序的项目目录中查找本地选项文件时，它将使用该文件并忽略全局选项文件中的值。

**警告**  请勿从 \\ tools \\ sdv \\ data \\ *&lt; &gt; drivermodel* 子目录中移动或删除全局选项文件，并且不要对它们进行重命名。 若要创建本地选项文件，请创建全局选项文件的副本，并将其放置在驱动程序的项目目录中。 如果 \\ 工具 \\ sdv data \\ \\ *&lt; drivermodel &gt;* 子目录中缺少全局选项文件，sdv 将终止验证并显示 "找不到 Sdv-default.xml" 错误消息。

 

 

 





