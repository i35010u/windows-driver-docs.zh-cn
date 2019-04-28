---
title: 支持标准纸张大小
description: 支持标准纸张大小
ms.assetid: 04f8fbdb-88f8-4595-b5d2-74315c02bb41
keywords:
- 标准纸张大小 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ee3143567a530f06e80f3613a1cf04e57401bd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331751"
---
# <a name="supporting-standard-paper-sizes"></a>支持标准纸张大小





标准纸张大小由[标准选项](standard-options.md)PaperSize 功能。

对于每个打印机支持的标准纸张大小，GPD 文件 PaperSize 功能必须包含\*选项其参数是一个标准的选项名称 （除了 CUSTOMSIZE) 的条目。 在此条目中，以下选项属性都是必需的：

\*PrintableArea \*PrintableOrigin \*rcNameID\*以下选项属性可用，但不是必需的命令：

\*CursorOrigin \*RotateSize？
\*适用于所有标准纸张大小，RCID PageProtectMem\_DMPAPER\_系统\_名称资源标识符 （stdnames.gpd 中定义） 应使用作为参数\* **rcNameID**.

 

 




