---
title: 蓝牙核心驱动程序层和支持的功率转换
description: 下表总结了蓝牙核心驱动程序支持的设备和系统电源状态。
ms.assetid: 25A3598E-51A7-4B16-92F7-9D2F39177946
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58fbf752748e57c0fe0017d902d942474d0af1e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328323"
---
# <a name="bluetooth-core-driver-layer-and-supported-power-transitions"></a>蓝牙核心驱动程序层和支持的功率转换


下表总结了蓝牙核心驱动程序支持的设备和系统电源状态。 "睡眠"状态是本部分中的使用的吞吐量和及其副主题描述非常低功耗状态蓝牙无线内部设置和配置具有持久性。

<table>
    <tr>
        <td></td>
        <td></td>
        <td colspan="3"><b>设备的电源状态</b></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td>D0 （活动）</td>
        <td>D2 （睡眠） – 某些 power 维护到蓝牙芯片的保持其内部状态</td>
        <td>D3 (Off) 的强大功能在于已删除 （*）</td>
    </tr>
    <tr>
        <td rowspan="6"><b>系统电源状态</b></td>
        <td>S0 （活动）</td>
        <td>活跃</td>
        <td>如果有唤醒睡眠状态</td>
        <td>关闭单选 RM</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
       <td>S2</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>S3 （睡眠）</td>
        <td>不可用</td>
        <td>如果有唤醒睡眠状态</td>
        <td>可以关闭</td>
    </tr>
    <tr>
        <td>S4（休眠）</td>
        <td>不可用</td>
        <td>如果有唤醒睡眠状态</td>
        <td>可以关闭</td>
    </tr>
    <tr>
        <td>S5（关闭）</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>可以关闭</td>
    </tr>
</table>



\*蓝牙核心驱动程序的重新初始化是必需的因为蓝牙芯片到断电

对于 SoC 系统支持系统状态的指导原则：

-   S0 (on) 和 S5 （关闭） 的支持是所必需的所有 Soc
-   S4 （休眠） 是所必需的基于 x86 的 Soc
-   支持连接待机系统不支持 S3

## <a name="span-idactives0d0spanspan-idactives0d0spanspan-idactives0d0spanactive-s0d0"></a><span id="Active__S0_D0_"></span><span id="active__s0_d0_"></span><span id="ACTIVE__S0_D0_"></span>活动 (S0/D0)


这是状态，在客户端应用程序经常使用蓝牙功能。

## <a name="span-idlowdutycyclesleeps0d2spanspan-idlowdutycyclesleeps0d2spanspan-idlowdutycyclesleeps0d2spanlow-duty-cyclesleep-s0d2"></a><span id="Low_Duty_Cycle_Sleep__S0_D2_"></span><span id="low_duty_cycle_sleep__s0_d2_"></span><span id="LOW_DUTY_CYCLE_SLEEP__S0_D2_"></span>低值班周期/睡眠 (S0/D2)


这是最常见的状态在其中系统处于有效地在 （S0)，但该驱动程序是在 D2 状态 – 控制器限制到较低的电源状态。 在此状态下，控制器可以恢复为活动状态 (D0) 相当快的速度而不会影响最终用户体验。

可以通过使用蓝牙键盘演示此状态的示例。 当没有键被按下几秒钟时，蓝牙的核心层限制到 D2 通知以及允许控制器进入空闲状态，同时保持探查模式以降低能耗中的连接。 在按下键，单选将接收唤醒通知并触发要恢复到 D0 然后读取传入数据的蓝牙核心驱动程序的唤醒事件。

有没有关联-蓝牙核心堆栈可以输入 D2 通知，并允许蓝牙无线限制下进入睡眠状态时，另一个示例是在初始条件中。 当用户想要将与远程 Bluetooth 的设备相关联时，可以快速恢复持久的非易失性设置时，进行了优化单选的功率消耗。

在此状态的常见和关键方案：

1.  不具有任何关联 （即没有与蓝牙设备配对）
2.  相关联，但进行连接在空闲
3.  相关联，但断开连接

更高版本的子主题提供更多详细信息输入到活动的空闲和恢复的机制。 此状态也将主状态变为 AOAC （始终开机和始终连接） 系统中。

## <a name="span-idsystemisonbutdeviceisoffs0d3spanspan-idsystemisonbutdeviceisoffs0d3spanspan-idsystemisonbutdeviceisoffs0d3spansystem-is-on-but-device-is-off-s0d3"></a><span id="System_is_On_but_Device_is_Off__S0_D3_"></span><span id="system_is_on_but_device_is_off__s0_d3_"></span><span id="SYSTEM_IS_ON_BUT_DEVICE_IS_OFF__S0_D3_"></span>系统上，但设备处于关闭状态 (S0/D3)


此状态当前为单选处于"off"模式下时仅支持单选管理。 状态会产生更长的延迟将还原到其活动状态的过程包括但不局限于设备级别初始化和配置，以及主机和设备初始化蓝牙核心驱动程序的蓝牙控制器。

## <a name="span-idsystemremotewake-ablesxd2spanspan-idsystemremotewake-ablesxd2spanspan-idsystemremotewake-ablesxd2spansystem-remote-wake-able-sxd2"></a><span id="System_Remote_Wake-able__Sx_D2_"></span><span id="system_remote_wake-able__sx_d2_"></span><span id="SYSTEM_REMOTE_WAKE-ABLE__SX_D2_"></span>系统远程唤醒可的 (Sx/D2)


对于 Windows 8.1，此 Sx 的支持保持不变并使用该特定状态以启用唤醒从 HID 设备的系统。 虽然在 D2，蓝牙芯片继续具有能力，因此其内部的易失性设置和配置保持持久性。 此功能是可选的。

## <a name="span-idsystemoffsxd3spanspan-idsystemoffsxd3spanspan-idsystemoffsxd3spansystem-off-sxd3"></a><span id="System_Off__Sx_D3__"></span><span id="system_off__sx_d3__"></span><span id="SYSTEM_OFF__SX_D3__"></span>关闭 (Sx/D3) 的系统


系统处于关闭状态，和蓝牙无线被假定为关闭或处于低功耗状态。 在 （除关机） 某些 Sx 状态，驱动程序堆栈所做的内存 （即它保持加载状态）。

## <a name="span-idradiomanagementspanspan-idradiomanagementspanspan-idradiomanagementspanradio-management"></a><span id="Radio_Management"></span><span id="radio_management"></span><span id="RADIO_MANAGEMENT"></span>单选管理


展望未来，将针对蓝牙 4.0 无线电收发器标准化单选管理 (RM)。 Bluetooth 堆栈将沿 HCI 发送\_重置命令，该单选应通过将单选放在任何传输模式和 D3 电源状态中的设备响应命令。 堆栈将意外删除所有子 devnodes，有效地将单选放入"飞行"模式。 串行总线驱动程序将保持处于关闭状态的单选中加载时，以便它可以接收请求从堆栈启用单选。 收件箱堆栈将处理 devnodes 重新枚举。 有关的单选管理实现的更多详细信息，请参阅[蓝牙软件无线电交换机函数原型](https://msdn.microsoft.com/library/windows/hardware/hh450832)。

 

 





