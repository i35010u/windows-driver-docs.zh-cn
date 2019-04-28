---
title: C28649
description: 警告 C28649 自动或全局堆栈数组永远不会为 NULL。
ms.assetid: 5440269b-6deb-4956-973a-201ab6c4c027
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28649
ms.openlocfilehash: d34eb21bf903f630dde698c8e46d7710efe07907
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345893"
---
# <a name="c28649"></a>C28649


警告 C28649:自动或全局堆栈数组永远不会为 NULL

基于堆栈的数组始终不会**NULL**。 但是，大多数情况下的目的是为了检查特定元素 （主要的第一个元素），针对**NULL**或对于**nul**字符。 由于省略的错误，程序员未命中取消引用 (\*) 结果被改为检查数组中的运算符。

 

 





