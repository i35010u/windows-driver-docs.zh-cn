---
title: Sdv-map.h
description: Sdv-map.h
ms.assetid: c230fb86-fe65-416b-bd3e-a0ab7270576d
keywords:
- 输出文件 WDK Static Driver Verifier
- Sdv map.h WDK 的 Static Driver Verifier
- 头文件 WDK Static Driver Verifier
- 驱动程序入口点 WDK Static Driver Verifier
- 入口点 WDK Static Driver Verifier
- 有关 Sdv map.h 的 Sdv map.h WDK Static Driver Verifier
- 扫描 DriverEntry 例程 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02ee90b793f42a3150612dfc97be2ed6ade6d323
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576775"
---
# <a name="sdv-maph"></a>Sdv-map.h


Sdv map.h 是列出 SDV 检测到驱动程序中的驱动程序入口点的标头文件。

SDV 在使用时，驱动程序的源目录中创建的 Sdv map.h 文件**staticdv /scan**命令，扫描驱动程序的源代码。 SDV 使用函数角色类型声明标识的入口点。 如果不使用**staticdv /scan**命令，使用时将 SDV 创建 Sdv map.h 文件**staticdv /check**命令以运行 SDV 分析。

如果此文件是不准确或不完整，您可以更正、 批准，重新扫描并重新运行验证。

本部分包括：

[了解 Sdv map.h](understanding-the-sdv-map-h-file.md)

[Sdv map.h 格式](format-of-the-sdv-map-h-file.md)

[批准 Sdv map.h](approving-the-sdv-map-h-file.md)

[重复入口点函数角色类型](duplicate-entry-points-for-a-function-role-type.md)

 

 





