---
title: Windows 内核模式安全字符串库
description: Windows 内核模式安全字符串库
ms.assetid: a54cd20c-2c2d-462d-b9fc-112e99562e52
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7d928afe0d61dfe5023a56be0eab0cc25aa693ab
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187023"
---
# <a name="windows-kernel-mode-safe-string-library"></a>Windows 内核模式安全字符串库


软件安全中的一个重要问题是与处理字符串的漏洞相关。 为了提供更高的安全性，Windows 提供了一个安全的字符串库。

安全字符串库例程带有字母 "**Rtl**" 的前缀;有关内核的所有安全字符串库例程的列表，请参阅 [Unicode 和 ANSI 字符的安全字符串函数](/windows-hardware/drivers/ddi/_kernel/#safe-string-functions-for-unicode-and-ansi-characters) 和 [UNICODE_STRING 结构的安全字符串函数](/windows-hardware/drivers/ddi/_kernel/#safe-string-functions-for-unicode_string-structures)。

有关使用安全字符串的详细信息，请参阅 [使用安全字符串函数](using-safe-string-functions.md)。

请注意，此外还提供了一个单独的运行时库，用于在内核中提供字符串功能的一般 C 编程。 有关运行库 (RTL) 的详细信息，请参阅 [Windows 内核模式运行时库](windows-kernel-mode-run-time-library.md)。 请注意，尽管这两个库都带有 "**Rtl**" 前缀，但它们不是同一库。

 

