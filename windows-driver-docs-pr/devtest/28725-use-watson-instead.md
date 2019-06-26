---
title: C28725
description: 警告而不是此 SetUnhandledExceptionFilter C28725 使用 Watson。
ms.assetid: 826B4BD2-226C-4986-86B3-E9DFD62DB225
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28725
ms.openlocfilehash: 33f105222db65259d2bcf62b82011f8bd54f8996
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371718"
---
# <a name="c28725"></a>C28725


警告 C28725:而不是此 SetUnhandledExceptionFilter 使用 Watson

当应用程序使用，将报告此警告[ **SetUnhandledExceptionFilter 函数**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-setunhandledexceptionfilter)。 该函数可用于取代进程的每个线程的顶级异常处理程序。 默认情况下，系统将传递到未经处理的异常[Windows 错误报告](https://docs.microsoft.com/windows/desktop/wer/windows-error-reporting)(WER)。 安全和方便起见，请参阅[使用 WER](https://docs.microsoft.com/windows/desktop/wer/using-wer)。

 

 





