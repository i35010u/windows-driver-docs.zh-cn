---
title: DirectX 5.0 接口
description: DirectX 5.0 接口
keywords:
- 操纵杆 WDK HID，接口
- 虚拟游戏杆驱动程序 WDK HID，接口
- VJoyD WDK HID，接口
- 接口 WDK 操纵杆
- 操纵杆 WDK HID，回调
- 虚拟游戏杆驱动程序 WDK HID，回调
- VJoyD WDK HID，回调
- 回调 WDK 操纵杆
- 轮询 WDK 操纵杆
- 游戏杆 WDK HID，版本
- VJoyD WDK HID，版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb0ac98e1b888681ad6bd9e38e6659a74e186cce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814503"
---
#  <a name="directx-50-interface"></a>DirectX 5.0 接口





VJoyD 及其先前版本无法识别 DirectX 5.0 和更高版本的接口。 因此，微型驱动程序必须在尝试注册前检查 VJoyD 版本。 VJoyD 不支持标准版本消息。 因此，你必须获取设备描述符块 (DDB) 才能手动实现此目的，然后检查 DDB 中标记的版本。 有关如何实现此操作的详细信息，请参阅示例驱动程序示例。 请注意，DDB 中标记的版本与版本资源中标记的版本不同。

微型驱动程序注册其回调的过程会大幅扩展，并在 DirectX 5.0 中启动。

VJoyD （与之前一样）或外部所有者 (如 HID 堆栈) 可加载微型驱动程序。 当 VJoyD 加载设备时，它需要微型驱动程序使用 VJoyD VJOYD \_ 注册 \_ 设备 \_ 驱动程序服务进行注册。 但是，微型驱动程序可能会收到三个系统控制消息，这些消息会提示它注册。 第一种是 SYS \_ 动态 \_ 设备 \_ 初始消息，如果在 VJoyD 加载 VxD 之前未加载 VxD，微型驱动程序将收到该消息。 这与用于注册的原始接口使用相同的机制。 由于它是 VxD 的全新负载，因此任何已定义的 INIT 部分都可用。 收到此消息后，VxD 会执行内部初始化，然后注册到 VJoyD。

如果应用程序已加载微型驱动程序 (例如，如果应用程序已将其加载到使用) 专用 IOCTL 接口，则在 VJoyD 加载它时，它不会再次收到此消息。 在这种情况下，Windows 98 将发出 SYS \_ 动态 \_ 设备 \_ REINIT 消息，而微型驱动程序将在响应中注册 VJoyD。 由于这不是 VxD 的全新负载，INIT 部分将不再可用。 对于在 Windows 98 下不运行的微型驱动程序，VJoyD 将不会响应加载微型驱动程序，因为 VxD 已经加载。 VJoyD 发出定向系统控制消息 "开始 \_ 保留 \_ 专用 \_ 系统 \_ 控制"，微型驱动程序应在响应中注册此控制。

除了加载时间注册，当驱动程序检测到设备的状态发生更改时，VJoyD 现在会接受新的注册类型。 除了回调以外，DirectX 5.0 接口允许在注册时设置各种控制参数和设备说明。 这包括设备的完整描述 (完成后，校准信息) ，它可以更改以适合它检测到的任何其他设备。

DirectX 5.0 和更高版本接口的操纵杆微型驱动程序回调包括控件回调、轮询回调和强制反馈回调。 为了适应这些更改，VJoyD VJOYD \_ 注册 \_ 设备 \_ 驱动程序服务将被重载，以便 EAX 保留0xffffffff 以指示新注册正在使用中，并且 ECX 保存指向保存参数的结构的指针。 EBX 和 EDX 的值是不确定的，驱动程序可能会假设 EBX 从未损坏的调用返回。

下面的示例演示了操纵杆微型驱动程序注册顺序：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>mov</p></td>
<td><p>eax，0ffffffffh</p></td>
</tr>
<tr class="even">
<td><p>mov</p></td>
<td><p>ecx，offset32 RegData</p></td>
</tr>
<tr class="odd">
<td><p>VxDcall</p></td>
<td><p>VJOYD_Register_Device_Driver</p></td>
</tr>
</tbody>
</table>

 

[**VJREGDRVINFO**](/previous-versions/windows/hardware/drivers/ff543581(v=vs.85))结构会传递到新注册。

VJREGDRVINFO 结构的 **dwFunction** 成员必须是 VJRT 加载的 \_ ; 所有其他值都是保留值。 加载的 VJRT 在 \_ 新接口中使用的方式与在原始接口中使用注册的方式相同，即，将回调传递到 VJoyD 以响应正在加载的微型驱动程序。

控件回调和轮询回调合并为单个表，因为所有驱动程序都必须提供控件回调，并且极少的设备只 (输出，因此不需要轮询回调) 。 这些回调使用 [**VJPOLLREG**](/previous-versions/windows/hardware/drivers/ff543577(v=vs.85)) 结构注册。

VJPOLLREG 结构的 **lpCfg** 成员指向标准的 configuration manager 回调，与原始接口中的 CfgRoutine 完全相同。 主要区别在于，VJoyD 会根据需要调用 configuration manager 回调。 VJoyD 将驱动程序链接到已安装的设备节点，并调用此回调来告知 configuration manager 活动的驱动程序。 除了以前的接口（称为每个配置管理器回调的所有加载的驱动程序），DirectX 5.0 和更高版本的接口仅调用其链接到已更改的设备节点的一个驱动程序。 此外，由于在未加载驱动程序时可能会发生 configuration manager 活动，因此 VJoyD 实现了一种基元缓存系统，因此，如果设备节点已启动，则在加载此设备节点时，会通知该驱动程序。

由于驱动程序始终是为其资源分配而调用的，因此它们不应检查默认端口以查找所需的资源。 遗憾的是，必须找到某种方法来使用以前的接口的驱动程序仍以旧方法工作。 这意味着，当 VJoyD 仅将一组资源分配给单个驱动程序时，加载的任何旧驱动程序仍可以使用尚未分配给它们的端口。 分配资源后，驱动程序应执行设备需要的任何握手来确定设备状态。

VJPOLLREG 结构的 **fpInitialize** 成员指向的 [*初始化*](/previous-versions/ff541025(v=vs.85))回调 () 替换之前接口中的 *JoyId* 回调。 主要区别在于，VJoyD 会将设备传递到 VJoyD 的任何设备实例标识传递回驱动程序，以便在驱动程序支持多个设备时，可以区分实例。

**注意**   如果需要打开注册表项，则应使用 [VJOYD \_ OpenConfigKey \_ service](/previous-versions/ff543545(v=vs.85)) 和 [VJOYD \_ OpenTypeKey \_ 服务](/previous-versions/ff543549(v=vs.85)) 宏，而不是直接打开注册表项。 使用这些服务宏可确保打开正确的注册表分支。 此外，如果基础注册表数据的结构不同，则未来版本的 DirectInput 将支持服务宏。

 

 

