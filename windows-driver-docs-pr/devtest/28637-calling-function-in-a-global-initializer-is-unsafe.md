---
title: C28637
description: 警告 C28637 调用全局初始值设定项中的函数是不安全。
ms.assetid: 9b392995-9583-4847-aded-f32e1daf28ed
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28637
ms.openlocfilehash: 0c80dadb44602f714710ccbfe9ef0fe560218488
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562630"
---
# <a name="c28637"></a>C28637


警告 C28637:全局初始值设定项中调用该函数是不安全

如果使用的 DLL，它通常是这种情况从 DllMain 调用任何静态构造函数。 有多种适用于从 DllMain 调用其他函数的约束。 具体而言，就可以创建内存泄漏，如果 DLL 加载和卸载动态。 有关详细信息，请参阅[DllMain 回调函数](https://go.microsoft.com/fwlink/p/?linkid=133876)。

 

 





