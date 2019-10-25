---
title: 选择加入即时空闲超时
description: 本主题讨论在不再需要电源时 Windows 8 驱动程序可用于选择立即断电状态的 ImmediateIdle 注册表值。
ms.assetid: 43721EC9-4901-4C68-9CCC-E0A71BF2200E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 020b439b78502ac87841d8062810cf9aed9dad26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833280"
---
# <a name="span-idaudioimmediate_idle_timeout_opt-inspanimmediate-idle-timeout-opt-in"></a><span id="audio.immediate_idle_timeout_opt-in"></span>立即空闲超时选择加入


本主题讨论在不再需要电源时 Windows 8 驱动程序可用于选择立即断电状态的*ImmediateIdle*注册表值。

除了[PortCls 注册表电源设置](portcls-registry-power-settings.md)中所述的默认电源设置外，Windows 8 还引入了一个新的注册表值，它也位于关联驱动程序的 PowerSettings 注册表项中。 例如，如果你的驱动程序的密钥是 &lt;UVXYZ&gt;，则会在 Windows 注册表的以下路径中找到该驱动程序的电源设置信息：

HKLM\\System\\CurrentControlSet\\控件\\类\\{4D36E96C-E325-11CE-BFC1-08002BE10318}\\&lt;UVXYZ&gt;\\PowerSettings。

除了[PortCls 注册表电源设置](portcls-registry-power-settings.md)中显示的默认电源设置值外，还会在*ImmediateIdle*中包括以下行：

``` syntax
"ImmediateIdle"=hex:00,00,00,00  
```

*ImmediateIdle*的数据类型为 REG\_DWORD，其默认值为 "0"，这等于 FALSE。 在前面的语法片段中，十六进制值 "0" 表示设备在不再需要电源时不会立即关闭。

要使你的驱动程序选择立即关机状态，当不再需要电源时，你必须使用以下语法：

``` syntax
"ImmediateIdle"=hex:01,00,00,00  
```

在前面的语法片段中，十六进制值 "1" 相当于 TRUE，这意味着当不再需要电源时，设备将立即断电。

当运行时电源管理框架调用**DevicePowerRequired**方法的回调时，如果设备不再需要电源，则 PortCls 会为*IdlePowerState*指示的 D 状态请求设备电源 IRP注册表值。 如果未提供任何状态，则使用默认值 D3。

如果驱动程序选取为立即空闲电源管理，则必须确保系统的电源引擎插件（PEP）包含防止不必要的逻辑，并为立即收到的 Irp 连续和向下供电。 应应用某些驻留规则，以使设备保持开机状态以进行批次 i/o 请求。

此外，在 Windows 7 中引入的新接口允许驱动程序以编程方式启用或禁用空闲电源管理，当驱动程序未选择立即空闲电源管理时，将继续执行。 这是通过[**IPortClsPower：： SetIdlePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspower-setidlepowermanagement)方法完成的，它将覆盖注册表中的设置，但*ImmediateIdle*设置为1（TRUE）的情况除外。

 

 




