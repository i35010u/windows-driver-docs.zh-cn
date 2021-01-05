---
title: Bug 检查 0x9E USER_MODE_HEALTH_MONITOR
description: USER_MODE_HEALTH_MONITOR bug 检查的值为0x0000009E。 此 bug 检查指示一个或多个关键用户模式组件无法满足运行状况检查。
keywords:
- Bug 检查 0x9E USER_MODE_HEALTH_MONITOR
- USER_MODE_HEALTH_MONITOR
ms.date: 12/22/2020
topic_type:
- apiref
api_name:
- USER_MODE_HEALTH_MONITOR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fa1672d81c71bcc0d12b988ac8d48e2b4b2da85
ms.sourcegitcommit: 7bdf85c72841fbc2093c315f900c69d2eef6e3e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2020
ms.locfileid: "97757894"
---
# <a name="bug-check-0x9e-user_mode_health_monitor"></a>Bug 检查0x9E：用户 \_ 模式 \_ 运行状况 \_ 监视器

用户 \_ 模式 \_ 运行状况 \_ 监视器 bug 检查的值为0x0000009E。 此 bug 检查指示一个或多个关键用户模式组件无法满足运行状况检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="user_mode_health_monitor-parameters"></a>用户 \_ 模式 \_ 运行状况 \_ 监视器参数


|参数|说明|
|--- |--- |
|1|在配置的超时时间内未能满足健康检查的过程|
|2|运行状况监视超时（以秒为单位）|
|3|监视源。 与进程地址组合在一起有助于识别哪个子组件已创建此监视器。 下面列出的值。|
|4|保留|

## <a name="values"></a>VALUES

<pre>
0  : WatchdogSourceDefault
      Source was not specified
1  : WatchdogSourceRhsCleanup
      Monitors that RHS (Resource Hosting Subsystem) process goes away when
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

硬件机制（如监视定时器）可以检测到基本内核服务没有执行。 但是，资源不足问题 (包括内存泄漏、锁争用和计划优先级配置错误) 可以阻止关键用户模式组件，而不会阻止 (Dpc) 或排出非分页池的延迟过程调用。

内核组件可以通过定期监视关键应用程序，将监视程序计时器功能扩展到用户模式。 此 bug 检查表明用户模式运行状况检查失败，以防正常关闭。 此 bug 检查通过重新启动或启用到其他服务器的应用程序故障转移来还原关键服务。

与所有 bug 检查一样，使用系统事件日志查找在时间段内停止代码之前的事件。 应检查日志中立即执行 bug 检查的事件，以获取有关可能原因的信息。

## <a name="see-also"></a>另请参阅

[使用 Windows 错误报告排查故障转移群集问题](/windows-server/failover-clustering/troubleshooting-using-wer-reports)

[故障转移群集系统日志事件](/windows-server/failover-clustering/system-events)

[Bug 检查 0x1C9 USER_MODE_HEALTH_MONITOR_LIVEDUMP](bug-check-0x1c9--user-mode-health-monitor-livedump.md)

[Bug 检查代码参考](bug-check-code-reference2.md)
