---
title: PwrTest DirectedFx 方案
description: PwrTest 定向的 Power Framework 方案旨在测试 PoFx v3 功能。
ms.date: 03/27/2019
ms.custom: 19H1
ms.openlocfilehash: ab4958d5016a64c21d7fdbd03bd268dca6e4d4bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838511"
---
# <a name="pwrtest-directedfx-scenario"></a>PwrTest DirectedFx 方案

PwrTest DirectedFx 方案旨在测试具有使用 [定向电源管理框架 (DFx) ](../kernel/introduction-to-the-directed-power-management-framework.md)的驱动程序的设备。

用户提供要测试的设备)  (的实例路径，以及要验证的设备电源状态（可选）。

如果未指定任何 D 状态，则测试将验证 (s) 设备是否未处于 D0 状态。  若要查找实例路径，请在设备管理器中检查设备的属性。  或者，运行没有选项的测试以获取系统上所有支持 DFx 的设备的实例路径列表。

可以在任何 [新式备用](/windows-hardware/design/device-experiences/modern-standby) 系统上运行此测试，而不考虑其在待机期间的网络连接设置，或者它是在 AC 还是 DC 电源上。

对于指定的设备，测试验证：

- 在父支持 DFx 之前必须关闭的设备和任何子设备。
- 设备已成功完成至少一个定向电源。
- 设备在完成定向电源关闭后进入正确的 D 状态。 （可选）

对于每个周期，测试显示：

- 系统处于空闲复原状态的时间
- 定向最 [深的运行时空闲平台状态 (DRIPS) ](/windows-hardware/design/device-experiences/prepare-hardware-for-modern-standby) 未占用的时间
    - 每个单独原因的激活时间
- 所有测试设备的单独统计信息和可选失败原因
    - `Device {Test Device} failed because device {Failed Device} {Failed Reason}`.
        - 为寻呼设备或调试设备
        - 不支持 DFx
        - 在组件上具有约束
        - 未能通过其 DFx 关机
- 每个广播树和所有参与者设备

建议为三个周期运行测试，以确保设备 () 可以进行多个定向的电源转换。  所有循环完成后，测试将输出成功/失败周期的总数。

如果系统上没有设备支持 DFx，则测试将返回 `Error retrieving list of available Directed Fx devices` 。

## <a name="syntax"></a>语法

```
pwrtest /directedfx [/c:n] [/d:n] [/p:n] [/device(:n):path] [/?] 
```

**/c：**<em>n</em>  
指定要运行的默认)  (1 的周期数。

**/d：**<em>n</em>  
指定周期 (之间的延迟时间，以秒为单位;60为默认) 。

**/p：**<em>n</em>  
指定保持连接备用 (的时间，以秒为单位）;300为默认) 。

**/device：**<em>n</em>  
路径提供要测试的设备的实例路径。  
N 提供设备因定向的 Fx 转换而应输入的可选设备电源状态。

**示例**

```
pwrtest /directedfx
```

## <a name="related-topics"></a>相关主题


[PwrTest 语法](pwrtest-syntax.md)
