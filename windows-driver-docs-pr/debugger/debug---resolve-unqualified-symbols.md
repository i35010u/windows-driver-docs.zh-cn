---
title: 调试解析非限定的符号
description: 调试解析非限定的符号
ms.assetid: 8b935640-a01d-46e8-a9e4-08f20e293196
keywords:
- 调试解析非限定的符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24679b1a2872e81170ab7bf14d93190a7ad9a513
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524679"
---
# <a name="debug--resolve-unqualified-symbols"></a>调试 |解析不合格的符号


选择**解析非限定符号**上**调试**菜单用于解析不具有任何模块的前缀的符号。

如果清除**解析非限定符号**，调试器无法解析不具有任何模块的前缀的符号。 如果不选择**解析非限定符号**和具有没有前缀的变量时未加载，调试器不会加载任何其他符号，若要解决此问题。 如果该选项是很清晰，但前提是它们已进行先前加载，仍可以使用非限定的符号。

不过，我们始终建议你使用模块限定符，则可以清除**解析非限定符号**选项，以避免加载时不使用模块限定符解析不正确或者存在拼写错误的符号的符号。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关符号的详细信息，加载符号，并验证符号，请参阅[符号](symbols.md)。

 

 





