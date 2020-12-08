---
title: C28172
description: 警告 C28172 函数具有 PAGED_CODE 或 PAGED_CODE_LOCKED，但未被声明为位于分页段中。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28172
ms.openlocfilehash: 947f1cb8650a572a3fbd79f13eb7c757dc9ef900
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818617"
---
# <a name="c28172"></a>C28172


警告 C28172：该函数已 \_ 锁定分页代码或分页 \_ 代码， \_ 但未声明为位于分页段中

\_ \_ \_ 使用 **\# 杂注分配 \_ 文本** 或 **\# 杂注代码 \_ seg**，包含分页的代码或分页代码的已锁定宏的函数尚未放置在分页内存中。 当节名称以 PAGE 开头时，代码分析工具将推断节是可分页的。 此错误在与函数中的第一个大括号 (**{**) 相对应的行号上报告。

此错误通常发生在以下情况下发生：要对函数进行分页，但省略了一个杂注或错放了一个，或者函数从分页到了非分页的情况。 有关详细信息，请参阅 [Warning C28170](28170-pageable-code-macro-not-found.md)。

 

 





