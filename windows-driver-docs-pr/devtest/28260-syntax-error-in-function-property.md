---
title: C28260
description: 警告 C28260 在分析函数内的属性时，发现批注中出现语法错误。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28260
ms.openlocfilehash: e0a8087910875ab3480a81b9430b3447db6aa649
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799805"
---
# <a name="c28260"></a>C28260


警告 C28260：分析函数内的属性时，在注释中发现了语法错误

此警告表明批注而不是所分析的代码中存在错误。 消息文本中提到的文本将从低级注释中提取，这通常是以宏的形式进行编码的。 但通常情况下，语法错误位于作为一个宏的参数的表达式中。 语法错误的常见位置是包含批注函数的标头文件。

 

 





