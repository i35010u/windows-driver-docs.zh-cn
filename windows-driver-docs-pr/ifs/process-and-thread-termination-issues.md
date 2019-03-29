---
title: 进程和线程终止问题
description: 进程和线程终止问题
ms.assetid: 11b38c60-1bd8-4f1b-a80e-14a93e4ac474
keywords:
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统、 进程和线程终止
- 进程终止 WDK 文件系统
- 线程终止 WDK 文件系统
- 终止进程或线程 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02d3f917b21439da077cded5461b9b7a01385245
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566796"
---
# <a name="process-and-thread-termination-issues"></a>进程和线程终止问题


## <span id="ddk_process_and_thread_termination_issues_if"></span><span id="DDK_PROCESS_AND_THREAD_TERMINATION_ISSUES_IF"></span>


存储与特定用户相关的状态信息的文件系统可能需要监视的进程和线程终止条件。 例如，与特定用户相关联的加密密钥可能需要终止，在放弃 （无论是计划内还是过早） 的专用的控件应用程序。 有关用于处理这些条件的例程的详细信息，请参阅[ **PsSetCreateProcessNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559951)并[ **PsSetCreateThreadNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559954).

 

 




