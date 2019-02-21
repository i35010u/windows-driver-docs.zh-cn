---
title: C28725
description: 警告而不是此 SetUnhandledExceptionFilter C28725 使用 Watson。
ms.assetid: 826B4BD2-226C-4986-86B3-E9DFD62DB225
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28725
ms.openlocfilehash: 467b727e7ffa20ea53e468898b5a302ecd5cd50d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519803"
---
# <a name="c28725"></a>C28725


警告 C28725:而不是此 SetUnhandledExceptionFilter 使用 Watson

当应用程序使用，将报告此警告[ **SetUnhandledExceptionFilter 函数**](https://msdn.microsoft.com/library/windows/desktop/ms680634)。 该函数可用于取代进程的每个线程的顶级异常处理程序。 默认情况下，系统将传递到未经处理的异常[Windows 错误报告](https://msdn.microsoft.com/library/windows/desktop/bb513641)(WER)。 安全和方便起见，请参阅[使用 WER](https://msdn.microsoft.com/library/windows/desktop/bb513616)。

 

 





