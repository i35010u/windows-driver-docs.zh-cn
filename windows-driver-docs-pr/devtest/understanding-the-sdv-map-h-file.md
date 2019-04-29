---
title: 了解 Sdv-map.h 文件
description: 了解 Sdv-map.h 文件
ms.assetid: 2ad3d94d-3991-414b-ae1c-27a07c10839f
keywords:
- 有关 Sdv map.h 的 Sdv map.h WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0db80cf0bfa5d1389258c4760999607dd5b54242
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384702"
---
# <a name="understanding-the-sdv-maph-file"></a>了解 Sdv-map.h 文件


之前验证驱动程序，SDV 扫描驱动程序的源代码和驱动程序的源目录中创建的 Sdv map.h 文件。 应检查并验证您的驱动程序之前批准此标头文件。

此外可以使用**staticdv /scan**定向 SDV 来扫描该驱动程序的命令的代码并创建该文件。 有关说明，请参阅[扫描该驱动程序](scanning-the-driver.md)。

如果 Sdv map.h 文件是不完整或不正确，也就是说，如果任何入口点为缺失，或入口点是使用错误的函数的角色类型、 关联验证是不可靠的。

SDV 的 WDM、 KMDF 和 NDIS 驱动程序使用的函数的列表，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。

Sdv map.h 文件中出现的函数角色类型是在其规则验证中使用的 SDV SDV 使用函数角色类型声明添加到生成中的驱动程序的源代码目录的 Sdv map.h 文件的头文件。 在 Sdv map.h 文件中，SDV 映射到在验证期间使用的 SDV 函数标识符的声明的驱动程序函数。 例如，对于 KMDF 驱动程序，回调函数调用*MyDpc*可能会映射到有趣\_WDF\_DPC\_1。 

SDV 不需要该驱动程序声明函数的所有回叫函数，它使用的角色类型。 它只需如果驱动程序已声明函数角色类型的 SDV 知道以及将其正确解释。 如果驱动程序不具有函数角色类型的 SDV 要求来验证特定规则，SDV 到结束，此规则不适用于驱动程序。 这不被视为错误或缺陷。 

请务必你先纠正 Sdv map.h 文件中的任何错误，然后验证该驱动程序。 如果该文件是不正确，则验证可能不是可靠。

 

 





