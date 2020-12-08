---
title: 进程和线程终止问题
description: 进程和线程终止问题
keywords:
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统、进程和线程终止
- 处理终止 WDK 文件系统
- 线程终止 WDK 文件系统
- 终止的进程或线程 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f528757f7274bd4d6bf4a561e539494475dd7693
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832999"
---
# <a name="process-and-thread-termination-issues"></a>进程和线程终止问题


## <span id="ddk_process_and_thread_termination_issues_if"></span><span id="DDK_PROCESS_AND_THREAD_TERMINATION_ISSUES_IF"></span>


存储与特定用户相关的状态信息的文件系统可能需要监视进程和线程终止条件。 例如，可能需要在终止时丢弃与特定用户关联的加密密钥， (无论是计划内还是过早) 专用控制应用程序。 有关用于处理这些情况的例程的详细信息，请参阅 [**PsSetCreateProcessNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine) 和 [**PsSetCreateThreadNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)。

 

