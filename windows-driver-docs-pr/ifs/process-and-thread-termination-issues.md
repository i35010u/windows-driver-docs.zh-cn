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
ms.openlocfilehash: 9f629acdc3e8c766e8738228972ea7614e225d90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385151"
---
# <a name="process-and-thread-termination-issues"></a>进程和线程终止问题


## <span id="ddk_process_and_thread_termination_issues_if"></span><span id="DDK_PROCESS_AND_THREAD_TERMINATION_ISSUES_IF"></span>


存储与特定用户相关的状态信息的文件系统可能需要监视的进程和线程终止条件。 例如，与特定用户相关联的加密密钥可能需要终止，在放弃 （无论是计划内还是过早） 的专用的控件应用程序。 有关用于处理这些条件的例程的详细信息，请参阅[ **PsSetCreateProcessNotifyRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)并[ **PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine).

 

 




