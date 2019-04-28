---
title: 全局和本地选项文件
description: 全局和本地选项文件
ms.assetid: 9b367e9f-f711-4b76-b331-7563edebb79c
keywords:
- 选项文件 WDK Static Driver Verifier
- 全局选项文件 WDK Static Driver Verifier
- 本地选项文件 WDK Static Driver Verifier
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9885e409667ee065f8336d3408c3f8286c5fe09b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329701"
---
# <a name="global-and-local-options-files"></a>全局和本地选项文件


可以在系统上的 sdv default.xml 文件的多个副本，可以编辑该文件的任何副本中的值。

有两种类型的选项文件：

-   *全局选项文件*是 SDV 安装中的 sdv default.xml 文件\\工具\\sdv\\数据\\*&lt;drivermodel&gt;* WDK 的子目录。 这些文件中的值应用到所有 SDV 验证后，根据驱动程序模型 （WDM、 WDF、 NDIS 或 Storport），除具有在其源目录中的本地选项文件的驱动程序验证。

-   一个*本地选项文件*是位于驱动程序的源目录中的 sdv default.xml 的副本。 复制必须具有的 sdv default.xml 文件的名称。 本地选项文件值仅适用于该驱动程序验证。 SDV 在驱动程序的项目目录中找到本地选项文件，它使用该文件，并忽略全局选项文件中的值。

**谨慎**  不要移动或删除从全局选项文件\\工具\\sdv\\数据\\*&lt;drivermodel&gt;* 子目录和不要重命名它们。 若要创建本地选项文件，使全局选项文件的副本并将其放在驱动程序的项目目录中。 如果全局选项文件中缺少\\工具\\sdv\\数据\\*&lt;drivermodel&gt;* 子目录，SDV 终止验证并显示"找不到 Sdv default.xml"错误消息。

 

 

 





