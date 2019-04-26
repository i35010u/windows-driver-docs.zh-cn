---
title: C28637
description: 警告 C28637 调用全局初始值设定项中的函数是不安全。
ms.assetid: 9b392995-9583-4847-aded-f32e1daf28ed
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28637
ms.openlocfilehash: 0c80dadb44602f714710ccbfe9ef0fe560218488
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327179"
---
# <a name="c28637"></a>C28637


警告 C28637:全局初始值设定项中调用该函数是不安全

如果使用的 DLL，它通常是这种情况从 DllMain 调用任何静态构造函数。 有多种适用于从 DllMain 调用其他函数的约束。 具体而言，就可以创建内存泄漏，如果 DLL 加载和卸载动态。 有关详细信息，请参阅[DllMain 回调函数](https://go.microsoft.com/fwlink/p/?linkid=133876)。

 

 





