---
title: 检查堆栈跟踪
description: 检查堆栈跟踪
ms.assetid: ca203f29-841f-411e-915a-81abaa96a8e6
keywords:
- 调试器引擎 API，堆栈跟踪
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f384f3a25510c3fa8a8bd4bde2bea077501bf0fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347783"
---
# <a name="examining-the-stack-trace"></a>检查堆栈跟踪


一个*调用堆栈*包含由线程进行的函数调用的数据。 每个函数调用的数据称为*堆栈帧*并包含返回的地址传递给函数，并且该函数的本地变量的参数。 每次函数调用进行新的堆栈帧时推送到堆栈的顶部。 该函数返回时，会在堆栈中弹出堆栈帧。

每个线程都具有其自己的调用堆栈，表示该线程中进行的调用。

若要获取堆栈跟踪，请使用方法[ **GetStackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff548425)并[ **GetContextStackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff545748)。 可以使用打印堆栈跟踪[ **OutputStackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff553252)并[ **OutputContextStackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff553203)。

 

 





