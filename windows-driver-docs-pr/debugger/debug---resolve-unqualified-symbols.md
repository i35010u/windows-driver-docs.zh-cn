---
title: 调试解析非限定符号
description: 调试解析非限定符号
keywords:
- 调试解析非限定符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9414add83cb51708e740cbcb8f4cedbd21dd9896
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830269"
---
# <a name="debug--resolve-unqualified-symbols"></a>调试 | 解决不符合要求的符号


选择 "**调试**" 菜单上的 "**解析非限定符号**" 可解析没有模块前缀的符号。

如果清除 " **解析非限定符号**"，调试器将无法解析没有模块前缀的符号。 如果未选择 " **解析非限定符号** "，并且尚未加载没有前缀的变量，则调试器不会加载任何其他要解析的符号。 如果此选项已被清除，则仍可以使用非限定符号，但前提是它们先前已加载。

尽管我们始终建议使用模块限定符，但如果不使用模块限定符，则可以清除 " **解析非限定符号** " 选项，以避免加载解析不正确或拼写错误的符号的符号。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关符号、加载符号和验证符号的详细信息，请参阅 [符号](symbols.md)。

 

 





