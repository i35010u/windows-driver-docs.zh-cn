---
title: Bug 检查 0x1C9 USER_MODE_HEALTH_MONITOR_LIVEDUMP
description: USER_MODE_HEALTH_MONITOR_LIVEDUMP bug 检查具有 0x000001C9 值。 它表示一个或多个重要的用户模式组件无法满足的运行状况检查。
keywords:
- Bug 检查 0x1C9 USER_MODE_HEALTH_MONITOR_LIVEDUMP
- USER_MODE_HEALTH_MONITOR_LIVEDUMP
ms.date: 01/10/2019
topic_type:
- apiref
api_name:
- USER_MODE_HEALTH_MONITOR_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 19174125c5e7b9682e4e5bce8b2f29a1fb88167d
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743464"
---
# <a name="bug-check-0x1c9-usermodehealthmonitorlivedump"></a>Bug 检查 0x1C9:用户\_模式下\_运行状况\_监视器\_LIVEDUMP

用户\_模式下\_运行状况\_监视器\_LIVEDUMP bug 检查的值为 0x000001C9。 它表示一个或多个重要的用户模式组件无法满足的运行状况检查。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。
 

## <a name="usermodehealthmonitorlivedump-parameters"></a>用户\_模式下\_运行状况\_监视器\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 未能满足配置的超时时间内的运行状况检查的过程。| 
|2| 运行状况监视超时 （秒）。| 
|3| 监视程序源。 这有助于标识源与进程地址结合使用。 有关可能的值，请参阅下文。 这些值与共享[USER_MODE_HEALTH_MONITOR](bug-check-0x9e--user-mode-health-monitor.md)。| 
|4| 保留。 |

**监视器源值**

```
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

## <a name="cause"></a>原因
-----
一个或多个重要的用户模式组件无法满足的运行状况检查。
 
监视程序计时器之类的硬件机制可以检测到不执行基本的核心服务。 但是，资源不足问题，包括内存泄漏、 锁争用和计划优先级配置不正确，可能会阻止关键用户模式组件，而无需阻止 Dpc 或清空非分页缓冲的池。 

内核组件可以通过定期监视关键应用程序扩展到用户模式下的监视程序计时器功能。 此 livedump 指示用户模式下运行状况检查失败的方式，以便我们将尝试终止此应用程序，并将保留监视如果终止完成的时间。 如果终止未完成的时间，则计算机将的 bugchecked 它还原关键服务重新启动和/或允许应用程序故障转移到其他服务器。 

（此代码可以永远不会用于实际的执行错误检查; 它用于标识实时转储）。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

