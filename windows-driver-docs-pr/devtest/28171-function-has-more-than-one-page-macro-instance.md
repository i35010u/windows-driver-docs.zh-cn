---
title: C28171
description: 警告 C28171 函数具有多个是 PAGED_CODE 或 PAGED_CODE_LOCKED 的实例。
ms.assetid: 7a3740aa-53fc-4219-9606-edc0e9bd9879
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28171
ms.openlocfilehash: 6416fd9749c234decbbd002dc89babc0a042ca54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361327"
---
# <a name="c28171"></a>C28171


警告 C28171:该函数具有多个实例 PAGED\_代码或 PAGED\_代码\_已锁定

此警告指示存在多个实例 PAGED\_代码或 PAGED\_代码\_已锁定宏在函数中的。 在分页的第二个或后续实例报告此错误\_代码或 PAGED\_代码\_已锁定宏。

分页部分中的函数必须具有恰好一个实例 PAGED\_代码或 PAGED\_代码\_锁定宏和宏应出现在第一个大括号之间的函数的开头 ( **{** ) 和第一个条件语句，以及之后的任何声明。

PREfast 驱动程序使用这些宏时 **\#杂注分配\_文本**或 **\#杂注代码\_seg**用于将函数转换为可分页的代码部分。 代码分析工具会推断出的节名称开头页时，部分是可分页。 有关详细信息，请参阅[警告 C28170](28170-pageable-code-macro-not-found.md)。

 

 





