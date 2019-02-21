---
title: C28639
description: 警告 C28639 调用关闭句柄的字符串。
ms.assetid: 346b9798-3719-4b8e-8edd-f8ee3b751cef
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28639
ms.openlocfilehash: 3b495f2b4159cc5e8f462031125f40b270dc461b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540857"
---
# <a name="c28639"></a>C28639


警告 C28639:使用字符串调用关闭句柄

该函数**CloseHandle**采用**void \\** * 参数。 可以强制转换 （还有其他因素） 指向的字符串指针**void \\** * 并将其作为参数传递时的目的是要传递的句柄打开使用字符串。

 

 





