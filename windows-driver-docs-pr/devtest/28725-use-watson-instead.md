---
title: C28725
description: 警告 C28725 使用 Watson 而不是此 SetUnhandledExceptionFilter。
ms.assetid: 826B4BD2-226C-4986-86B3-E9DFD62DB225
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28725
ms.openlocfilehash: fa5ac1006e3155c6b9e9702da6391d54045dbe23
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382127"
---
# <a name="c28725"></a>C28725


警告 C28725：使用 Watson 而不是此 SetUnhandledExceptionFilter

当应用程序使用 [**SetUnhandledExceptionFilter 函数**](/windows/desktop/api/errhandlingapi/nf-errhandlingapi-setunhandledexceptionfilter)时，将报告此警告。 函数可用于取代进程的每个线程的顶级异常处理程序。 默认情况下，系统会将未经处理的异常传递给 [Windows 错误报告](/windows/desktop/wer/windows-error-reporting) (WER) 。 为了安全起见，请参阅 [使用 WER](/windows/desktop/wer/using-wer)。

 

