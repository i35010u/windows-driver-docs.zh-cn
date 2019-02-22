---
title: 如何更改跟踪的每个行上的前缀输出
description: 如何更改跟踪的每个行上的前缀输出
ms.assetid: be2b6207-79f5-4d71-a6a2-075f3078a873
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61becf5f3b8a75ee0541712cbc9a127ee8c7b462
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545676"
---
# <a name="how-do-i-change-the-prefix-output-on-every-trace-line"></a>如何更改跟踪的每个行上的前缀输出？


使用以下命令更改跟踪的每个行上的前缀输出：

```
set TRACE_FORMAT_PREFIX=[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!] 
tracefmt -f mytracefile 
```

有关跟踪的信息\_格式\_作为参数的前缀，请参阅[跟踪消息前缀](trace-message-prefix.md)主题。









