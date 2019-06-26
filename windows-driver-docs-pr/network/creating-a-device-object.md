---
title: 创建设备对象
description: 创建设备对象
ms.assetid: 9474e080-b2c3-4c1b-af19-bf269d1c94d4
keywords:
- Windows 筛选平台标注驱动程序 WDK，初始化
- 标注驱动程序 WDK Windows 筛选平台，初始化
- 初始化标注驱动程序 WDK Windows 筛选平台
- 设备对象 WDK Windows 筛选平台
- WDM 基于标注驱动程序 WDK Windows 筛选平台
- WDF 基于标注驱动程序 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b5c662a1d1f5cd670fcd5b5ad6dd5dc6536124c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374935"
---
# <a name="creating-a-device-object"></a>创建设备对象


它可以向筛选器引擎注册其调出之前，标注驱动程序必须创建一个设备对象。 标注驱动程序创建一个设备对象的方式取决于是否标注驱动程序基于 Windows 驱动程序模型 (WDM) 或 Windows 驱动程序框架 (WDF)。

### <a name="wdm-based-callout-drivers"></a>WDM 基于标注驱动程序

如果标注驱动程序基于 WDM，它创建一个设备对象通过调用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)函数。 例如：

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

### <a name="wdf-based-callout-drivers"></a>WDF 基于标注驱动程序

如果标注驱动程序基于 WDF，它通过调用创建 framework 设备对象[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)函数。 若要使用筛选器引擎注册其标注，WDF 基于标注驱动程序必须获取指向与 framework 设备对象相关联的 WDM 设备对象的指针。 WDF 基于标注驱动程序通过调用获取指向此 WDM 设备对象的指针[ **WdfDeviceWdmGetDeviceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmgetdeviceobject)函数。 例如：

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

 

 





