---
title: 针对快照中允许的字符施加的 XML 限制
description: 针对快照中允许的字符施加的 XML 限制
keywords:
- 快照 WDK GDL，允许字符
- GDL WDK，源文件
- GDL WDK，字符串
- 源文件 WDK GDL
- 字符串 WDK GDL，允许字符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0779790e23b187efe50c36d4add10251f107777
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785755"
---
# <a name="xml-restrictions-on-allowed-characters-in-snapshots"></a>针对快照中允许的字符施加的 XML 限制


XML 源文件只能包含控制字符 (也就是说，这些字符的 ANSI 值小于 0x20 hex) ：0x09、0x0a 和0x0d。 此限制意味着 GDL 源文件不能包含 XML 禁止的任何控制字符。 此外，由于 GDL 字符串的内容直接映射到 XML 字符串 (并且该字符串的任何十六进制字符串值转换为其 ANSI 或 Unicode 等效) ，因此 GDL 字符串不得使用十六进制字符串格式或任何禁止控制字符来包含或表示。 但是，命令字符串，因为它们不是解释性的，所以可以使用十六进制字符串格式继续表示控制字符。

 

 




