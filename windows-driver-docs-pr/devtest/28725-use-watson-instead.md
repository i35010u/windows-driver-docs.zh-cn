---
title: C28725
description: 警告 C28725 使用 Watson 而不是此 SetUnhandledExceptionFilter。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28725
ms.openlocfilehash: 026defdf4dbec3512f1f80f96a0ea9565f4d6b29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841353"
---
# <a name="c28725"></a>C28725


警告 C28725：使用 Watson 而不是此 SetUnhandledExceptionFilter

当应用程序使用 [**SetUnhandledExceptionFilter 函数**](/windows/win32/api/errhandlingapi/nf-errhandlingapi-setunhandledexceptionfilter)时，将报告此警告。 函数可用于取代进程的每个线程的顶级异常处理程序。 默认情况下，系统会将未经处理的异常传递给 [Windows 错误报告](/windows/desktop/wer/windows-error-reporting) (WER) 。 为了安全起见，请参阅 [使用 WER](/windows/desktop/wer/using-wer)。

 

