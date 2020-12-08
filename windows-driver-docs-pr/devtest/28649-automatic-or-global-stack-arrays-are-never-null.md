---
title: C28649
description: 警告 C28649 自动或全局堆栈数组始终不为 NULL。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28649
ms.openlocfilehash: 8a5b7388d61d2311a0566016b165e7777969be0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840193"
---
# <a name="c28649"></a>C28649


警告 C28649：自动或全局堆栈数组始终不为 NULL

基于堆栈的数组绝不能为 **NULL**。 但是，大多数情况下，目的是检查特定元素， (主要元素) **为 NULL** 或 **nul** 字符。 由于省略错误，程序员缺少引用 (\*) 运算符，从而导致正在检查数组。

 

 





