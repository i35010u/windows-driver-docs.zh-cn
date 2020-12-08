---
title: 导向式电源管理框架简介
description: 描述定向电源管理框架，或 DFx，它是 Power Framework 的一部分或 PoFx （版本3）。
ms.date: 02/21/2020
ms.custom: 19H1
ms.openlocfilehash: e70ceaeb17142769670415c1aad0909d4513c4b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838873"
---
# <a name="introduction-to-the-directed-power-management-framework"></a>导向式电源管理框架简介

从1903版的 Windows 10 版中开始， ([PoFx](./overview-of-the-power-management-framework.md)) 提供可选的定向电源模式，定向 PoFx (DFx) 。

对于 DFx，操作系统会将设备堆栈定向到进入空闲状态且无 [激活](/windows-hardware/design/device-experiences/activators)器中转软件活动时进入其适当的低功耗空闲状态，从而使系统能够更可靠地进入低功率。

目标是使系统更具强大的功能，并跨外形规格降低 Windows 设备的能耗。

当前仅具有 D 状态约束的设备支持 DFx。  DFx 将跳过具有 F 状态约束的任何设备子树。

DFx 不会关闭分页或调试设备。

## <a name="requirements-for-wdf-non-miniport-drivers"></a>WDF (非微型端口) 驱动程序的要求

在 [WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构中指定 **SystemManagedIdleTimeout** 或 **SystemManagedIdleTimeoutWithHint** 的 WDF 驱动程序可以通过将以下注册表项添加到 [DDInstall 部分](../install/inf-ddinstall-hw-section.md)中 INF 的 [AddReg 指令部分](../install/inf-addreg-directive.md)来选择 DFx：

`HKR,"WDF","WdfDirectedPowerTransitionEnable",0x00010001,1`

默认情况下，针对版本31和更高版本的 WDF 驱动程序将启用 DFx。 如果不需要，驱动程序可以通过将注册表项设置为0来选择退出 DFx： 

`HKR,"WDF","WdfDirectedPowerTransitionEnable",0x00010001,0`

由于请求系统管理的空闲超时会使 WDF 代表驱动程序注册 PoFx，因此在此方案中，驱动程序不需要注册到 PoFx。

如果驱动程序指定 **DriverManagedIdleTimeout**，请考虑切换到系统托管的空闲超时。  如果这不可行，请使用下面 WDM 部分中的指导原则选择加入 DFx。

如果 WDF 驱动程序不使用运行时电源管理，请添加对它的支持并使用系统管理的空闲超时。  为此，请提供 [WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings) 结构作为 [**WdfDeviceAssignS0IdleSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)的输入。

## <a name="requirements-for-wdm-non-miniport-drivers"></a>WDM (非微型端口) 驱动程序的要求

如果你的驱动程序未使用 WDF 提供的系统托管的空闲支持 (则该驱动程序是使用 [驱动程序托管的空闲](/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_power_policy_idle_timeout_type)的 WDF 驱动程序，或是 WDM 驱动程序) ，它仍然可以通过向 PoFx 注册自己来获得 DFx 支持。  在此方案中，驱动程序通过实现以下内容向 PoFx 注册：

- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK 回调函数](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK 回调函数](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_up_callback)


在 [PO_FX_DEVICE_V3](/windows-hardware/drivers/ddi/wdm/ns-wdm-po_fx_device_v3) 结构中提供指向这些回调的指针，该结构是 [**PoFxRegisterDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregisterdevice) 函数的输入。

若要获得 DFx 支持，驱动程序必须：

* `PO_FX_DIRECTED_POWER*`注册 PoFx 时提供回调
* 从 Sx 转换的恢复时，从其 [PO_FX_DIRECTED_POWER_UP_CALLBACK](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_up_callback)回调函数调用 [**PoFxReportDevicePoweredOn**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)

## <a name="example"></a>示例

以下示例显示了上述自注册选项：

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

如果先前指定了驱动程序 `PO_FX_VERSION_V1` ，请注意， `PO_FX_DEVICE_V3` 结构 `PO_FX_COMPONENT_V2` 对组件数组结构使用。

## <a name="requirements-for-miniport-drivers"></a>微型端口驱动程序的要求

对于遵循端口/微型端口驱动程序模型的设备类，系统提供的端口驱动程序通常会处理电源策略所有权。  大多数微型端口不需要进行任何代码更改即可选择加入 DFx，因为需要相应的端口驱动程序来处理 DFx 支持。

## <a name="testing"></a>正在测试

Microsoft 为 DFx 提供三个测试： [Windows 驱动程序工具包](../download-the-wdk.md) 中用于测试用户指定的设备的单设备测试、设备级的 hlk 测试，以及用于测试系统上所有设备的系统级的 hlk 测试。

单设备测试作为 WDK 随附的 [PwrTest](../devtest/pwrtest.md) 工具的一部分提供。  若要访问它，请使用开关运行该工具 `/directedfx` 。  有关详细信息，请参阅 [PwrTest DirectedFx 方案](../devtest/pwrtest-directedfx-scenario.md)。

有关 HLK 测试的信息，请参阅以下页面：

- [定向 FX 单一设备测试](/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [定向 FX 系统验证测试](/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)

建议在 S4 转换后测试 DFx，以便捕获驱动程序在从 S4 恢复后可能无法正确调用 [PoFxReportDevicePoweredOn](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon) 的任何情况。

## <a name="dfx-and-s-state-transitions"></a>DFx 和 S 状态转换

- DFx 转换的目标 D 状态应匹配运行时 D3 (RTD3) ，这可能不同于 S3/S4 转换的目标 D 状态。  假设某个设备进入 D2 for RTD3，但进入了用于 S3/S4 的 D3。  在这种情况下，DFx 的目标 D 状态应为 D2。
- 同样，DFx 的 "用于唤醒的 arm" 行为应与 RTD3 （可能不同于 S3/S4 转换中使用的类型）匹配。  例如，设备可能进入 RTD3 的 D2/唤醒，但对于 S3/S4，请输入 D3/无唤醒。  在此方案中，DFx 转换还应输入 D2/唤醒。

## <a name="dfx-and-runtime-d3-rtd3"></a>DFx 和运行时 D3 (RTD3) 

- 使用 RTD3，设备进入空闲状态时通常会进入较低的 power D 状态。  如果新工作到达，设备会立即唤醒到 D0。  使用 DFx，设备应继续保留其目标 D 状态 (，并挂起其队列中的新工作，) 直到 PoFx 将其打开。


## <a name="see-also"></a>另请参阅

- [为新式待机准备硬件](/windows-hardware/design/device-experiences/prepare-hardware-for-modern-standby)
- [PwrTest](../devtest/pwrtest.md)
- [PO_FX_DEVICE_V3 结构](/windows-hardware/drivers/ddi/wdm/ns-wdm-po_fx_device_v3)
- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK 回调函数](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK 回调函数](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_up_callback)
- [PoFxCompleteDirectedPowerDown 函数](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompletedirectedpowerdown) 
- [PwrTest DirectedFx 方案](../devtest/pwrtest-directedfx-scenario.md)
- [定向 FX 单一设备测试](/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [定向 FX 系统验证测试](/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
