---
title: 卸载标注驱动程序
description: 卸载标注驱动程序
ms.assetid: a8c1bb33-41f8-420c-a761-669864eb9444
keywords:
- Windows 筛选平台标注驱动程序 WDK，卸载
- 标注驱动程序 WDK Windows 筛选平台，卸载
- 正在卸载驱动程序 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0af4f957b5e8bc92b513c13e3b7e164814fa6c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541024"
---
# <a name="unloading-a-callout-driver"></a>卸载标注驱动程序


若要卸载标注驱动程序，操作系统将调用标注驱动程序的卸载函数。 有关如何指定标注驱动程序的卸载函数的详细信息，请参阅[指定卸载函数](specifying-an-unload-function.md)。

标注驱动程序的卸载函数确保标注驱动程序的标注从筛选器引擎中注销之前标注驱动程序是从系统内存中卸载。 标注驱动程序拨打[ **FwpsCalloutUnregisterById0** ](https://msdn.microsoft.com/library/windows/hardware/ff551144)函数或[ **FwpsCalloutUnregisterByKey0** ](https://msdn.microsoft.com/library/windows/hardware/ff551145)函数取消注册从筛选器引擎标注。 标注驱动程序必须从其卸载函数之前返回之后它已成功注销所有筛选器引擎从其标注。

标注驱动程序已注销所有筛选器引擎从其标注后，它必须删除该设备对象，它创建之前它最初注册其标注。 基于 Windows 驱动程序模型 (WDM) 调用的标注驱动程序[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)函数删除的设备对象。 基于 Windows 驱动程序框架 (WDF) 调用的标注驱动程序[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)函数删除 framework 设备对象。

标注驱动程序还必须销毁它以前通过调用创建任何数据包注入句柄[ **FwpsInjectionHandleDestroy0** ](https://msdn.microsoft.com/library/windows/hardware/ff551181)函数从其卸载函数在返回之前。

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

前面的示例假定 WDM 基于标注驱动程序。 WDF 基于标注驱动程序，唯一的区别是传递给标注驱动程序的卸载函数和标注驱动程序如何删除 framework 设备对象的参数。

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

 

 





