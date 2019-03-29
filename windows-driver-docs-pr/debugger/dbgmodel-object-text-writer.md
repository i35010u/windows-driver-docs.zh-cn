---
title: 调试器数据模型-文本 Wrtier 对象
description: 将文本写入文件。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3decf94b03848a8193677209083ae23a7320c5dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569076"
---
# <a name="text-writer-objects"></a>文本编写器对象 
## <a name="summary"></a>总结
文本编写器对象写入到文件的给定编码的文本。

## <a name="object-methods"></a>对象方法
|“属性”|签名|描述|
|--- |--- |--- |
|写入|Write(object)|将给定对象的字符串转换写入到文件而不进行换行。|
|WriteLine|WriteLine(object)|将给定对象的字符串转换写入到跟换行符的文件。|
|WriteContents|WriteContents(object)|循环访问*对象*并将对应每个循环访问元素的字符串写入到文件而不进行之间每一个换行符。|
|WriteLineContents|WriteLineContents(object)|循环访问*对象*并将对应每个循环访问元素的字符串写入到具有之间每个换行符的文件。|