---
title: C28637
description: 警告 C28637 在全局初始值设定项中调用函数是不安全的。
ms.assetid: 9b392995-9583-4847-aded-f32e1daf28ed
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28637
ms.openlocfilehash: 3f0181d17db6e6820fd9d9baabb7c6c5659e02ef
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382429"
---
# <a name="c28637"></a>C28637


警告 C28637：在全局初始值设定项中调用函数是不安全的

使用 DLL 时，通常会从 DllMain 调用任何静态构造函数。 有一些约束适用于从 DllMain 调用其他函数。 具体而言，如果动态加载和卸载 DLL，则可以创建内存泄漏。 有关详细信息，请参阅 [DllMain 回调函数](/windows/win32/dlls/dllmain)。

 

