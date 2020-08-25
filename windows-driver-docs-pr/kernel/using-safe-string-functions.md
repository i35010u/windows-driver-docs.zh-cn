---
title: 使用安全字符串函数
description: 使用安全字符串函数
ms.assetid: a84008e8-e490-4640-a734-ef55cfbdfea3
keywords:
- 安全字符串函数 WDK
- 字符串操作函数 WDK
- 缓冲 WDK 安全字符串函数
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3633945ee0496d3df00835afb3eeff7483617149
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802775"
---
# <a name="using-safe-string-functions"></a>使用安全字符串函数





许多系统安全问题都是由于缓冲区处理不当和生成的缓冲区溢出导致的。 不良缓冲区处理通常与字符串操作操作相关联。 C/c + + 语言运行库提供的标准字符串操作函数 (**strcat**、 **strcpy**、 **sprintf**等) 不阻止写入缓冲区的末尾。

两组新的字符串操作函数（称为 *安全字符串函数*）为代码中的正确缓冲区处理提供额外处理。 这些安全的字符串函数在 Windows 驱动程序工具包 (WDK) 中提供，适用于 Microsoft Windows XP SP1 和更高版本的驱动程序开发工具包 (DDK) 和 Windows SDK。 它们旨在替换 Windows 提供的内置 C/c + + 和类似的例程。

一组安全字符串函数用于内核模式代码。 这些函数在名为 Ntstrsafe.h 而的头文件中具有原型。 此头文件和关联的库在 WDK 中可用。

其他一组安全字符串函数可在用户模式应用程序中使用。 对应的标头文件 Strsafe 包含这些函数的原型。 Windows SDK 中提供了该文件和关联的库。 有关 Strsafe 的详细信息，请参阅 [使用 Strsafe 函数](https://go.microsoft.com/fwlink/p/?linkid=165522)。

一组内核模式安全字符串函数包含以下两个子集：

-   [Unicode 和 ANSI 字符的安全字符串函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

    其中的每个函数都在支持双字节 Unicode 字符的 W 后缀版本中提供，并且支持单字节 ANSI 字符。 例如， [**RtlStringCbCatN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatna)，它将两个字符串连接起来并限制附加字符串的长度，可用作 [**RtlStringCbCatNW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatnw) 和 [**RtlStringCbCatNA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe//nf-ntstrsafe-rtlstringcbcatna)。

-   [UNICODE 字符串结构的安全字符串函数 \_](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

    其中每个函数都接受 [**UNICODE \_ 字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string) 结构作为输入或输出参数，或者两者都接受。 例如， [**RtlStringCbCopyUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestring) 接受作为输入参数的结构， [**RtlUnicodeStringCopyString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystring) 接受作为输出参数的结构， [**RtlUnicodeStringCopy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopy) 接受该结构作为输入和输出参数。

内核模式安全字符串函数提供以下功能：

-   每个安全字符串函数接收目标缓冲区的大小作为输入。 因此，该函数可以确保它不会写入超过缓冲区的末尾。

-   Unicode 和 ANSI 字符串函数终止所有包含 NULL 字符的输出字符串，即使操作截断了预期的结果。

-   所有安全字符串函数都将返回一个 NTSTATUS 值，其中只有一个可能成功的代码 (状态 \_ 成功) 。

-   大多数安全字符串函数在字节计数和字符计数版本中均可用。 例如， [**RtlStringCbCata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcata) 连接两个字节计数的字符串， [**RtlStringCchCata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcata) 将两个字符计数字符串连接起来。

-   最安全的字符串函数以提供附加功能的扩展的 Ex 后缀版本提供。 例如， [**RtlStringCbCatExa**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatexa) 扩展了 [**RtlStringCbCata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcata)的功能。

本节包括下列主题：

[内核模式安全字符串函数摘要](summary-of-kernel-mode-safe-string-functions.md)

[导入内核模式安全字符串函数](importing-kernel-mode-safe-string-functions.md)

 

 




