---
title: 指定卸载函数
description: 指定卸载函数
ms.assetid: 3bfac8a5-1367-40bd-81b5-4a7fb9aaaece
keywords:
- Windows 筛选平台标注驱动程序 WDK，初始化
- 标注驱动程序 WDK Windows 筛选平台，初始化
- 初始化标注驱动程序 WDK Windows 筛选平台
- 基于 WDM 的标注驱动程序 WDK Windows 筛选平台
- 基于 WDF 的标注驱动程序 WDK Windows 筛选平台
- 卸载函数 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab42a478ead3b77a2fc49b295322877f51b97670
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841873"
---
# <a name="specifying-an-unload-function"></a>指定卸载函数


标注驱动程序必须提供 unload 函数。 当从系统中卸载标注驱动程序时，操作系统将调用此函数。 标注驱动程序的 unload 函数必须保证在从系统内存中卸载标注驱动程序之前，标注驱动程序的标注已从筛选器引擎中取消注册。 如果标注驱动程序未提供 unload 函数，则无法从系统中卸载该驱动程序。

标注驱动程序如何指定卸载函数取决于标注驱动程序是基于 Windows 驱动模型（WDM）还是 Windows 驱动程序框架（WDF）。

### <a name="wdm-based-callout-drivers"></a>基于 WDM 的标注驱动程序

如果标注驱动程序基于 WDM，则它会在其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数中指定[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数。 例如：

```C++
VOID
 Unload(
    IN PDRIVER_OBJECT DriverObject
    );

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  ...

  // Specify the callout driver's Unload function
 DriverObject->DriverUnload = Unload;

  ...
}
```

### <a name="wdf-based-callout-drivers"></a>基于 WDF 的标注驱动程序

如果标注驱动程序基于 WDF，则它会在其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数中指定[*EvtDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)函数。 例如：

```C++
VOID
 Unload(
    IN WDFDRIVER Driver
    );

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS status;
  WDF_DRIVER_CONFIG config;
  WDFDRIVER driver;

  ...

  // Initialize the driver config structure
  WDF_DRIVER_CONFIG_INIT(&config, NULL);

  // Indicate that this is a non-PNP driver
 config.DriverInitFlags = WdfDriverInitNonPnpDriver;

  // Specify the callout driver's Unload function
 config.EvtDriverUnload = Unload;

  // Create a WDFDRIVER object
 status =
 WdfDriverCreate(
 DriverObject,
 RegistryPath,
      NULL,
      &config,
      &driver
      );

  ...

 return status;
}
```

有关如何实现注解驱动程序的 unload 功能的信息，请参阅[卸载标注驱动程序](unloading-a-callout-driver.md)。

 

 





