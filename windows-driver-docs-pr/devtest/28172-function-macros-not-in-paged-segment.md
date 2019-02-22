---
title: C28172
description: 警告的 C28172 函数具有 PAGED_CODE 或 PAGED_CODE_LOCKED，但未声明位于分页段中。
ms.assetid: c97bf9e8-583c-41ca-9c50-ac2af3dd5dc0
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28172
ms.openlocfilehash: 1569c1bc5f8e3cceed3c41a51fa3a2bb17f45de8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547561"
---
# <a name="c28172"></a>C28172


警告 C28172:该函数已分页\_代码或 PAGED\_代码\_已锁定，但未声明位于分页段

包含分页的函数\_代码或 PAGED\_代码\_锁定宏尚未用于分页的内存中使用**\#杂注分配\_文本**或**\#杂注代码\_seg**。 代码分析工具会推断出的节名称开头页时，部分是可分页。 此错误报告在与第一个大括号相对应的行号 (**{**) 函数中。

如果该函数原来是为了进行分页，通常会出现此错误但杂注之一已省略或误放，或从函数更改时分页到非分页。 有关详细信息，请参阅[警告 C28170](28170-pageable-code-macro-not-found.md)。

 

 





