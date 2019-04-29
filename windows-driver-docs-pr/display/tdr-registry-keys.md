---
title: 超时检测和恢复 (TDR) 注册表项
description: 以下 TDR （超时检测和恢复）-与相关的注册表项均显示驱动程序开发测试或调试目的。
ms.assetid: 77b8b2aa-0821-4297-a1e4-57894bd4181f
keywords:
- TDR （超时检测和恢复）
- WDK 显示开发
ms.date: 10/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1130c27a3109ed22211b9fb62e6f6e86d5fcfc01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362715"
---
# <a name="timeout-detection-and-recovery-tdr-registry-keys"></a>超时检测和恢复 (TDR) 注册表项

可以使用以下 TDR （超时检测和恢复） 的相关注册表项进行测试或调试目的。 也就是说，它们应不被操作外部目标测试或调试任何应用程序。

-   **TdrLevel**

    指定恢复的初始级别。 默认值是在超时时恢复 (**TdrLevelRecover**)。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrLevel
    ValueType : REG_DWORD
    ValueData : TdrLevelOff (0) - Detection disabled 
     TdrLevelBugcheck (1) - Bug check on detected timeout, for example, no recovery.
     TdrLevelRecoverVGA (2) - Recover to VGA (not implemented).
     TdrLevelRecover (3) - Recover on timeout. This is the default value.
    ```

-   **TdrDelay**

    指定 GPU 可以延迟 preempt 请求在 GPU 计划程序中的秒的数。 这是有效的超时阈值。 默认值为 2 秒。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrDelay
    ValueType : REG_DWORD
    ValueData : Number of seconds to delay. 2 seconds is the default value.
    ```

-   **TdrDdiDelay**

    指定操作系统允许将保留该驱动程序的线程的秒数。 在指定时间后操作系统 bug 检查代码视频的计算机\_TDR\_失败 (0x116)。 默认值为 5 秒。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrDdiDelay
    ValueType : REG_DWORD
    ValueData : Number of seconds to leave the driver. 5 seconds is the default value.
    ```

-   **TdrTestMode**

    保留。 不使用。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrTestMode
    ValueType : REG_DWORD
    ValueData : Do not use.
    ```

-   **TdrDebugMode**

    指定与调试相关 TDR 过程的行为。 默认值是 TDR\_调试\_模式\_恢复\_否\_提示，指示不中断调试器。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrDebugMode
    ValueType : REG_DWORD
    ValueData : TDR_DEBUG_MODE_OFF (0) - Break to kernel debugger before the recovery to allow investigation of the timeout. 
     TDR_DEBUG_MODE_IGNORE_TIMEOUT (1) - Ignore any timeout.
     TDR_DEBUG_MODE_RECOVER_NO_PROMPT (2) - Recover without breaking into the debugger. This is the default value.
     TDR_DEBUG_MODE_RECOVER_UNCONDITIONAL (3) - Recover even if some recovery conditions are not met (for example, recover on consecutive timeouts).
    ```

-   **TdrLimitTime**

    支持 Windows Server 2008 和更高版本和 Service Pack 1 (SP1) 和更高版本的 Windows Vista 中。

    指定在其中的默认时间有特定数量的 TDRs (由指定**TdrLimitCount**密钥) 允许而不发生崩溃的计算机。 默认值为 60 秒。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrLimitTime
    ValueType : REG_DWORD
    ValueData : Number of seconds before crashing. 60 seconds is the default value.
    ```

-   **TdrLimitCount**

    支持 Windows Server 2008 和更高版本和 Service Pack 1 (SP1) 和更高版本的 Windows Vista 中。

    指定由指定的时间内允许的 TDRs (0x117) 的默认数目**TdrLimitTime**密钥而不发生崩溃的计算机。 默认值为 5。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrLimitCount
    ValueType : REG_DWORD
    ValueData : Number of TDRs before crashing. The default value is 5.
    ```

