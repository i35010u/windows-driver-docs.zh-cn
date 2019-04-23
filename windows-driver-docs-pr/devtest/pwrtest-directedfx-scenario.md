---
title: PwrTest DirectedFx 方案
description: PwrTest 定向 Power Framework 方案旨在测试 PoFx v3 功能。
ms.assetid: edf70fce-4c2a-4747-854f-feb919e01324
ms.date: 03/27/2019
ms.custom: 19H1
ms.openlocfilehash: 24716ed7cc721c67340843f37d1285ddae9b6a7b
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905259"
---
# <a name="pwrtest-directedfx-scenario"></a>PwrTest DirectedFx 方案

PwrTest DirectedFx 方案旨在测试与使用的驱动程序的设备[定向电源管理框架 (DFx)](../kernel/introduction-to-the-directed-power-management-framework.md)。

用户提供要测试的设备和 （可选） 若要验证的设备电源状态的实例路径。

如果指定没有 D 状态，则此测试将验证设备未处于 D0。  若要查找的实例路径，请检查设备的属性在设备管理器。  或者，运行该测试不带任何选项来获取系统上的所有 DFx 支持的设备实例路径的列表。

此测试可以运行任何[现代备用](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)系统而不考虑其网络连接设置期间待机或它是否在交流或直流电源上。

对于指定的设备，请测试验证：

- 设备和父级之前必须关闭任何子设备支持 DFx。
- 设备已成功完成至少一个定向的 power 减少/增加。
- 完成向下定向的电源后，在设备进入正确的 D 状态。 （可选）

为每个周期，显示了测试：

- 系统处于空闲状态的复原能力的时间
- 时间该定向[最深运行时空闲平台状态 (DRIPS)](https://docs.microsoft.com/windows-hardware/design/device-experiences/prepare-hardware-for-modern-standby)未占用
    - 每个单个原因处于活动状态时间
- 各项统计信息和可选失败的原因的所有测试设备
    - `Device {Test Device} failed because device {Failed Device} {Failed Reason}`。
        - 是分页设备或调试的设备
        - 不支持 DFx
        - 已在组件上的约束
        - 失败调用关闭其 DFx 电源
- 每个广播树和参与者的所有设备

建议运行三个周期的测试以确保设备可以进行多个定向的 power 转换。  完成所有循环都后，在测试输出成功/失败周期总数。

如果在系统上的没有设备支持 DFx，该测试返回`Error retrieving list of available Directed Fx devices`。

## <a name="syntax"></a>语法

```
pwrtest /directedfx [/c:n] [/d:n] [/p:n] [/device(:n):path] [/?] 
```

**/c:**<em>n</em>  
指定了多少个周期 （1 为默认值） 运行。

**/d:**<em>n</em>  
指定周期之间的延迟时间 （以秒为单位; 60 是默认值）。

**/p:**<em>n</em>  
指定要保留在连接待机状态的时间 （以秒为单位; 300 是默认值）。

**/device:**<em>n</em>  
路径提供一个设备用以测试的实例路径。  
N 提供设备应由于定向 Fx 转换输入的可选设备电源状态。

**示例**

```
pwrtest /directedfx
```

## <a name="related-topics"></a>相关主题


[PwrTest 语法](pwrtest-syntax.md)

