---
title: 调试器数据模型 - 文本读取器对象
description: 读取带文件的文本。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: c6ab3867607fbc4e957c629826ec9a69c8e807de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376082"
---
# <a name="text-reader-objects"></a>文本读取器对象 
## <a name="summary"></a>总结
文本读取器对象从文件读取文本。

## <a name="object-methods"></a>对象方法
|名称|签名|描述|
|--- |--- |--- |
|ReadLine|ReadLine()|从文件读取直到下一步的行尾 （或文件尾标记） 并返回作为字符串读取。|
|ReadLineContents|ReadLineContents()|返回字符串的可迭代集合。 集合中的每个字符串表示文件中的一行。|