---
description: WinUSB 电源管理
title: WinUSB 电源管理
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 19954b7c8f595c514013fd326926df36b794c95f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714858"
---
# <a name="winusb-power-management"></a>WinUSB 电源管理


WinUSB 使用 KMDF 状态机进行电源管理。 可以通过调用 [**WinUsb \_ SetPowerPolicy**](/windows/win32/api/winusb/nf-winusb-winusb_setpowerpolicy)管理电源策略。

为了修改 WinUSB 的电源行为，可以在设备的 INF 中修改默认注册表设置。 必须通过在 HW 中添加值，将这些值写入到注册表中的设备特定位置 **。** INF 的 AddReg 部分。

可在设备 INF 中指定以下列表中描述的注册表值，以修改电源行为。

<a href="" id="system-wake"></a>**系统唤醒**  
此功能由 **SystemWakeEnabled** DWORD 注册表设置控制。 此值指示是否应允许设备从低功耗状态唤醒系统。

```INF
HKR,,SystemWakeEnabled,0x00010001,1
```

-   如果值为零，或缺少该值，则表示不允许设备唤醒系统。
-   若要允许设备唤醒系统，请将 **SystemWakeEnabled** 设置为非零值。 "设备 **属性** " 页中的复选框会自动启用，以便用户可以重写该设置。

**注意**   更改**SystemWakeEnabled**设置对选择性挂起没有影响，此注册表值仅适用于系统挂起。

 

<a href="" id="selective-suspend"></a>**选择性挂起**  
可以通过多个系统或 WinUSB 设置中的任何一个禁用选择性挂起。 单个设置无法强制 WinUSB 启用选择性挂起。

在 [**WinUsb \_ SetPowerPolicy**](/windows/win32/api/winusb/nf-winusb-winusb_setpowerpolicy)的 *PolicyType* 参数中指定的以下电源策略设置将影响选择性挂起的行为：

-   \_当设置为零时，自动挂起会将设备设置为选择性挂起模式。
-   挂起 \_ 延迟设置设备进入空闲状态与 WinUSB 请求设备进入选择性挂起之间的时间间隔。

下表显示了注册表项如何影响选择性挂起功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表项</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>DeviceIdleEnabled</strong></td>
<td>这是一个 DWORD 值。 此注册表值指示在空闲 (选择性挂起) 时，设备是否能够关闭电源。
<ul>
<li>如果值为零，或缺少该值，则表示设备不支持在空闲时关闭电源。</li>
<li>非零值表示设备支持在空闲时关闭电源。</li>
<li>如果未设置 DeviceIdleEnabled，则将忽略 AUTO_SUSPEND 电源策略设置的值。</li>
</ul>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DeviceIdleEnabled,0x00010001,1</code></pre></td>
</tr>
<tr class="even">
<td><strong>DeviceIdleIgnoreWakeEnable</strong></td>
<td>如果设置为非零值，则会挂起设备，即使它不支持 RemoteWake。</td>
</tr>
<tr class="odd">
<td><strong>UserSetDeviceIdleEnabled</strong></td>
<td>此值为 DWORD 值。 此注册表值指示是否应在允许用户覆盖空闲默认值的 "设备 <strong>属性</strong> " 页中启用复选框。 如果将 <strong>UserSetDeviceIdleEnabled</strong> 设置为非零值，则会启用此复选框，用户可以禁用空闲时关闭设备电源。 如果值为零，或缺少该值，则指示复选框未启用。
<ul>
<li>如果用户禁用了设备节能，则将忽略 AUTO_SUSPEND 电源策略设置的值。</li>
<li>如果用户启用了设备节能，则使用 AUTO_SUSPEND 的值来确定在空闲时是否挂起设备。</li>
</ul>
<p>如果未设置<strong>DeviceIdleEnabled</strong> ，则将忽略<strong>UserSetDeviceIdleEnabled</strong> 。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,UserSetDeviceIdleEnabled,0x00010001,1</code></pre></td>
</tr>
<tr class="even">
<td><strong>DefaultIdleState</strong></td>
<td>这是一个 DWORD 值。 此注册表值设置 AUTO_SUSPEND 电源策略设置的默认值。 当句柄未打开到设备时，此注册表项用于启用或禁用选择性挂起。
<ul>
<li>如果值为零或缺少此值，则表示默认情况下，设备在空闲时不会挂起。 仅当启用了 AUTO_SUSPEND 电源策略时，才允许设备挂起。</li>
<li>非零值表示默认情况下，在空闲时允许挂起设备。</li>
</ul>
<p>如果未设置 <strong>DeviceIdleEnabled</strong> ，则忽略此值。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DefaultIdleState,0x00010001,1</code></pre></td>
</tr>
<tr class="odd">
<td><strong>DefaultIdleTimeout</strong></td>
<td>这是一个 DWORD 值。 此注册表值设置 SUSPEND_DELAY 电源策略设置的默认状态。
<p>值指示在确定设备处于空闲状态之前要等待的时间量（以毫秒为单位）。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DefaultIdleTimeout,0x00010001,100</code></pre></td>
</tr>
</tbody>
</table>

 

<a href="" id="detecting-idle"></a>**检测空闲**  
所有写入和控制传输都会强制设备进入 **D0** 电源状态并重置空闲计时器。 中的终结点队列不是电源管理的。 读取请求在提交设备时唤醒设备。 但是，在读取请求等待时，设备可能会处于空闲状态。

## <a name="related-topics"></a>相关主题
[WinUSB 体系结构和模块](winusb-architecture.md)  
[选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)  
[WinUSB (Winusb.sys) 安装](winusb-installation.md)  
[如何通过 WinUSB Functions 访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[用于修改管道策略的 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 函数](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  
[**WinUsb \_ GetPowerPolicy**](/windows/win32/api/winusb/nf-winusb-winusb_getpowerpolicy)  
[**WinUsb \_ SetPowerPolicy**](/windows/win32/api/winusb/nf-winusb-winusb_setpowerpolicy)