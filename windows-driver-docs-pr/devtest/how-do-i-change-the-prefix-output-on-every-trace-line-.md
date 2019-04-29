---
title: 如何更改跟踪的每个行上的前缀输出
description: 如何更改跟踪的每个行上的前缀输出
ms.assetid: be2b6207-79f5-4d71-a6a2-075f3078a873
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61becf5f3b8a75ee0541712cbc9a127ee8c7b462
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360389"
---
# <a name="how-do-i-change-the-prefix-output-on-every-trace-line"></a>如何更改每个跟踪行中的前缀输出？


使用以下命令更改跟踪的每个行上的前缀输出：

```
set TRACE_FORMAT_PREFIX=[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!] 
tracefmt -f mytracefile 
```

有关跟踪的信息\_格式\_作为参数的前缀，请参阅[跟踪消息前缀](trace-message-prefix.md)主题。









