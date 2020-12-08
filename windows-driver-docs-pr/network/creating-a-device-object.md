---
title: " (Windows 筛选平台创建设备对象) "
description: 创建设备对象
keywords:
- Windows 筛选平台标注驱动程序 WDK，初始化
- 标注驱动程序 WDK Windows 筛选平台，初始化
- 初始化标注驱动程序 WDK Windows 筛选平台
- 设备对象 WDK Windows 筛选平台
- 基于 WDM 的标注驱动程序 WDK Windows 筛选平台
- 基于 WDF 的标注驱动程序 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c5acba1f29eae762689026318916f7f4a8c4bce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813687"
---
# <a name="creating-a-device-object-windows-filtering-platform"></a> (Windows 筛选平台创建设备对象) 


标注驱动程序必须先创建一个设备对象，然后才能使用筛选器引擎注册其标注。 标注驱动程序如何创建设备对象取决于标注驱动程序是基于 Windows 驱动模型 (WDM) 还是 Windows 驱动程序框架 (WDF) 。

### <a name="wdm-based-callout-drivers"></a>WDM-Based 标注驱动程序

如果标注驱动程序基于 WDM，它会通过调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 函数来创建设备对象。 例如：

```C++
PDEVICE_OBJECT deviceObject;

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS status;

  ...

  // Create a device object
 status =
 IoCreateDevice(
 DriverObject,
      0,
      NULL,
      FILE_DEVICE_UNKNOWN,
      FILE_DEVICE_SECURE_OPEN,
      FALSE,
      &deviceObject
      );

  ...

 return status;
}
```

### <a name="wdf-based-callout-drivers"></a>WDF-Based 标注驱动程序

如果标注驱动程序基于 WDF，它会通过调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 函数来创建框架设备对象。 若要使用筛选器引擎注册其标注，基于 WDF 的标注驱动程序必须获取一个指针，该指针指向与框架设备对象相关联的 WDM 设备对象。 基于 WDF 的标注驱动程序通过调用 [**WdfDeviceWdmGetDeviceObject**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmgetdeviceobject) 函数获取指向此 WDM 设备对象的指针。 例如：

```C++
WDFDEVICE wdfDevice;

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  WDFDRIVER driver;
  PWDFDEVICE_INIT deviceInit;
  PDEVICE_OBJECT deviceObject;
  NTSTATUS status;

  ...

  // Allocate a device initialization structure
 deviceInit =
 WdfControlDeviceInitAllocate(
    driver;
    &SDDL_DEVOBJ_KERNEL_ONLY
    );

  // Set the device characteristics
 WdfDeviceInitSetCharacteristics(
    deviceInit,
    FILE_DEVICE_SECURE_OPEN,
    FALSE
    );

  // Create a framework device object
 status =
 WdfDeviceCreate(
    &deviceInit,
    WDF_NO_OBJECT_ATTRIBUTES,
    &wdfDevice
    );

  // Check status
 if (status == STATUS_SUCCESS) {

    // Initialization of the framework device object is complete
    WdfControlFinishInitializing(
      wdfDevice
    );

    // Get the associated WDM device object
    deviceObject = WdfDeviceWdmGetDeviceObject(wdfDevice);
  }

  ...

 return status;
}
```

 

