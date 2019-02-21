---
title: 支持的供应商定义的纸张大小
description: 支持的供应商定义的纸张大小
ms.assetid: 5c356857-ef43-41e4-a4ed-fae6655bd9ce
keywords:
- 供应商提供的纸张大小 WDK Unidrv
- 使用了非标准纸张大小 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3962d8c19760145cceb7d4e818d8d2cea6213d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542002"
---
# <a name="supporting-vendor-defined-paper-sizes"></a>支持的供应商定义的纸张大小





供应商定义的纸张大小是特定于供应商和每个打印机的 GPD 文件必须完全描述。 这些大小也称为非标准的纸张大小，原因是它们不包括在[标准选项](standard-options.md)PaperSize 功能。

有关打印机支持的每个供应商定义的纸张大小，GPD 文件 PaperSize 功能都必须包括\*选项其参数不是一个标准的选项名称的条目。 在此条目中，以下选项属性都是必需的：

\*PageDimensions \*PrintableArea \*PrintableOrigin \*rcNameID 或\*名称\*以下选项属性可用，但不是必需的命令：

\*CursorOrigin \*RotateSize？
\*PageProtectMem
 

 




