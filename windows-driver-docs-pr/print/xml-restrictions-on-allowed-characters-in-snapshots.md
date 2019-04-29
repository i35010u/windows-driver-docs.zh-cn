---
title: 针对快照中允许的字符施加的 XML 限制
description: 针对快照中允许的字符施加的 XML 限制
ms.assetid: e90fb0f2-28f7-4264-bd8c-cd5994717bad
keywords:
- 快照 WDK GDL 个字符的限制
- GDL WDK 源文件
- GDL WDK 字符串
- 源文件 WDK GDL
- 字符串 WDK GDL，个字符的限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a3a152ef4fd6303e7f9991e6f6ea1148949b535
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355249"
---
# <a name="xml-restrictions-on-allowed-characters-in-snapshots"></a>针对快照中允许的字符施加的 XML 限制


XML 源文件可以包含仅的控制字符 （即，这些 ANSI 值小于 0x20 的十六进制字符）：0x09、 0x0a 和 0x0d。 此限制意味着 GDL 源代码文件，不能包含 XML 禁止任何控制字符。 也因为 GDL 字符串的内容 （与任何十六进制字符串值转换为它们的 ANSI 或 Unicode 等效项） 将直接映射到一个 XML 字符串，GDL 字符串不得包含或使用十六进制字符串格式或任何已禁止的控制字符来表示。 但是，命令字符串，因为它们不解释，可以继续使用十六进制字符串格式来表示控制字符。

 

 




