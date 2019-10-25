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
ms.openlocfilehash: 7f4004d0ce0fd952f5c9613ed43df59fd0d7ee2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824719"
---
# <a name="opening-initializing-and-closing-an-sd-card-bus-interface"></a>打开、初始化和关闭 SD 卡总线接口


安全数字（SD）设备驱动程序必须打开并初始化 SD 总线接口，才能与它们所管理的设备或主机控制器交互。 这需要对 SD bus 库进行两次调用：对[**SdBusOpenInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbusopeninterface)的调用，然后调用对总线驱动程序所提供的例程（初始化接口）。 **SdBusOpenInterface**返回一个指针，该指针指向一个例程，该例程在[**SDBUS\_接口**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))的**InterfaceReference**成员中初始化接口\_标准结构。 设备驱动程序必须调用此初始化例程，以向总线驱动程序提供指向中断通知回调例程的指针。 总线驱动程序使用此回调通知设备驱动程序硬件中断。 有关初始化 SD 总线接口的例程的详细信息，请参阅[**PSDBUS\_INITIALIZE\_interface\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)。 设备驱动程序通常会在其[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程内打开并初始化 SD 总线接口。

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

在此代码示例中，设备驱动程序调用**SdBusOpenInterface**来打开接口，而总线驱动程序存储指向设备扩展中的初始化例程的指针（**DeviceExtension-&gt;BusInterface。 InitializeInterface**). **SdBusOpenInterface**返回后，驱动程序从设备扩展中检索此指针。 接下来，驱动程序将指针置于其自己的中断回调例程**pMyDriverCallback，** 在[**SDBUS\_接口\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537919(v=vs.85))结构中，并将此结构传递到初始化例程。

设备驱动程序还必须检索上下文信息，该信息**SdBusOpenInterface**在 SDBUS\_接口的**上下文**成员中返回，\_标准结构。 只要驱动程序调用 SD 总线接口例程，就必须在此上下文数据中传递。

### <a name="closing-an-sd-interface"></a>关闭 SD 接口

若要关闭 SD 接口，驱动程序必须通过调用 SDBUS\_接口的**InterfaceDereference**成员中的例程来取消引用接口\_标准结构，这将释放由**SdBusOpenInterface**例程。 当接收到以下任一 Irp 时，SD 设备驱动程序应关闭所有打开的 SD 接口：

[**IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

[**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP\_MN\_意外\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

下面的代码示例说明了驱动程序如何可以取消引用 SD 卡总线接口：

```cpp
if (pDevExt->BusInterface.InterfaceDereference) {
    (pDevExt->BusInterface.InterfaceDereference) (pDevExt->BusInterface.Context);
    RtlZeroMemory(&pDevExt->BusInterface, sizeof(SDBUS_INTERFACE_STANDARD));
}
```

**SdBusOpenInterface**调用将指向 SDBUS\_接口中的接口取消引用例程的指针存储\_标准结构。 但是，在尝试调用例程之前，驱动程序应该验证指针是否不为**NULL** 。

 

 




