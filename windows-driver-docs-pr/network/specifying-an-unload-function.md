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
ms.openlocfilehash: ca491f9c414837d5d6e8c66f4e41f4abc01613b5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205931"
---
# <a name="specifying-an-unload-function"></a>指定卸载函数


标注驱动程序必须提供 unload 函数。 当从系统中卸载标注驱动程序时，操作系统将调用此函数。 标注驱动程序的 unload 函数必须保证在从系统内存中卸载标注驱动程序之前，标注驱动程序的标注已从筛选器引擎中取消注册。 如果标注驱动程序未提供 unload 函数，则无法从系统中卸载该驱动程序。

标注驱动程序如何指定卸载函数取决于标注驱动程序是否基于 Windows 驱动模型 (WDM) 或 Windows 驱动程序框架 (WDF) 。

### <a name="wdm-based-callout-drivers"></a>基于 WDM 的标注驱动程序

如果标注驱动程序基于 WDM，则它会在其[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数中指定[**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数。 例如：

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

如果标注驱动程序基于 WDF，则它会在其[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数中指定[*EvtDriverUnload*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)函数。 例如：

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

有关如何实现注解驱动程序的 unload 功能的信息，请参阅 [卸载标注驱动程序](unloading-a-callout-driver.md)。

 

