---
title: WDM 读卡器驱动程序
description: WDM 读卡器驱动程序
keywords:
- 供应商提供的驱动程序 WDK 智能卡，必需例程
- WDM WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea809e231bc87660e721565fa72bbae88642e703
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804859"
---
# <a name="wdm-reader-driver"></a>WDM 读卡器驱动程序

## <a name="required-routines"></a>必需的例程

以下例程是 WDM 读取器驱动程序所必需的。

### <a name="driverentry"></a>[DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)

初始化驱动程序对象和调度表。

### <a name="adddevice"></a>[AddDevice](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)

创建智能卡读卡器的设备对象。 此外， [AddDevice](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 可以调用以下任何驱动程序库例程：

- [SmartcardInitialize (WDM) ](/previous-versions/ff548944(v=vs.85)) 完成驱动程序初始化。 在 [AddDevice](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 中调用此例程为必备。
- [SmartcardLogError (WDM) ](/previous-versions/ff548947(v=vs.85)) 记录错误。 如果[SmartcardInitialize (WDM) ](/previous-versions/ff548944(v=vs.85))失败，则驱动程序必须在[AddDevice](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)中调用此例程。
- [SmartcardCreateLink (WDM) ](/previous-versions/ff548935(v=vs.85)) 为注册表中的读取器设备创建一个符号链接。

### <a name="unload"></a>[[](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)

从系统中删除驱动程序。

### <a name="dispatchcreate"></a>[DispatchCreate](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

－和－

### <a name="dispatchclose"></a>[DispatchClose](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

分别支持 [IRP_MJ_CREATE](../kernel/irp-mj-create.md) 和 [IRP_MJ_CLOSE&lt](../kernel/irp-mj-close.md)。 为了与读取器建立连接，资源管理器会将 **IRP_MJ_CREATE** 发送到读取器驱动程序。 若要连接到服务器，资源管理器会发送 **IRP_MJ_CLOSE**。

### <a name="dispatchcleanup"></a>[DispatchCleanup](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

支持 [IRP_MJ_CLEANUP](../kernel/irp-mj-cleanup.md)，资源管理器会将其发送到读取器驱动程序以取消挂起的 i/o 请求。

### <a name="dispatchpnp"></a>[DispatchPnP](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

支持 [IRP_MJ_PNP](../kernel/irp-mj-pnp.md)

### <a name="dispatchpower"></a>[DispatchPower](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

支持 [IRP_MJ_POWER](../kernel/irp-mj-power.md)。

### <a name="dispatchdevicecontrol"></a>[DispatchDeviceControl](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

支持 [IRP_MJ_DEVICE_CONTROL](../kernel/irp-mj-device-control.md) ，它是智能卡请求的主入口点。 接收 IRP_MJ_DEVICE_CONTROL 时， [DispatchDeviceControl](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 必须立即调用 [SmartcardDeviceControl (WDM) ](/previous-versions/ff548939(v=vs.85))，这是处理设备控制请求的智能卡驱动程序库例程。 下面的代码示例演示如何从 WDM 驱动程序调用此库例程：

```cpp
NTSTATUS
DriverDeviceControl(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp
    )
{
    PDEVICE_EXTENSION deviceExtension = DeviceObject -&gt; DeviceExtension;

    return SmartcardDeviceControl(
        &(deviceExtension-&gt;SmartcardExtension),
        Irp
        );
```

如果无法处理在调用中指定的特定 IOCTL， **SmartcardDeviceControl** 将调用驱动程序对未知 IOCTL 请求的回调。
