---
title: 支持供应商定义的纸张大小
description: 支持供应商定义的纸张大小
keywords:
- 供应商提供的纸张大小 WDK Unidrv
- 非标准纸张大小 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b6747344d4d4b12297a6981361bd05358088846
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806817"
---
# <a name="supporting-vendor-defined-paper-sizes"></a>支持供应商定义的纸张大小





供应商定义的纸张大小是特定于供应商的，必须由每个打印机的 GPD 文件全面描述。 这些大小也称为非标准纸张大小，因为它们不包含在 PaperSize 功能的 [标准选项](standard-options.md) 中。

对于打印机支持的每个供应商定义的纸张大小，GPD 文件的 PaperSize 功能必须包括一个 \* 选项条目，其参数不是标准选项名称之一。 在此条目中，需要以下选项属性：

\*PageDimensions \* PrintableArea \* PrintableOrigin \* rcNameID 或 \* Name \* 命令可以使用以下选项属性，但这不是必需的：

\*CursorOrigin \* RotateSize？
\*PageProtectMem
 

 




