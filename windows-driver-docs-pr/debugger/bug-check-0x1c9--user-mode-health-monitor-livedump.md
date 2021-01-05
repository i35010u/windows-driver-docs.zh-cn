---
title: Bug 检查 0x1C9 USER_MODE_HEALTH_MONITOR_LIVEDUMP
description: USER_MODE_HEALTH_MONITOR_LIVEDUMP bug 检查的值为0x000001C9。 它表示一个或多个关键用户模式组件无法满足运行状况检查。
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
ms.openlocfilehash: 77832365e3b9b2abc777678ea44f767587cc9abc
ms.sourcegitcommit: 7bdf85c72841fbc2093c315f900c69d2eef6e3e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2020
ms.locfileid: "97757892"
---
# <a name="bug-check-0x1c9-user_mode_health_monitor_livedump"></a>Bug 检查0x1C9：用户 \_ 模式 \_ 运行状况 \_ 监视器 \_ LIVEDUMP

用户 \_ 模式 \_ 运行状况 \_ 监视器 \_ LIVEDUMP bug 检查的值为0x000001C9。 它表示一个或多个关键用户模式组件无法满足运行状况检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="user_mode_health_monitor_livedump-parameters"></a>用户 \_ 模式 \_ 运行状况 \_ 监视器 \_ LIVEDUMP 参数

|参数|说明|
|--- |--- |
|1| 在配置的超时时间内未能满足运行状况检查的进程。| 
|2| 运行状况监视超时 (秒) 。| 
|3| 监视源。 与进程地址结合，这有助于标识源。 请参见下面可能的值。 这些值与  [USER_MODE_HEALTH_MONITOR](bug-check-0x9e--user-mode-health-monitor.md)共享。| 
|4| 保留。 |

**监视器源值**

<pre>
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
</pre>

## <a name="cause"></a>原因
-----
一个或多个关键用户模式组件无法满足运行状况检查。

硬件机制（如监视定时器）可以检测到基本内核服务没有执行。 但是，资源不足的问题（包括内存泄漏、锁定争用和计划优先级配置错误）可能会阻止重要的用户模式组件，而不会阻止 Dpc 或排出非分页池。 

内核组件可以通过定期监视关键应用程序，将监视程序计时器功能扩展到用户模式。 此 livedump 表示用户模式运行状况检查失败，因此我们将尝试终止此应用程序，并在终止时停止监视。 如果终止未按时完成，则计算机将 bugchecked 它通过重新启动和/或允许应用程序故障转移到其他服务器来恢复关键服务。 

 (此代码永远不能用于实际错误检查;它用于标识实时转储。 ) 


## <a name="see-also"></a>另请参阅
----------

[使用 Windows 错误报告排查故障转移群集问题](/windows-server/failover-clustering/troubleshooting-using-wer-reports)

[故障转移群集系统日志事件](/windows-server/failover-clustering/system-events)

[Bug 检查 0x1C9 USER_MODE_HEALTH_MONITOR](bug-check-0x9e--user-mode-health-monitor.md)

[Bug 检查代码参考](bug-check-code-reference2.md)

