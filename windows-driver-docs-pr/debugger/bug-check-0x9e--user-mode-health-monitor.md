---
title: Bug 检查 0x9E USER_MODE_HEALTH_MONITOR
description: USER_MODE_HEALTH_MONITOR bug 检查具有 0x0000009E 值。 此 bug 检查表示一个或多个关键的用户模式组件无法满足的运行状况检查。
ms.assetid: 5ad56234-5150-4acb-828d-198c2e5fb9b6
keywords:
- Bug 检查 0x9E USER_MODE_HEALTH_MONITOR
- USER_MODE_HEALTH_MONITOR
ms.date: 12/26/2018
topic_type:
- apiref
api_name:
- USER_MODE_HEALTH_MONITOR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8c261bdac649de71ff8948a6d72d9753bad26b3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367260"
---
# <a name="bug-check-0x9e-usermodehealthmonitor"></a>Bug 检查 0x9E：用户\_模式下\_运行状况\_监视器


用户\_模式下\_运行状况\_监视器 bug 检查的值为 0x0000009E。 此 bug 检查表示一个或多个关键的用户模式组件无法满足的运行状况检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="usermodehealthmonitor-parameters"></a>用户\_模式下\_运行状况\_监视器参数


|参数|描述|
|--- |--- |
|1|无法满足运行状况检查超时配置中的过程|
|2|运行状况监视超时，以秒为单位|
|3|监视程序源。 与过程结合使用地址有助于识别哪个子组件已创建此监视器。 下面列出的值。|
|4|保留|
 

**VALUES** 

```text
        0  : WatchdogSourceDefault
              Source was not specified
        1  : WatchdogSourceRhsCleanup
              Monitors that RHS process goes away when
              terminating on graceful exit
        2  : WatchdogSourceRhsResourceDeadlockBugcheckNow
              RHS was asked to immediately bugcheck machine
              on resource deadlock
        3  : WatchdogSourceRhsExceptionFromResource
              Resource has leaked unhandled exception from an entry point,
              RHS is terminating and this watchdog monitors that
              process will go away
        4  : WatchdogSourceRhsUnhandledException
              Unhandled exception in RHS.
              RHS is terminating and this watchdog monitors that
              process will go away
        5  : WatchdogSourceRhsResourceDeadlock
              Monitors that RHS process goes away when
              terminating on resource deadlock
        6  : WatchdogSourceRhsResourceTypeDeadlock
              Monitors that RHS process goes away when
              terminating on resource type deadlock
        7  : WatchdogSourceClussvcUnhandledException
              Unhandled exception in clussvc.
              clussvc is terminating and this watchdog monitors that
              process will go away
        8  : WatchdogSourceClussvcBugcheckMessageRecieved
              Another cluster node has sent message asking to bugcheck this node.
        9  : WatchdogSourceClussvcWatchdogBugcheck
              User mode watchdog has expired and created netft watchdog
              to bugchecked the node.
       0xA : WatchdogSourceClussvcIsAlive
              Cluster service sends heartbeat to netft every 500 millseconds.
              By default, netft expects at least 1 heartbeat per second.
              If this watchdog was triggered that means clussvc is not getting
              CPU to send heartbeats.
      0x65 : WatchdogSourceRhsResourceDeadlockPhysicalDisk
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x66 : WatchdogSourceRhsResourceDeadlockStoragePool
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x67 : WatchdogSourceRhsResourceDeadlockFileServer
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x68 : WatchdogSourceRhsResourceDeadlockSODAFileServer
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x69 : WatchdogSourceRhsResourceDeadlockStorageReplica
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x6A : WatchdogSourceRhsResourceDeadlockStorageQOS
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x6B : WatchdogSourceRhsResourceDeadlockStorageNFSV2
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0xC9 : WatchdogSourceRhsResourceTypeDeadlockPhysicalDisk
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCA : WatchdogSourceRhsResourceTypeDeadlockStoragePool
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCB : WatchdogSourceRhsResourceTypeDeadlockFileServer
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCC : WatchdogSourceRhsResourceTypeDeadlockSODAFileServer
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCD : WatchdogSourceRhsResourceTypeDeadlockStorageReplica
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCE : WatchdogSourceRhsResourceTypeDeadlockStorageQOS
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCF : WatchdogSourceRhsResourceTypeDeadlockStorageNFSV2
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
```

<a name="cause"></a>原因
-----

硬件机制，例如监视程序计时器可检测到不执行基本的核心服务。 但是，资源不足问题 （包括内存泄漏、 锁争用和计划优先级配置不正确） 可能会阻止关键用户模式组件没有阻止延缓的过程调用 (Dpc) 或清空非页面缓冲池。

内核组件可以通过定期监视关键应用程序扩展到用户模式下的监视程序计时器功能。 此 bug 检查指示用户模式下运行状况检查失败会阻止正常关闭的方式。 此 bug 检查还原关键服务通过重新启动或启用应用程序故障转移到其他服务器。



 

 




