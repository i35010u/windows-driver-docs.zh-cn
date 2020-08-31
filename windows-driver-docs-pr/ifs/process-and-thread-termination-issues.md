---
title: 进程和线程终止问题
description: 进程和线程终止问题
ms.assetid: 11b38c60-1bd8-4f1b-a80e-14a93e4ac474
keywords:
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统、进程和线程终止
- 处理终止 WDK 文件系统
- 线程终止 WDK 文件系统
- 终止的进程或线程 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c169bc754bf0580b187d824368892e3fe4059e07
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063260"
---
# <a name="process-and-thread-termination-issues"></a>进程和线程终止问题


## <span id="ddk_process_and_thread_termination_issues_if"></span><span id="DDK_PROCESS_AND_THREAD_TERMINATION_ISSUES_IF"></span>


存储与特定用户相关的状态信息的文件系统可能需要监视进程和线程终止条件。 例如，可能需要在终止时丢弃与特定用户关联的加密密钥， (无论是计划内还是过早) 专用控制应用程序。 有关用于处理这些情况的例程的详细信息，请参阅 [**PsSetCreateProcessNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine) 和 [**PsSetCreateThreadNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)。

 

