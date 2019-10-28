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
ms.openlocfilehash: 8dea17e2a2f4d4218f5ec969dcd32632743d15fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841024"
---
# <a name="process-and-thread-termination-issues"></a>进程和线程终止问题


## <span id="ddk_process_and_thread_termination_issues_if"></span><span id="DDK_PROCESS_AND_THREAD_TERMINATION_ISSUES_IF"></span>


存储与特定用户相关的状态信息的文件系统可能需要监视进程和线程终止条件。 例如，与特定用户关联的加密密钥可能需要在专用控件应用程序的终止（无论是已计划还是过早）时被丢弃。 有关用于处理这些情况的例程的详细信息，请参阅[**PsSetCreateProcessNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)和[**PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)。

 

 




