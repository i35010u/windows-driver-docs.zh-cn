---
title: 测试和调试 TDR
description: '用于测试和调试 TDR (超时检测和恢复的注册表项和 WHLK 测试) '
keywords:
- TDR 调试，驱动程序开发
- 超时检测和恢复调试，驱动程序开发
- TDR 测试，驱动程序开发
- 超时检测和恢复测试，驱动程序开发
- 注册表项，TDR，驱动程序开发
- 注册表项，超时检测和恢复，驱动程序开发
- WDK 显示开发
- TDR 测试，WHLK
- TDR 测试，Windows 硬件实验室工具包
ms.date: 10/06/2020
ms.localizationpriority: medium
ms.custom: contperf-fy21q2
ms.openlocfilehash: 6d6a688182353a40e81dbd49e1220019a0b2d432
ms.sourcegitcommit: 0b60dbbac80f1578b0217b7cffc5b72af755725f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99529857"
---
# <a name="testing-and-debugging-tdr"></a>测试和调试 TDR

## <a name="tdr-tests-in-whlk"></a>WHLK 中的 TDR 测试

[Windows 硬件实验室工具包](/windows-hardware/test/hlk/) (WHLK) 包含驱动程序开发人员可用于测试和调试的特定于 TDR 的测试。 例如，开发人员可以使用 [**SIMULATEPREEMPTION TDR**](/windows-hardware/test/hlk/testref/86be5032-cfcd-4ee5-a515-0e3ebc0cb6f4)手动触发 GPU TDR。 有关各种 TDR 相关测试的详细信息，请参阅 [**设备。**](/windows-hardware/test/hlk/testref/device-graphics)

## <a name="tdr-registry-keys-for-testing-and-debugging"></a>TDR 用于测试和调试的注册表项

只有在驱动程序开发过程中，开发人员才能使用以下 TDR (超时检测和恢复) 相关注册表项，以便进行测试或调试。

> [!NOTE]
> 这些注册表项不应由最终用户或在驱动程序开发过程中进行目标测试或调试的应用程序操作。

### <a name="tdrlevel"></a>TdrLevel

指定初始恢复级别。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
KeyValue  : TdrLevel
ValueType : REG_DWORD
ValueData : TdrLevelXxx (see the following table)
```

其中，TdrLevel *Xxx* 可以是以下值之一：

| 值 | 含义 |
| ----- | ------- |
| TdrLevelOff (0)  | 已禁用检测 |
| TdrLevelBugcheck (1)  | 检测到超时时检查 Bug例如，无恢复。 |
| TdrLevelRecoverVGA (2)  | 恢复到 VGA (未实现) 。 |
| TdrLevelRecover (3)  | 在超时时恢复。 这是默认值。 |

### <a name="tdrdelay"></a>TdrDelay

指定 GPU 可以延迟 GPU 计划程序的 preempt 请求的秒数。 这实际上是超时阈值。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
KeyValue  : TdrDelay
ValueType : REG_DWORD
ValueData : Number of seconds to delay. The default value is 2 seconds.
```

### <a name="tdrddidelay"></a>TdrDdiDelay

指定 OS 允许线程离开驱动程序的秒数。 在指定的时间后，操作系统 bug-使用代码 VIDEO_TDR_FAILURE (0x116) 检查计算机。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
KeyValue  : TdrDdiDelay
ValueType : REG_DWORD
ValueData : Number of seconds to leave the driver. The default value is 5 seconds.
```

### <a name="tdrdebugmode"></a>TdrDebugMode

指定 TDR 进程的与调试相关的行为。 默认值为 TDR_DEBUG_MODE_RECOVER_NO_PROMPT，指示不中断到调试器。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
KeyValue  : TdrDebugMode
ValueType : REG_DWORD
ValueData : TDR_DEBUG_MODE_XXX (see the following table)
```

| 值 | 含义 |
| ----- | ------- |
| TDR_DEBUG_MODE_OFF (0)  | 在恢复之前中断内核调试器，以允许调查超时。 |
| TDR_DEBUG_MODE_IGNORE_TIMEOUT (1)  | 忽略任何超时。 |
| TDR_DEBUG_MODE_RECOVER_NO_PROMPT (2)  | 在不中断调试器的情况下进行恢复。 这是默认值。 |
| TDR_DEBUG_MODE_RECOVER_UNCONDITIONAL (3)  | 即使未满足某些恢复条件，也进行恢复 (例如，在连续超时) 恢复。 |

### <a name="tdrlimittime"></a>TdrLimitTime

指定默认的时间，在此时间内允许由 **TdrLimitCount** 键) 指定的 tdr (，而不会使计算机崩溃。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
KeyValue  : TdrLimitTime
ValueType : REG_DWORD
ValueData : Number of seconds before crashing. The default value is 60 seconds.
```

### <a name="tdrlimitcount"></a>TdrLimitCount

指定在 **TdrLimitTime** 键指定的时间内允许 (0x117) 的默认数量，而不会使计算机崩溃。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
KeyValue  : TdrLimitCount
ValueType : REG_DWORD
ValueData : Number of TDRs before crashing. The default value is 5.
```

### <a name="tdrtestmode"></a>TdrTestMode

保留。 请勿使用。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
KeyValue  : TdrTestMode
ValueType : REG_DWORD
ValueData : Do not use.
```
