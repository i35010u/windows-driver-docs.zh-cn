---
title: Windows 内核模式安全字符串库
description: Windows 内核模式安全字符串库
ms.assetid: a54cd20c-2c2d-462d-b9fc-112e99562e52
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 65f17fabfd5ec34940e77be5a4c66e57559c8b78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576955"
---
# <a name="windows-kernel-mode-safe-string-library"></a>Windows 内核模式安全字符串库


在软件安全性方面的主要问题之一被与使用字符串的漏洞。 若要提供更高的安全性，Windows 提供了一个安全字符串库。

安全字符串库例程都带有前缀字母"**Rtl**"; 有关内核的所有安全字符串库例程的列表，请参阅[Unicode 和 ANSI 字符的安全字符串函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/#safe-string-functions-for-unicode-and-ansi-characters)并[UNICODE_STRING 结构的安全字符串函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/#safe-string-functions-for-unicodestring-structures)。

有关使用安全字符串的详细信息，请参阅[使用安全字符串函数](using-safe-string-functions.md)。

请注意，还有单独的运行时库具有的字符串的功能在内核中的常规 C 编程。 有关运行时库 (RTL) 的详细信息，请参阅[Windows 内核模式下运行时库](windows-kernel-mode-run-time-library.md)。 请注意，即使这两个库都带有前缀"**Rtl**"它们不是同一个库。

 

 




