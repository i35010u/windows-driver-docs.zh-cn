---
title: Sdv-map.h
description: Sdv-map.h
keywords:
- 输出文件 WDK 静态驱动程序验证程序
- Sdv-map 静态驱动程序验证程序
- 标头文件 WDK 静态驱动程序验证程序
- 驱动程序入口点 WDK 静态驱动程序验证程序
- 入口点 WDK 静态驱动程序验证程序
- Sdv-map-map 静态驱动程序验证程序，关于 Sdv
- 扫描 DriverEntry 例程 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f237f9fab219161aedeeb0f4802370f3791b7550
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838327"
---
# <a name="sdv-maph"></a>Sdv-map.h


Sdv 是一个标头文件，该文件列出驱动程序中 SDV 检测到的驱动程序入口点。

当你使用 **staticdv/scan** 命令扫描驱动程序的源代码时，SDV 在驱动程序的源目录中创建 SDV 文件。 SDV 使用函数角色类型声明来标识入口点。 如果不使用 **staticdv/scan** 命令，则在使用 **staticdv/CHECK** 命令运行 SDV 分析时，SDV 将创建 SDV-map 文件。

如果此文件不准确或不完整，你可以更正并批准它，然后重新扫描并重新运行验证。

本节包括：

[了解 Sdv](understanding-the-sdv-map-h-file.md)

[Sdv 格式](format-of-the-sdv-map-h-file.md)

[批准 Sdv](approving-the-sdv-map-h-file.md)

[函数角色类型的重复入口点](duplicate-entry-points-for-a-function-role-type.md)

 

 





