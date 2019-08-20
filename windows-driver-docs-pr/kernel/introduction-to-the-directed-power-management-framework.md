---
title: 导向式电源管理框架简介
description: 描述定向电源管理框架或 DFx, 它等效于 Power Framework 或 PoFx (版本 3)。
ms.assetid: 58550c57-3439-4212-b0c6-6a2fbfd38414
ms.date: 03/27/2019
ms.custom: 19H1
ms.openlocfilehash: 5f2d941645a954c8574bedc83acad3f87f334cf7
ms.sourcegitcommit: ffa7111fb450ae189b4d071e273117404cb299fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2019
ms.locfileid: "68380084"
---
# <a name="introduction-to-the-directed-power-management-framework"></a>导向式电源管理框架简介

从 Windows 10 1903 版开始, 运行时电源管理框架 ([PoFx](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)) 的版本3提供了一个可选的定向电源模式, 即定向 PoFx (DFx)。

对于 DFx, 操作系统会指导设备堆栈进入空闲状态, 并使系统进入空闲状态, 从而使系统能够更可靠地进入低功耗。

目标是使系统更具强大的功能, 并跨外形规格降低 Windows 设备的能耗。

DFx 目前仅支持 D 状态管理。  DFx 将跳过具有 F 状态约束的任何设备子树。

## <a name="requirements-for-wdf-non-miniport-drivers"></a>WDF (非微型端口) 驱动程序的要求

指定[WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构中的**SystemManagedIdleTimeout**或**SystemManagedIdleTimeoutWithHint**的 WDF 驱动程序可以通过将以下注册表项添加到 INF 的 DDInstall.HW 部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)中的 [AddReg 指令部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)：

```
HKR,"WDF","WdfDirectedPowerTransitionEnable",0x00010001,1
```

由于请求系统管理的空闲超时会使 WDF 代表驱动程序注册 PoFx, 因此在此方案中, 驱动程序不需要注册到 PoFx。

如果驱动程序指定**DriverManagedIdleTimeout**, 请考虑切换到系统托管的空闲超时。  如果这不可行, 请使用下面 WDM 部分中的指导原则选择加入 DFx。

如果 WDF 驱动程序不使用运行时电源管理, 请添加对它的支持并使用系统管理的空闲超时。  为此, 请提供[WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构作为[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)的输入。

## <a name="requirements-for-wdm-non-miniport-drivers"></a>WDM (非微型端口) 驱动程序的要求

如果你的驱动程序未使用 WDF 提供的系统托管的空闲支持 (该驱动程序是使用驱动程序托管的空闲的 WDF 驱动程序, 或者是 WDM 驱动程序), 则它仍然可以通过向 PoFx 注册自己来获得 DFx 支持。  在此方案中, 驱动程序通过实现以下内容向 PoFx 注册:

- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)


提供指向[**PoFxRegisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregisterdevice)函数输入的[PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)结构中的这些回调的指针。

若要获得 DFx 支持, 驱动程序必须:

* 注册 PoFx 时提供回调`PO_FX_DIRECTED_POWER*`
* 从 Sx 转换的恢复时调用[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)的[PO_FX_DIRECTED_POWER_UP_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)回调函数

## <a name="example"></a>示例

以下示例显示了上述自注册选项:

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

如果先前指定`PO_FX_VERSION_V1`了驱动程序, `PO_FX_DEVICE_V3`请注意, `PO_FX_COMPONENT_V2`结构对组件数组结构使用。

## <a name="requirements-for-miniport-drivers"></a>微型端口驱动程序的要求

对于遵循端口/微型端口驱动程序模型的设备类, 系统提供的端口驱动程序通常会处理电源策略所有权。  大多数微型端口不需要进行任何代码更改即可选择加入 DFx, 因为需要相应的端口驱动程序来处理 DFx 支持。

## <a name="testing"></a>正在测试

Microsoft 提供了三种可用于 DFx 的测试: [Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)中用于测试用户指定的设备的单设备测试、设备级的 hlk 测试, 以及用于测试系统上所有设备的系统级的 hlk 测试。

单设备测试作为 WDK 随附的[PwrTest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest)工具的一部分提供。  若要访问它, 请使用`/directedfx`开关运行该工具。  有关详细信息, 请参阅[PwrTest DirectedFx 方案](../devtest/pwrtest-directedfx-scenario.md)。

有关 HLK 测试的信息, 请参阅以下页面:

- [定向 FX 单一设备测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [定向 FX 系统验证测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)

建议在 S4 转换后测试 DFx, 以便捕获驱动程序在从 S4 恢复后可能无法正确调用[PoFxReportDevicePoweredOn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)的任何情况。

## <a name="dfx-and-s-state-transitions"></a>DFx 和 S 状态转换

- DFx 转换的目标 D 状态应与运行时 D3 (RTD3) 的状态匹配, 这可能不同于 S3/S4 转换的目标 D 状态。  假设某个设备进入 D2 for RTD3, 但进入了用于 S3/S4 的 D3。  在这种情况下, DFx 的目标 D 状态应为 D2。
- 同样, DFx 的 "用于唤醒的 arm" 行为应与 RTD3 (可能不同于 S3/S4 转换中使用的类型) 匹配。  例如, 设备可能进入 RTD3 的 D2/唤醒, 但对于 S3/S4, 请输入 D3/无唤醒。  在此方案中, DFx 转换还应输入 D2/唤醒。

## <a name="dfx-and-runtime-d3-rtd3"></a>DFx 和运行时 D3 (RTD3)

- 使用 RTD3, 设备进入空闲状态时通常会进入较低的 power D 状态。  如果新工作到达, 设备会立即唤醒到 D0。  使用 DFx, 设备应继续保持其目标 D 状态 (并在其队列中挂起新工作), 直到 PoFx 将其打开。

## <a name="see-also"></a>请参阅

- [为新式待机准备硬件](https://docs.microsoft.com/windows-hardware/design/device-experiences/prepare-hardware-for-modern-standby)
- [PwrTest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest)
- [PO_FX_DEVICE_V3 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)
- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)
- [PoFxCompleteDirectedPowerDown 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompletedirectedpowerdown) 
- [PwrTest DirectedFx 方案](../devtest/pwrtest-directedfx-scenario.md)
- [定向 FX 单一设备测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [定向 FX 系统验证测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
