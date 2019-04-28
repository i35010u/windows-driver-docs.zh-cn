---
title: 导向式电源管理框架简介
description: 描述定向电源管理框架或 DFx，这等同于电源框架或 PoFx，版本 3。
ms.assetid: 58550c57-3439-4212-b0c6-6a2fbfd38414
ms.date: 03/27/2019
ms.custom: 19H1
ms.openlocfilehash: 5bd11c3b5728e9e6515c687fa902e2236e37608b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341434"
---
# <a name="introduction-to-the-directed-power-management-framework"></a>导向式电源管理框架简介

从 Windows 10，版本 1903年，版本 3 的运行时电源管理框架开始 ([PoFx](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)) 提供了一个可选定向电源模型，定向 PoFx (DFx)。

使用 DFx，操作系统设备堆栈时系统将转换为处于空闲状态，，从而使系统更可靠地进入低能耗进入其相应的低能耗空闲状态。

目的是为了使系统电源效率并减少在外观造型上的适用于 Windows 设备的能源消耗。

DFx 目前支持仅 D 状态管理。  DFx 跳过使用 F 状态约束任何设备的子树。

## <a name="requirements-for-wdf-non-miniport-drivers"></a>WDF （非微型端口） 驱动程序的要求

指定的 WDF 驱动程序**SystemManagedIdleTimeout**或**SystemManagedIdleTimeoutWithHint**中[WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构可以选择到 DFx 通过添加以下注册表项的 INF [AddReg 指令部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)内[DDInstall.HW 部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section):

```
HKR,"WDF","WdfDirectedPowerTransitionEnable",0x00010001,1
```

请求系统管理的空闲超时导致 WDF 驱动程序的名义注册 PoFx，因为该驱动程序不需要在此方案中向 PoFx 注册。

如果指定了该驱动程序**DriverManagedIdleTimeout**，请考虑切换到系统管理空闲超时。  如果这不可行，使用在下面的 WDM 部分准则来选择加入 DFx。

如果 WDF 驱动程序不使用运行时的电源管理，添加对它的支持，并使用系统管理空闲超时。  若要执行此操作，提供[WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构，作为输入[ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)。

## <a name="requirements-for-wdm-non-miniport-drivers"></a>用于 WDM （非微型端口） 驱动程序的要求

如果您的驱动程序不使用提供的 WDF 的系统管理的空闲支持 (驱动程序是任一 WDF 驱动程序使用驱动程序管理处于空闲状态，或 WDM 驱动程序)，它仍可以通过将自身注册与 PoFx 获取 DFx 支持。  在此方案中，该驱动程序将向注册 PoFx 通过实现：

- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)


提供指向在这些回调[PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)输入到结构[ **PoFxRegisterDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregisterdevice)函数。

若要获取 DFx 支持仅，设备可以提供仅`PO_FX_DIRECTED_POWER*`回调注册 PoFx 时。  它不需要实现 PoFx 回调的其余部分。

## <a name="example"></a>示例

下面的示例演示上面所述的自助注册选项：

```
PO_FX_DEVICE_V3 MyPoFxDevice;
POHANDLE MyPoFxHandle;

RtlZeroMemory(&MyPoFxDevice, sizeof(PO_FX_DEVICE_V3));
MyPoFxDevice.Version = PO_FX_VERSION_V3;

// Initialize other PoFx callbacks and other fields like
// components and their idle states.

MyPoFxDevice.DirectedPowerUpCallback = <Driver's DFx power up callback>
MyPoFxDevice.DirectedPowerDownCallback = <Driver's DFx power down callback>

Status = PoFxRegisterDevice(
  <Driver's device object>,
  (PPO_FX_DEVICE)&MyPoFxDevice,
  &MyPoFxHandle);
  if (!NT_SUCCESS(Status)) {
  return Status;
}
```

如果您的驱动程序指定`PO_FX_VERSION_V1`之前，请注意，`PO_FX_DEVICE_V3`结构使用`PO_FX_COMPONENT_V2`组件数组结构。

## <a name="requirements-for-miniport-drivers"></a>微型端口驱动程序

按照端口/微型端口驱动程序模型的设备类，系统提供的端口驱动程序通常处理电源策略所有权。  不应需要选择加入 DFx，任何代码更改，因为相应的端口驱动程序需要处理 DFx 支持大多数微型端口。

## <a name="testing"></a>正在测试

Microsoft 提供三个测试，可用于 DFx： 中的单个设备测试[Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)用于测试用户指定的设备、 设备级 HLK 测试和用于测试的所有设备上的系统级 HLK 测试系统。

单一设备测试现作为的一部分[PwrTest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest)附带 WDK 的工具。  若要访问它，请运行与工具`/directedfx`切换。  有关详细信息，请参阅[PwrTest DirectedFx 方案](../devtest/pwrtest-directedfx-scenario.md)。

有关 HLK 测试的信息，请参阅以下页面：

- [定向 FX 单一设备测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [定向 FX 系统验证测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)

## <a name="dfx-and-s-state-transitions"></a>DFx 和 S 状态转换

- DFx 转换的目标 D 状态应匹配的运行时 D3 (RTD3)，这可能会不同于 S3/S4 转换的目标 D 状态。  请考虑在其中设备进入 D2 为 RTD3，但为 S3/S4 输入 D3 的方案。  在这种情况下，DFx 的目标 D 状态应为 D2。
- 同样，DFx arm 为唤醒行为应与匹配 RTD3，这可能会有所不同，S3/S4 转换中使用。  例如，设备可能 RTD3，输入有 D2/唤醒但 S3/S4 输入 D3/否-唤醒东西。  在此方案中，DFx 转换应还输入 D2/唤醒东西。

## <a name="dfx-and-runtime-d3-rtd3"></a>DFx 和运行时 D3 (RTD3)

- 与 RTD3，设备通常时将进入低功耗 D 状态进入空闲状态。  如果新的工作到达时，到 D0 立即唤醒设备。  使用 DFx，设备应继续保留在其目标 D 状态 （和其队列中挂起新的工作） 直到 PoFx 将其定向到电源备份。

## <a name="see-also"></a>请参阅

- [为新式待机准备硬件](https://docs.microsoft.com/windows-hardware/design/device-experiences/prepare-hardware-for-modern-standby)
- [PwrTest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest)
- [PO_FX_DEVICE_V3 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)
- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)
- [PoFxCompleteDirectedPowerDown](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompletedirectedpowerdown)函数
- [PwrTest DirectedFx 方案](../devtest/pwrtest-directedfx-scenario.md)
- [定向 FX 单一设备测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [定向 FX 系统验证测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
