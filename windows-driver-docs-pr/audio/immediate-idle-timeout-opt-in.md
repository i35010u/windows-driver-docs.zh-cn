---
title: 选择加入即时空闲超时
description: 本主题讨论了 Windows 8 驱动程序可用来选择加入的即时电源关闭状态，如果不再需要 power ImmediateIdle 注册表值。
ms.assetid: 43721EC9-4901-4C68-9CCC-E0A71BF2200E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2de1bcac68be13f32c96039adea5e499282f640
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333504"
---
# <a name="span-idaudioimmediateidletimeoutopt-inspanimmediate-idle-timeout-opt-in"></a><span id="audio.immediate_idle_timeout_opt-in"></span>即时空闲超时参加


本主题讨论*ImmediateIdle* Windows 8 驱动程序可用来选择加入的即时电源关闭状态，如果不再需要 power 的注册表值。

除了默认电源设置中所述[PortCls 注册表电源设置](portcls-registry-power-settings.md)，Windows 8 引入了也位于关联的驱动程序的 PowerSettings 注册表项的新注册表值。 例如，如果有一个驱动程序时，其键是&lt;UVXYZ&gt;，则可能在 Windows 注册表中的以下路径中找到该驱动程序的电源设置信息：

HKLM\\System\\CurrentControlSet\\Control\\Class\\{4D36E96C-E325-11CE-BFC1-08002BE10318}\\&lt;UVXYZ&gt;\\PowerSettings.

除了默认的电源设置中显示的值和[PortCls 注册表电源设置](portcls-registry-power-settings.md)，还应包括下面一行*ImmediateIdle*:

``` syntax
"ImmediateIdle"=hex:00,00,00,00  
```

*ImmediateIdle*的数据类型为 REG\_DWORD 和其默认值为等于 FALSE 的"0"。 在上述语法片段中，"0"表示该设备将立即关闭电源时不再需要 power 的十六进制值。

为您的驱动程序，若要选择加入到即时电源关闭状态，当不再需要 power 时，必须使用以下语法：

``` syntax
"ImmediateIdle"=hex:01,00,00,00  
```

在前面的语法片段中，"1"的十六进制值相当于为 TRUE，并且它意味着，设备将立即关闭电源时不再需要 power。

运行时的电源管理框架时调用的回调**DevicePowerRequired**方法，指明该设备不再需要 power，PortCls 则 D 状态由指示请求设备电源IRP*IdlePowerState*注册表值。 如果未不提供任何状态，则使用 D3 的默认值。

如果选择在中即时空闲电源管理的驱动程序，它必须确保系统电源引擎插件 (PEP) 包含不必要地阻止所需的逻辑和持续向上和向下提供适配器支持的 Irp 接收即时连续的。 一些驻留规则应该应用为了保持设备的 I/O 请求批处理为提供支持。

此外，允许以编程方式启用或禁用空闲电源管理的驱动程序的 Windows 7 中引入的新接口继续时不中选择即时空闲电源管理驱动程序已被拒绝。 这是通过[ **IPortClsPower::SetIdlePowerManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff536875)方法，并且将覆盖在注册表中，除了在其中设置*ImmediateIdle*是设置为 1 (TRUE)。

 

 




