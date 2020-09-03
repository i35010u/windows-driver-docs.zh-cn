---
title: 打开、初始化和关闭 SD 卡总线接口
description: 打开、初始化和关闭 SD 卡总线接口
ms.assetid: 986a352e-c479-444d-9c65-7958dd638bbb
keywords:
- SD WDK 总线，打开接口
- SD WDK 总线，初始化接口
- SD WDK 总线，关闭接口
- 正在初始化 SD bus 接口
- SdBusOpenInterface
- SDBUS_INTERFACE_STANDARD
- 接口 WDK SD bus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bba0e09a051254e83dfff64de2b37c942971ef34
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384179"
---
# <a name="opening-initializing-and-closing-an-sd-card-bus-interface"></a>打开、初始化和关闭 SD 卡总线接口


安全数字 (SD) 设备驱动程序必须打开并初始化 SD 总线接口，才能与它们所管理的设备或主机控制器交互。 这需要对 SD bus 库进行两次调用：对 [**SdBusOpenInterface**](/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbusopeninterface) 的调用，然后调用对总线驱动程序所提供的例程（初始化接口）。 **SdBusOpenInterface**返回一个指针，该指针指向在[**SDBUS \_ 接口 \_ 标准**](/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))结构的**InterfaceReference**成员中初始化接口的例程。 设备驱动程序必须调用此初始化例程，以向总线驱动程序提供指向中断通知回调例程的指针。 总线驱动程序使用此回调通知设备驱动程序硬件中断。 有关初始化 SD 总线接口的例程的详细信息，请参阅 [**PSDBUS \_ INITIALIZE \_ interface \_ 例程**](/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)。 设备驱动程序通常会在其 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程内打开并初始化 SD 总线接口。

下面的代码示例演示了打开和初始化 SD 总线接口的调用序列：

```cpp
  status = SdBusOpenInterface (pDevExt->UnderlyingPDO,
    &pDevExt->BusInterface,
    sizeof(SDBUS_INTERFACE_STANDARD),
    SDBUS_INTERFACE_VERSION);

  if (NT_SUCCESS(status)) {
    SDBUS_INTERFACE_PARAMETERS interfaceParameters = {0};
    interfaceParameters.Size = 
      sizeof(SDBUS_INTERFACE_PARAMETERS);
    interfaceParameters.TargetObject = 
      DeviceExtension->TargetObject;
    interfaceParameters.DeviceGeneratesInterrupts = TRUE;
    interfaceParameters.CallbackRoutine = pMyDriverCallback;
    status = STATUS_UNSUCCESSFUL;
    if (DeviceExtension->BusInterface.InitializeInterface) {
      status = (pDevExt->BusInterface.InitializeInterface)
        (pDevExt->BusInterface.Context, &interfaceParameters);
    }
      }
```

在此代码示例中，设备驱动程序调用 **SdBusOpenInterface** 来打开接口，而总线驱动程序在设备扩展中存储一个指向初始化例程的指针， (**BusInterface.IniDeviceExtension &gt; tializeInterface**) 。 **SdBusOpenInterface**返回后，驱动程序从设备扩展中检索此指针。 接下来，驱动程序将指针置于其自己的中断回调例程 **pMyDriverCallback，** [**SDBUS \_ 接口 \_ 参数**](/previous-versions/windows/hardware/drivers/ff537919(v=vs.85)) 结构中，并将此结构传递到初始化例程。

设备驱动程序还必须检索 **SdBusOpenInterface** 在 SDBUS 接口标准结构的 **上下文** 成员中返回的上下文 \_ 信息 \_ 。 只要驱动程序调用 SD 总线接口例程，就必须在此上下文数据中传递。

### <a name="closing-an-sd-interface"></a>关闭 SD 接口

若要关闭 SD 接口，驱动程序必须通过调用 SDBUS 接口标准结构的 **InterfaceDereference** 成员中的例程来取消对接口的引用 \_ \_ ，这将释放 **SdBusOpenInterface** 例程分配的所有资源。 当接收到以下任一 Irp 时，SD 设备驱动程序应关闭所有打开的 SD 接口：

[**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](../kernel/irp-mn-query-remove-device.md)

[**IRP \_ MN \_ 删除 \_ 设备**](../kernel/irp-mn-remove-device.md)

[**IRP \_ MN \_ 意外 \_ 删除**](../kernel/irp-mn-surprise-removal.md)

下面的代码示例说明了驱动程序如何可以取消引用 SD 卡总线接口：

```cpp
if (pDevExt->BusInterface.InterfaceDereference) {
    (pDevExt->BusInterface.InterfaceDereference) (pDevExt->BusInterface.Context);
    RtlZeroMemory(&pDevExt->BusInterface, sizeof(SDBUS_INTERFACE_STANDARD));
}
```

**SdBusOpenInterface**调用在 SDBUS \_ 接口标准结构中存储指向接口取消引用例程的指针 \_ 。 但是，在尝试调用例程之前，驱动程序应该验证指针是否不为 **NULL** 。

 

