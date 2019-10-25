---
title: 蓝牙核心驱动程序层和支持的功率转换
description: 下表总结了蓝牙核心驱动程序支持的设备和系统电源状态。
ms.assetid: 25A3598E-51A7-4B16-92F7-9D2F39177946
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acefa2bf99669bb5633b69cd6fcc7a9306d03b3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832190"
---
# <a name="bluetooth-core-driver-layer-and-supported-power-transitions"></a>蓝牙核心驱动程序层和支持的功率转换


下表总结了蓝牙核心驱动程序支持的设备和系统电源状态。 "睡眠" 状态用于此部分及其子主题的吞吐量，用于描述蓝牙无线电的内部设置和配置是持久的。

<table>
    <tr>
        <td></td>
        <td></td>
        <td colspan="3"><b>设备电源状态</b></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td>D0 （活动）</td>
        <td>D2 （睡眠）–在蓝牙芯片中保留一些电源，使其保持其内部状态</td>
        <td>D3 （关）-已删除电源（*）</td>
    </tr>
    <tr>
        <td rowspan="6"><b>系统电源状态</b></td>
        <td>S0 （活动）</td>
        <td>活跃</td>
        <td>如果唤醒，则为睡眠</td>
        <td>无线电 RM 关闭</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>N/A</td>
        <td>N/A</td>
        <td>N/A</td>
    </tr>
    <tr>
       <td>S2</td>
        <td>N/A</td>
        <td>N/A</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td>S3 （睡眠）</td>
        <td>N/A</td>
        <td>如果唤醒，则为睡眠</td>
        <td>可以关闭电源</td>
    </tr>
    <tr>
        <td>S4（休眠）</td>
        <td>N/A</td>
        <td>如果唤醒，则为睡眠</td>
        <td>可以关闭电源</td>
    </tr>
    <tr>
        <td>S5（关闭）</td>
        <td>N/A</td>
        <td>N/A</td>
        <td>可以关闭电源</td>
    </tr>
</table>



由于蓝牙芯片丢失电源，因此需要通过蓝牙核心驱动程序进行 \*重新初始化

针对 SoC 系统的系统状态支持准则：

-   所有 Soc 都需要 S0 （on）和 S5 （shutdown）支持
-   S4 （休眠）对基于 x86 的 Soc 是必需的
-   支持连接备用的系统不支持 S3

## <a name="span-idactive__s0_d0_spanspan-idactive__s0_d0_spanspan-idactive__s0_d0_spanactive-s0d0"></a><span id="Active__S0_D0_"></span><span id="active__s0_d0_"></span><span id="ACTIVE__S0_D0_"></span>活动（S0/D0）


这是客户端应用程序主动使用蓝牙功能时的状态。

## <a name="span-idlow_duty_cycle_sleep__s0_d2_spanspan-idlow_duty_cycle_sleep__s0_d2_spanspan-idlow_duty_cycle_sleep__s0_d2_spanlow-duty-cyclesleep-s0d2"></a><span id="Low_Duty_Cycle_Sleep__S0_D2_"></span><span id="low_duty_cycle_sleep__s0_d2_"></span><span id="LOW_DUTY_CYCLE_SLEEP__S0_D2_"></span>低责任周期/睡眠（S0/D2）


这是系统有效使用的最常见状态，但驱动程序处于 D2 状态-控制器将被限制为低功率状态。 在此状态下，控制器可以恢复到活动状态（D0），而不会影响最终用户体验。

可以使用蓝牙键盘演示此状态的示例。 如果没有按键几秒钟，则蓝牙核心层会限制为 D2，通知并允许控制器进入空闲状态，同时在监听模式下保持连接以减少功率消耗。 按键时，无线电将收到唤醒通知，并触发唤醒事件，使蓝牙 core 驱动程序恢复到 D0，然后读取传入的数据。

另一个示例是在没有关联的情况下的初始条件下，蓝牙核心堆栈可以进入 D2 来通知并允许蓝牙无线电进入睡眠状态。 无线电的功率消耗经过优化，但当用户打算与远程蓝牙设备关联时，持久的非易失性设置可以快速恢复。

处于此状态的常见和关键方案：

1.  无关联（即，不包含蓝牙设备配对）
2.  具有关联，已连接但处于空闲状态
3.  具有关联但已断开连接

后面的子主题提供了有关进入空闲状态和恢复活动的机制的更多详细信息。 此状态还会成为 AOAC （Always On Always 连接）系统中的主要状态。

## <a name="span-idsystem_is_on_but_device_is_off__s0_d3_spanspan-idsystem_is_on_but_device_is_off__s0_d3_spanspan-idsystem_is_on_but_device_is_off__s0_d3_spansystem-is-on-but-device-is-off-s0d3"></a><span id="System_is_On_but_Device_is_Off__S0_D3_"></span><span id="system_is_on_but_device_is_off__s0_d3_"></span><span id="SYSTEM_IS_ON_BUT_DEVICE_IS_OFF__S0_D3_"></span>系统处于开启状态，但设备处于关闭状态（S0/D3）


当前只有无线电设备处于 "关闭" 模式时，才支持此状态。 此状态将导致将蓝牙控制器还原到其活动状态的延迟时间较长，其中，进程包括但不限于设备级别初始化和配置，以及由蓝牙核心驱动程序进行主机和设备初始化。

## <a name="span-idsystem_remote_wake-able__sx_d2_spanspan-idsystem_remote_wake-able__sx_d2_spanspan-idsystem_remote_wake-able__sx_d2_spansystem-remote-wake-able-sxd2"></a><span id="System_Remote_Wake-able__Sx_D2_"></span><span id="system_remote_wake-able__sx_d2_"></span><span id="SYSTEM_REMOTE_WAKE-ABLE__SX_D2_"></span>系统远程唤醒（Sx/D2）


对此 Sx 的支持对 Windows 8.1 保持不变，此特定状态用于启用从 HID 设备唤醒系统。 在 D2 中，蓝牙芯片会继续通电，因此其内部易失性设置和配置保持持久性。 此功能是可选的。

## <a name="span-idsystem_off__sx_d3__spanspan-idsystem_off__sx_d3__spanspan-idsystem_off__sx_d3__spansystem-off-sxd3"></a><span id="System_Off__Sx_D3__"></span><span id="system_off__sx_d3__"></span><span id="SYSTEM_OFF__SX_D3__"></span>系统关闭（Sx/D3）


系统已关闭，并且系统假定蓝牙无线电处于关闭状态或处于低功耗状态。 在某些 Sx 状态下（关闭除外），驱动程序堆栈仍处于内存中（即它仍处于加载状态）。

## <a name="span-idradio_managementspanspan-idradio_managementspanspan-idradio_managementspanradio-management"></a><span id="Radio_Management"></span><span id="radio_management"></span><span id="RADIO_MANAGEMENT"></span>无线电管理


今后，将为蓝牙4.0 无线电系统标准化无线电管理（RM）。 蓝牙堆栈会向下发送 HCI\_RESET 命令，该命令会将无线电置于 "无传输" 模式下，并将设备置于 D3 电源状态。 然后，堆栈会意外地删除所有子 devnodes，从而将无线电有效地放置在 "飞行" 模式下。 当处于无线电关闭状态时，串行总线驱动程序会保持加载状态，因此它可以接收来自堆栈的请求以打开无线电。 收件箱堆栈将处理 devnodes 的重新枚举。 有关实现收音机管理的更多详细信息，请参阅[蓝牙软件无线电开关函数原型](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

 

 





