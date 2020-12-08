---
title: C28639
description: 警告 C28639 用字符串调用关闭句柄。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28639
ms.openlocfilehash: 50a1cc7877f96a0719ffa0c6c9b439c3e3f09f72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819801"
---
# <a name="c28639"></a>C28639


警告 C28639：正在用字符串调用关闭句柄

函数 **CloseHandle** 使用 **void \\** _ 参数。 如果要传递使用字符串打开的句柄，则可以将字符串指针) 字符串指针 (转换为 _ *void \\** *，并将其作为参数进行传递。

 

 





