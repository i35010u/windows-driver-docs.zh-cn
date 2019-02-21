---
title: DirectX 5.0 接口
description: DirectX 5.0 接口
ms.assetid: 416a9187-d64f-48a4-8868-fd5158d58a25
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
- 游戏杆 WDK HID，版本
- VJoyD WDK HID 版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45280843a3e3900821a27bb363a2a1e4d4bba022
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522748"
---
#  <a name="directx-50-interface"></a>DirectX 5.0 接口





VJoyD 和任何其早期版本无法识别的 DirectX 5.0 和更高版本的接口。 因此，它是命令性微型驱动程序，它将尝试注册之前会检查 VJoyD 的版本。 VJoyD 不支持标准版消息。 因此，您必须 VJoyD 要实现这一点，手动获取设备描述符块 (DDB)，然后检查在 DDB 中标记的版本。 有关如何实现此的详细信息，请参阅示例的示例驱动程序。 请注意在 DDB 中标记的版本不是标记为版本资源中的版本相同。

显著扩展依据微型驱动程序注册其回调过程和它在 DirectX 5.0 中启动。

VJoyD，与之前一样或外部所有者 （如 HID 堆栈上） 可以加载微型驱动程序。 当 VJoyD 加载设备时，它需要微型驱动程序以注册其自身使用 VJoyD VJOYD\_注册\_设备\_驱动程序服务。 但是，微型驱动程序可能会收到三个系统控制消息，应提示它没有正确注册。 第一种是 SYS\_动态\_设备\_INIT 消息，如果 VJoyD 加载它之前不会加载 VxD 接收微型驱动程序。 这作为为注册的原始接口使用相同的机制。 因为它是一个全新的 VxD 负载，任何定义的 INIT 部分可用。 在收到此消息，VxD 执行内部初始化并 VJoyD 然后注册。

如果应用程序已加载微型驱动程序 （例如，如果应用程序已加载以使用专用的 IOCTL 接口），它不会收到此消息试 VJoyD 加载它时。 在这些情况下，Windows 98 发出 SYS\_动态\_设备\_REINIT 消息和微型驱动程序，在响应中，应注册 VJoyD。 由于这不是一个全新的 VxD 负载，INIT 部分不再可用。 对于不运行在 Windows 98 的微型驱动程序，VJoyD 采用缺乏响应加载作为微型驱动程序已加载的 VxD。 VJoyD 发出定向的系统控制消息 BEGIN\_保留\_专用\_系统\_控件，微型驱动程序应注册响应中。

加载时间在注册时，除了 VJoyD 现在接受新的注册类型时驱动程序检测到更改，它可以驱动的设备的状态。 除了回调，DirectX 5.0 接口允许各种控制参数和设置注册的设备说明。 这包括设备 （随附的校准信息），但它可以进行更改以适应它检测到的任何其他设备的完整说明。

DirectX 5.0 和更高版本的接口的游戏杆微型驱动程序回调包含控制回调、 轮询回调，以及强制反馈回叫。 若要适应这些变化，VJoyD VJOYD\_注册\_设备\_驱动程序服务重载，以便 EAX 保存 0xFFFFFFFF，以指示新注册中使用，并且 ECX 保留一个指向一个结构，其中包含参数。 EBX 和 EDX 中的值是未定义，驱动程序可能会假定 EBX 返回从调用未被破坏。

下面的示例演示游戏杆微型驱动程序注册序列：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Mov</p></td>
<td><p>eax 0ffffffffh</p></td>
</tr>
<tr class="even">
<td><p>Mov</p></td>
<td><p>ecx offset32 RegData</p></td>
</tr>
<tr class="odd">
<td><p>VxDcall</p></td>
<td><p>VJOYD_Register_Device_Driver</p></td>
</tr>
</tbody>
</table>

 

[ **VJREGDRVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff543581)结构传递到新注册。

**DwFunction** VJREGDRVINFO 结构的成员必须为 VJRT\_加载; 保留所有其他值。 VJRT\_LOADED，注册用于在原始的界面中，即在微型驱动程序加载到响应中的回调传递给 VJoyD 方式相同，新界面中使用。

控制回调和轮询回调将合并成单个表，因为所有驱动程序必须提供控制回调，而极少设备是仅输出 （并因此不需要轮询回调）。 使用注册这些回调[ **VJPOLLREG** ](https://msdn.microsoft.com/library/windows/hardware/ff543577)结构。

**LpCfg** VJPOLLREG 结构的成员将指向标准配置管理器回叫，与在原始界面 CfgRoutine 完全相同。 主要区别是 VJoyD 调用相应的配置管理器回调。 VJoyD 链接到已安装的设备节点的驱动程序，并调用此回调以通知配置管理器活动的驱动程序。 上一接口调用所有已加载的驱动程序用于每个配置管理器回叫，DirectX 5.0 和更高版本的接口仅调用一个驱动程序而它已链接到设备节点的已更改。 此外，不加载该驱动程序时，configuration manager 活动可能会发生这种情况，因为 VJoyD 实现基元缓存系统，以便在加载时启动设备节点后，如果此设备节点的通知驱动程序。

由于始终为调用在其资源分配驱动程序，因此它们不应检查默认端口，以查找所需的资源。 遗憾的是，旧方法中的驱动程序，必须找到一些方法，可以使用上一接口也仍然可用。 这意味着，尽管 VJoyD 仅分配一组到单个驱动程序的资源，会加载任何旧驱动程序仍然可以使用未分配给它们的端口。 当已分配资源时，驱动程序应执行任何所需的设备，以确定设备状态的握手。

[*初始化*](https://msdn.microsoft.com/library/windows/hardware/ff541025)回调 (指向**fpInitialize** VJPOLLREG 结构中的成员) 将替换*JoyId*中的回调以前的接口。 主要区别在于，VJoyD 传递回该驱动程序设备过程中传递给 VJoyD 注册以便可以区分这些实例，如果该驱动程序支持多个设备任何设备实例标识。

**请注意**  如果你需要打开注册表项，则应使用[VJOYD\_OpenConfigKey\_服务](https://msdn.microsoft.com/library/windows/hardware/ff543545)并[VJOYD\_OpenTypeKey\_服务](https://msdn.microsoft.com/library/windows/hardware/ff543549)宏而不是直接打开注册表项。 使用这些服务宏可确保打开正确的注册表分支。 此外，支持的服务的宏将在将来版本的 DirectInput 时可能会以不同方式结构化的基础的注册表数据。

 

 

 




