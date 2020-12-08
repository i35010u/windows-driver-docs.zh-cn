---
title: 了解 Sdv-map.h 文件
description: 了解 Sdv-map.h 文件
keywords:
- Sdv-map-map 静态驱动程序验证程序，关于 Sdv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 078e9e620dee50e7f00a3f99a4fbb8f47f3c01c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830121"
---
# <a name="understanding-the-sdv-maph-file"></a>了解 Sdv-map.h 文件


在验证驱动程序之前，SDV 会扫描驱动程序的源代码，并在驱动程序的源目录中创建 Sdv 文件。 在验证驱动程序之前，应检查并批准此标头文件。

还可以使用 **staticdv/scan** 命令来指示 SDV 扫描驱动程序的代码和创建文件。 有关说明，请参阅 [扫描驱动程序](scanning-the-driver.md)。

如果 Sdv 文件不完整或不正确（即，如果缺少任何入口点或入口点与错误的函数角色类型相关联，则验证不可靠。

有关 SDV 用于 WDM、KMDF 和 NDIS 驱动程序的函数的列表，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md)。

Sdv 文件中出现的函数角色类型是 SDV 在其规则验证中使用的类型。 SDV 使用已添加到标头文件中的函数角色类型声明在驱动程序的源代码目录中生成 Sdv 文件。 在 Sdv 文件中，SDV 将声明的驱动程序函数映射到在验证期间 SDV 使用的函数标识符。 例如，对于 KMDF 驱动程序，名为 *MyDpc* 的回调函数可能会映射到有趣的 \_ WDF \_ DPC \_ 1。 

SDV 不要求驱动程序为其使用的所有回调函数声明函数角色类型。 仅当驱动程序声明了 SDV 知道并正确解释的函数角色类型时，它才需要。 如果驱动程序没有 SDV 所需的函数角色类型来验证特定的规则，SDV 将得出规则，指出该规则不适用于该驱动程序。 这不会被视为错误或缺陷。 

在验证驱动程序之前，请务必更正 Sdv 文件中的任何错误。 如果文件错误，则验证可能不可靠。

 

 





