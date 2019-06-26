---
title: 指定卸载函数
description: 指定卸载函数
ms.assetid: 3bfac8a5-1367-40bd-81b5-4a7fb9aaaece
keywords:
- Windows 筛选平台标注驱动程序 WDK，初始化
- 标注驱动程序 WDK Windows 筛选平台，初始化
- 初始化标注驱动程序 WDK Windows 筛选平台
- WDM 基于标注驱动程序 WDK Windows 筛选平台
- WDF 基于标注驱动程序 WDK Windows 筛选平台
- 卸载函数 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95526a041a191e881ce82b40685550e687e3b111
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374712"
---
# <a name="specifying-an-unload-function"></a>指定卸载函数


标注驱动程序必须提供卸载函数。 从系统中卸载标注驱动程序时，操作系统将调用此函数。 标注驱动程序的卸载函数必须保证标注驱动程序的标注的筛选器引擎从注销之前标注驱动程序是从系统内存中卸载。 如果它不提供卸载函数不能从系统中卸载标注驱动程序。

标注驱动程序是如何指定卸载函数取决于是否标注驱动程序基于 Windows 驱动程序模型 (WDM) 或 Windows 驱动程序框架 (WDF)。

### <a name="wdm-based-callout-drivers"></a>WDM 基于标注驱动程序

如果标注驱动程序基于 WDM，它指定[ **Unload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)函数，在其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数。 例如：

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

### <a name="wdf-based-callout-drivers"></a>WDF 基于标注驱动程序

如果为基础 WDF 标注驱动程序，它指定[ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)函数，在其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数。 例如：

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

有关如何实现标注驱动程序的卸载函数的信息，请参阅[卸载标注驱动程序](unloading-a-callout-driver.md)。

 

 





