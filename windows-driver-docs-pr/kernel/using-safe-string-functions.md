---
title: 使用安全字符串函数
description: 使用安全字符串函数
ms.assetid: a84008e8-e490-4640-a734-ef55cfbdfea3
keywords:
- 安全字符串函数 WDK
- 字符串操作函数 WDK
- 缓冲区 WDK 安全字符串函数
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee63e77c0760c1aef2619c25e18d0038da4082b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350999"
---
# <a name="using-safe-string-functions"></a>使用安全字符串函数





许多系统安全性问题所引起的不佳缓冲区处理和得到的缓冲区溢出。 不佳缓冲区处理通常是与字符串处理操作相关联。 提供的 C 标准字符串操作函数 /C++的语言运行时库 (**strcat**， **strcpy**， **sprintf**等) 不会阻止超出缓冲区末尾的写入。

两组新的字符串操作函数，称为*安全的字符串函数*，提供适当的缓冲区在代码中处理的其他处理。 这些安全的字符串函数是可在 Windows Driver Kit (WDK) 和 Microsoft Windows XP SP1 和更高版本的驱动程序开发工具包 (DDK) 和 Windows SDK。 它们旨在取代其内置的 C /C++对应的和由 Windows 提供的类似例程。

一组安全的字符串函数是在内核模式代码中使用。 在名为 Ntstrsafe.h 的标头文件中，这些函数是构建出原型。 WDK 中提供了此标头文件和关联的库。

安全字符串函数的其他组是在用户模式应用程序中使用。 相应的头文件 Strsafe.h，包含这些函数的原型。 该文件和关联的库是在 Windows SDK 中提供。 有关 Strsafe.h 详细信息，请参阅[使用 Strsafe.h 函数](https://go.microsoft.com/fwlink/p/?linkid=165522)。

组的内核模式安全的字符串函数包括以下两个子集：

-   [Unicode 和 ANSI 字符的安全字符串函数](https://msdn.microsoft.com/library/windows/hardware/ff563642)

    每个函数是在支持双字节 Unicode 字符的 W 后缀的版本和支持单字节 ANSI 字符的一个后缀的版本中可用。 例如， [ **RtlStringCbCatN**](https://msdn.microsoft.com/library/windows/hardware/ff562801)，其中串联两个字符串，并限制追加的字符串的长度是可用作**RtlStringCbCatNW**和**RtlStringCbCatNA**。

-   [安全字符串函数对于 UNICODE\_字符串结构](https://msdn.microsoft.com/library/windows/hardware/ff563644)

    每个这些函数都接受[ **UNICODE\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff564879)作为输入或输出参数和 / 或结构。 例如， [ **RtlStringCbCopyUnicodeString** ](https://msdn.microsoft.com/library/windows/hardware/ff562815)接受作为输入参数，结构[ **RtlUnicodeStringCopyString** ](https://msdn.microsoft.com/library/windows/hardware/ff562948)接受的结构作为输出参数，并[ **RtlUnicodeStringCopy** ](https://msdn.microsoft.com/library/windows/hardware/ff562942)接受作为输入和输出参数的结构。

内核模式安全字符串函数可提供以下功能：

-   每个安全的字符串函数作为输入接收目标缓冲区的大小。 因此，该函数可以确保，它不会写入超过缓冲区的末尾。

-   Unicode 和 ANSI 字符串函数终止 NULL 字符开头的所有输出字符串，即使该操作将截断想要的结果。

-   所有安全的字符串函数都返回的 NTSTATUS 值，只有一个可能的成功代码 (状态\_成功)。

-   大多数安全的字符串函数是在字节计数和字符计数的版本中可用。 例如， [ **RtlStringCbCat** ](https://msdn.microsoft.com/library/windows/hardware/ff562795)串联两个字节计数字符串并[ **RtlStringCchCat** ](https://msdn.microsoft.com/library/windows/hardware/ff562834)串联两个计数字符的字符串。

-   提供了附加功能的扩展，例如为后缀版本中提供了大多数安全的字符串函数。 例如， [ **RtlStringCbCatEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562799)扩展的功能[ **RtlStringCbCat**](https://msdn.microsoft.com/library/windows/hardware/ff562795)。

本部分包括以下主题：

[内核模式安全字符串函数的摘要](summary-of-kernel-mode-safe-string-functions.md)

[导入内核模式安全的字符串函数](importing-kernel-mode-safe-string-functions.md)

 

 




