---
title: 原始接口
description: 原始接口
ms.assetid: 78f1e722-c2bd-4232-96f1-71df7e6ece23
keywords:
- 游戏杆 WDK HID，接口
- 虚拟游戏杆驱动程序 WDK HID，接口
- VJoyD WDK HID 接口
- WDK 游戏杆接口
- 游戏杆 WDK HID，回调
- 虚拟游戏杆驱动程序 WDK HID，回调
- VJoyD WDK HID 回调
- 回调 WDK 游戏杆
- 轮询 WDK 游戏杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f3207028979b5fd028a9303155e988e764255d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545542"
---
#  <a name="original-interface"></a>原始接口





以下的游戏杆微型驱动程序回调是特定于原始接口：

-   一个[轮询回调](polling-callback.md)返回游戏杆位置和按钮的信息。

-   一个[配置管理器回调](configuration-manager-callback.md)处理在 Windows 95 中的配置管理器消息。

-   一个[硬件功能回调](hardware-capabilities-callback.md)用于处理请求的游戏杆功能。

-   一个[游戏杆标识回调](joystick-identification-callback.md)VJoyD 用于通知的游戏杆，微型驱动程序应响应。

必须将四个特定于游戏杆的回叫注册 VJoyD VJOYD\_注册\_设备\_驱动程序服务，然后再返回处理 SYS\_动态\_设备\_INIT 消息。 EAX 必须指向轮询例程，EBX （配置处理程序）、 （功能回调），ECX 和 EDX （标识例程）。 游戏杆微型驱动程序注册序列的示例如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Mov</p></td>
<td><p>eax offset32 _PollRoutine@8</p></td>
</tr>
<tr class="even">
<td><p>Mov</p></td>
<td><p>ebx，offset32 _CfgRoutine</p></td>
</tr>
<tr class="odd">
<td><p>Mov</p></td>
<td><p>ecx offset32 _HWCapsRoutine@8</p></td>
</tr>
<tr class="even">
<td><p>Mov</p></td>
<td><p>edx offset32 _JoyIdRoutine@8</p></td>
</tr>
<tr class="odd">
<td><p>VxDcall</p></td>
<td><p>VJOYD_Register_Device_Driver</p></td>
</tr>
</tbody>
</table>

 

除了在注册时，微型驱动程序可以执行在此时间的任何其他初始化。 游戏杆微型驱动程序模型不需要任何特定操作以响应 SYS\_动态\_设备\_退出，但 VxD 可能仍将使用它的最后一个内部清理。

 

 




