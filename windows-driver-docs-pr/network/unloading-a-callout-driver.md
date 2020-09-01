---
title: 卸载标注驱动程序
description: 卸载标注驱动程序
ms.assetid: a8c1bb33-41f8-420c-a761-669864eb9444
keywords:
- Windows 筛选平台标注驱动程序 WDK，卸载
- 标注驱动程序 WDK Windows 筛选平台，卸载
- 卸载驱动程序 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf0a2db3c0e6eb77da488e6ebd930aff0da7a3d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208545"
---
# <a name="unloading-a-callout-driver"></a>卸载标注驱动程序


若要卸载标注驱动程序，操作系统将调用标注驱动程序的 unload 函数。 有关如何指定标注驱动程序的 unload 函数的详细信息，请参阅 [指定卸载函数](specifying-an-unload-function.md)。

标注驱动程序的 unload 函数可保证在从系统内存中卸载标注驱动程序之前，不会从筛选器引擎中注销标注驱动程序的标注。 标注驱动程序调用 [**FwpsCalloutUnregisterById0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutunregisterbyid0) 函数或 [**FwpsCalloutUnregisterByKey0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutunregisterbykey0) 函数从筛选器引擎中注销标注。 标注驱动程序不能从其卸载函数返回，直到它成功地从筛选器引擎中注销其所有标注。

标注驱动程序从筛选器引擎中注销其所有标注后，必须先删除它在最初注册其标注之前创建的设备对象。 基于 Windows 驱动模型 (WDM) 的标注驱动程序将调用 [**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice) 函数来删除设备对象。 基于 Windows 驱动程序框架 (WDF) 的标注驱动程序将调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 函数来删除框架设备对象。

标注驱动程序还必须销毁先前通过调用 [**FwpsInjectionHandleDestroy0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectionhandledestroy0) 函数创建的任何数据包注入句柄，然后再从其 unload 函数返回。

例如：

```C++
// Device object
PDEVICE_OBJECT deviceObject;

// Variable for the run-time callout identifier
UINT32 CalloutId;

// Injection handle
HANDLE injectionHandle;

// Unload function
VOID
 Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  NTSTATUS status;

  // Unregister the callout
 status =
 FwpsCalloutUnregisterById0(
 CalloutId
      );

  // Check result
 if (status == STATUS_DEVICE_BUSY)
  {
    // For each data flow that is being processed by the
    // callout that has an associated context, clean up
    // the context and then call FwpsFlowRemoveContext0
    // to remove the context from the data flow.
    ...

    // Finish unregistering the callout
 status =
 FwpsCalloutUnregisterById0(
 CalloutId
        );
  }

  // Check status
 if (status != STATUS_SUCCESS)
  {
    // Handle error
    ...
  }

  // Delete the device object
 IoDeleteDevice(
 deviceObject
    );

  // Destroy the injection handle
 status =
 FwpsInjectionHandleDestroy0(
 injectionHandle
      );

  // Check status
 if (status != STATUS_SUCCESS)
  {
    // Handle error
    ...
  }
}
```

前面的示例假定使用基于 WDM 的标注驱动程序。 对于基于 WDF 的标注驱动程序，唯一的区别在于传递给标注驱动程序的 unload 函数的参数以及 callout 驱动程序如何删除框架设备对象。

```C++
WDFDEVICE wdfDevice;

VOID
 Unload(
    IN WDFDRIVER Driver;
    )
{

  ...

  // Delete the framework device object
 WdfObjectDelete(
 wdfDevice
    );

  ...
}
```

 

