---
title: Windows 内核模式安全字符串库
description: Windows 内核模式安全字符串库
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d9ec92ada1db9bf6833299639d7e84ced6b5531
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785105"
---
# <a name="windows-kernel-mode-safe-string-library"></a>Windows 内核模式安全字符串库


软件安全中的一个重要问题是与处理字符串的漏洞相关。 为了提供更高的安全性，Windows 提供了一个安全的字符串库。

安全字符串库例程带有字母 "**Rtl**" 的前缀;有关内核的所有安全字符串库例程的列表，请参阅 [Unicode 和 ANSI 字符的安全字符串函数](/windows-hardware/drivers/ddi/_kernel/#safe-string-functions-for-unicode-and-ansi-characters) 和 [UNICODE_STRING 结构的安全字符串函数](/windows-hardware/drivers/ddi/_kernel/#safe-string-functions-for-unicode_string-structures)。

有关使用安全字符串的详细信息，请参阅 [使用安全字符串函数](using-safe-string-functions.md)。

请注意，此外还提供了一个单独的运行时库，用于在内核中提供字符串功能的一般 C 编程。 有关运行库 (RTL) 的详细信息，请参阅 [Windows Kernel-Mode Run-Time 库](windows-kernel-mode-run-time-library.md)。 请注意，尽管这两个库都带有 "**Rtl**" 前缀，但它们不是同一库。

 

