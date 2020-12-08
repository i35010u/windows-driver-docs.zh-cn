---
title: C28171
description: 警告 C28171 该函数有多个 PAGED_CODE 或 PAGED_CODE_LOCKED 的实例。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28171
ms.openlocfilehash: c1a0d9deab28ae93043d42a755e8502987319a1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838153"
---
# <a name="c28171"></a>C28171


警告 C28171：该函数有多个分页 \_ 代码实例或锁定的分页 \_ 代码 \_

此警告意味着函数中有多个分页 \_ 代码实例或分页代码的已 \_ \_ 锁定宏。 此错误是在分页代码的第二个或后续实例上报告的，或者是已 \_ \_ 锁定的代码的 \_ 宏。

分页节中的函数必须恰好有一个分页 \_ 代码实例或分页代码已 \_ \_ 锁定宏，该宏应该出现在函数开头 (**{**) 和第一个条件语句之后以及任何声明之后。

PREfast for 驱动程序在 **\# 杂注分配 \_ 文本** 或 **\# 杂注代码 \_ seg** 用于将函数移到可分页代码节时使用这些宏。 当节名称以 PAGE 开头时，代码分析工具将推断节是可分页的。 有关详细信息，请参阅 [Warning C28170](28170-pageable-code-macro-not-found.md)。

 

 





