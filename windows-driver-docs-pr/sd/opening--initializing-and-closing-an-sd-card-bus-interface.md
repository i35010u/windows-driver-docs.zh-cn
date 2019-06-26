---
title: 打开、初始化和关闭 SD 卡总线接口
description: 打开、初始化和关闭 SD 卡总线接口
ms.assetid: 986a352e-c479-444d-9c65-7958dd638bbb
keywords:
- SD WDK 总线，打开接口
- SD WDK 总线，初始化接口
- SD WDK 总线，关闭接口
- 初始化 SD 总线接口
- SdBusOpenInterface
- SDBUS_INTERFACE_STANDARD
- 接口 WDK SD 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55811c6cfb87b3eec6f0eca6b13ac48f79088b5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384504"
---
# <a name="opening-initializing-and-closing-an-sd-card-bus-interface"></a>打开、初始化和关闭 SD 卡总线接口


安全数字 (SD) 设备驱动程序必须打开并初始化 SD 总线接口与主机控制器或他们管理的设备进行交互。 这需要两个调用 SD 总线库： 调用[ **SdBusOpenInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nf-ntddsd-sdbusopeninterface)跟初始化界面总线驱动程序提供的例程的调用。 **SdBusOpenInterface**返回的指针初始化的接口中的例程**InterfaceReference**的成员[ **SDBUS\_接口\_标准**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))结构。 设备驱动程序必须调用此初始化例程提供用一个指针指向中断通知回调例程总线驱动程序。 总线驱动程序使用此回调以通知的硬件中断的设备驱动程序。 有关初始化 SD 总线接口的例程的详细信息，请参阅[ **PSDBUS\_初始化\_接口\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)。 设备驱动程序通常会打开并初始化 SD 总线接口中的其[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。

下面的代码示例说明了打开并初始化 SD 总线接口的调用的顺序：

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

在此代码示例中，设备驱动程序调用**SdBusOpenInterface**以打开接口和总线驱动程序存储指向的指针初始化例程中设备扩展 (**DeviceExtension-&gt;BusInterface.InitializeInterface**)。 之后**SdBusOpenInterface**返回时，该驱动程序检索此指针从设备扩展。 接下来，驱动程序将指针放到其自身中断回调例程**pMyDriverCallback，** 中[ **SDBUS\_接口\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537919(v=vs.85))结构，并将此结构传递给初始化例程。

设备驱动程序还必须检索的上下文信息的**SdBusOpenInterface**中返回**上下文**SDBUS 成员\_接口\_标准结构。 只要该驱动程序调用 SD 总线接口例程时，应用程序必须通过在此上下文数据。

### <a name="closing-an-sd-interface"></a>关闭 SD 接口

若要关闭的 SD 接口，驱动程序必须取消引用接口的调用中的例程**InterfaceDereference** SDBUS 成员\_接口\_标准结构，释放所有资源由分配**SdBusOpenInterface**例程。 SD 设备驱动程序应关闭所有打开的 SD 接口接收任何以下 Irp 时：

[**IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

[**IRP\_MN\_REMOVE\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP\_MN\_SURPRISE\_REMOVAL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

下面的代码示例演示了如何将驱动程序可以取消引用 SD 卡总线接口：

```cpp
if (pDevExt->BusInterface.InterfaceDereference) {
    (pDevExt->BusInterface.InterfaceDereference) (pDevExt->BusInterface.Context);
    RtlZeroMemory(&pDevExt->BusInterface, sizeof(SDBUS_INTERFACE_STANDARD));
}
```

**SdBusOpenInterface**调用存储一个指向接口指针取消引用中 SDBUS 例程\_接口\_标准结构。 但是，驱动程序应验证的指针不是**NULL**然后再尝试调用例程。

 

 




