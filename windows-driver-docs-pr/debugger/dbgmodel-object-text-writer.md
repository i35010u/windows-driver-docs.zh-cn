---
title: 调试器数据模型-文本 Wrtier 对象
description: 向文件写入文本。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3decf94b03848a8193677209083ae23a7320c5dd
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750034"
---
# <a name="text-writer-objects"></a>文本编写器对象 
## <a name="summary"></a>总结
文本编写器对象将给定编码的文本写入文件。

## <a name="object-methods"></a>对象方法
|名称|签名|描述|
|--- |--- |--- |
|写入|写入（object）|将给定对象的字符串转换写入文件，而不使用换行符。|
|WriteLine|WriteLine （object）|将给定对象的字符串转换写入文件，后跟一个换行符。|
|WriteContents|WriteContents （对象）|循环访问*对象*，并将每个迭代的元素的字符串转换写入文件，其中每个元素之间没有换行符。|
|WriteLineContents|WriteLineContents （对象）|循环访问*对象*，并将每个迭代元素的字符串转换写入文件，每个循环元素之间有一个换行符。|