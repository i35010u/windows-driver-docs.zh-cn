---
title: 支持标准纸张大小
description: 支持标准纸张大小
keywords:
- 标准纸张大小 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1af07f9bf6030af323192242104ae380aa95f755
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806795"
---
# <a name="supporting-standard-paper-sizes"></a>支持标准纸张大小





标准纸张大小由 PaperSize 功能的 [标准选项](standard-options.md) 表示。

对于打印机支持的每个标准纸张大小，GPD 文件的 PaperSize 功能必须包括一个 \* 选项条目，其参数是除 CUSTOMSIZE) 之外的标准选项名称之一 (。 在此条目中，需要以下选项属性：

\*PrintableArea \* PrintableOrigin \* rcNameID \* 命令，可以使用以下选项属性，但这不是必需的：

\*CursorOrigin \* RotateSize？
\*PageProtectMem 对于所有标准纸张大小， \_ \_ \_ stdnames. gpd) 中定义的 RCID DMPAPER 系统名称资源标识符 (应用作 \* **rcNameID** 的参数。

 

 




