---
Description: WinUSB 电源管理
title: WinUSB 电源管理
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: e84ef44620283c82d1ce7b2c2967c3e02764d765
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385349"
---
# <a name="winusb-power-management"></a>WinUSB 电源管理


WinUSB 电源管理使用 KMDF 状态机。 电源策略通过调用[ **WinUsb\_SetPowerPolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpowerpolicy)。

若要修改的 WinUSB power 行为，可在设备 INF 中修改默认注册表设置。 这些值必须通过添加中的值写入到设备注册表中的特定位置**硬件。AddReg** INF 部分。

可以修改 power 行为的设备 INF 中指定以下列表所述的注册表值。

<a href="" id="system-wake"></a>**系统唤醒**  
此功能受**SystemWakeEnabled** DWORD 注册表设置。 此值指示是否应允许设备唤醒系统从低功耗状态。

```INF
HKR,,SystemWakeEnabled,0x00010001,1
```

-   值为零或不存在此值指示该设备不能将系统唤醒。
-   若要允许设备唤醒系统，请设置**SystemWakeEnabled**为非零值。 在设备中的复选框**属性**页会自动启用，以便用户可以重写该设置。

**请注意**  Changing **SystemWakeEnabled**设置对产生任何影响选择性挂起，此注册表值仅适用于系统挂起。

 

<a href="" id="selective-suspend"></a>**选择性挂起**  
选择性挂起任何多个系统或 WinUSB 设置可以禁用。 单个设置不能强制 WinUSB 若要启用选择性挂起。

以下电源中指定的策略设置[ **WinUsb\_SetPowerPolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpowerpolicy)的*PolicyType*参数会影响选择性的行为挂起：

-   自动\_挂起时设置为零，但它不会不设置设备选择性挂起模式。
-   挂起\_延迟设置当设备变为空闲状态与 WinUSB 当请求进入选择性设备之间的时间挂起。

下表显示了注册表项如何影响选择性挂起功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表项</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>DeviceIdleEnabled</strong></td>
<td>这是一个 DWORD 值。 此注册表值指示设备是否能够在断电时空闲 （选择性挂起）。
<ul>
<li>值为零或不存在此值指示该设备不支持所提供支持向下空闲时。</li>
<li>一个非零值指示正在提供支持下，在该设备支持空闲。</li>
<li>如果未设置 DeviceIdleEnabled，被忽略 AUTO_SUSPEND 电源策略设置的值。</li>
</ul>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DeviceIdleEnabled,0x00010001,1</code></pre></td>
</tr>
<tr class="even">
<td><strong>DeviceIdleIgnoreWakeEnable</strong></td>
<td>它设置为非零值时，挂起设备，即使它不支持 RemoteWake。</td>
</tr>
<tr class="odd">
<td><strong>UserSetDeviceIdleEnabled</strong></td>
<td>此值是一个 DWORD 值。 此注册表值，该值指示是否应在设备中启用一个复选框<strong>属性</strong>页，允许用户重写的空闲状态的默认值。 当<strong>UserSetDeviceIdleEnabled</strong>设置为非零值启用复选框，用户可以禁用设备空闲时关闭。 值为零或不存在此值指示未启用复选框。
<ul>
<li>如果用户禁用设备电源节省量，则忽略 AUTO_SUSPEND 电源策略设置的值。</li>
<li>如果用户启用设备能源节约，然后 AUTO_SUSPEND 的值用于确定是否将挂起设备空闲时。</li>
</ul>
<p><strong>UserSetDeviceIdleEnabled</strong>如果，则忽略<strong>DeviceIdleEnabled</strong>未设置。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,UserSetDeviceIdleEnabled,0x00010001,1</code></pre></td>
</tr>
<tr class="even">
<td><strong>DefaultIdleState</strong></td>
<td>这是一个 DWORD 值。 此注册表值设置 AUTO_SUSPEND 电源策略设置的默认值。 此注册表项用于启用或禁用选择性挂起一个句柄未打开到设备时。
<ul>
<li>值为零或不存在此值指示，默认情况下，设备不会挂起空闲时。 允许设备挂起空闲时，仅当启用 AUTO_SUSPEND 电源策略时。</li>
<li>一个非零值指示默认情况下设备允许空闲时挂起。</li>
</ul>
<p>如果忽略此值<strong>DeviceIdleEnabled</strong>未设置。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DefaultIdleState,0x00010001,1</code></pre></td>
</tr>
<tr class="odd">
<td><strong>DefaultIdleTimeout</strong></td>
<td>这是一个 DWORD 值。 此注册表值设置 SUSPEND_DELAY 电源策略设置的默认状态。
<p>值表示以毫秒为单位确定设备处于空闲状态之前要等待的时间量。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DefaultIdleTimeout,0x00010001,100</code></pre></td>
</tr>
</tbody>
</table>

 

<a href="" id="detecting-idle"></a>**检测空闲**  
所有写入并控制传输都强制设备插入**D0**电源状态和重置空闲计时器。 在终结点队列不是电源管理。 读取请求时就将其提交唤醒设备。 但是，可以在设备进入空闲状态，而等待的读取的请求。

## <a name="related-topics"></a>相关主题
[WinUSB 体系结构和模块](winusb-architecture.md)  
[选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)  
[WinUSB (Winusb.sys) 安装](winusb-installation.md)  
[如何通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[针对管道策略修改 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  
[**WinUsb\_GetPowerPolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpowerpolicy)  
[**WinUsb\_SetPowerPolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpowerpolicy)  



