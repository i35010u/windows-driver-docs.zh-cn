---
title: 访问配置信息
description: 访问配置信息
keywords:
- NetAdapterCx 访问配置信息，NetCx 访问配置信息
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11e4b0ecdc8c7434a41333bad86f14683d28af03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838763"
---
# <a name="accessing-configuration-information"></a>访问配置信息

NetAdapterCx 类扩展支持一组可用于访问客户端驱动程序注册表参数的函数。

通常，客户端驱动程序从其 [*EVT_WDF_DRIVER_DEVICE_ADD*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中读取配置信息。

对于 Get-netadapter 对象，请首先调用 [**NetAdapterOpenConfiguration**](/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapteropenconfiguration) 以获取配置对象的句柄。  然后，可以对其进行查询：

```C++
NETCONFIGURATION configuration;

status = NetAdapterOpenConfiguration(NetAdapter, 
                                     WDF_NO_OBJECT_ATTRIBUTES, 
                                     &configuration);
if (!NT_SUCCESS(status)) {
    return status;
}

status = NetConfigurationQueryUlong(configuration, 
                                    NET_CONFIGURATION_QUERY_ULONG_NO_FLAGS, 
                                    &SomeValue, 
                                    &myvalue);

NetConfigurationClose(configuration);
```

为网络设备打开和查询配置对象类似于：

```C++
status = NetDeviceOpenConfiguration(Device, 
                                    WDF_NO_OBJECT_ATTRIBUTES, 
                                    &configuration);
if(!NT_SUCCESS(status))
{
    return status;
}

WDFCOLLECTION myStrings;

DECLARE_CONST_UNICODE_STRING(myValueName, L"ExampleValueName");

status = NetConfigurationQueryMultiString(configuration,
                                          myValueName,
                                          WDF_NO_OBJECT_ATTRIBUTES,
                                          myStrings);
```

有一些 `NetConfiguration*` 函数可用于查询 ULONG 数据、字符串、多字符串 (类似于 REG_MULTI_SZ) 、二进制 blob 和软件可配置的网络地址：

* [**NetConfigurationAssignBinary**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignbinary)
* [**NetConfigurationAssignMultiString**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignmultistring)
* [**NetConfigurationAssignUlong**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignulong)
* [**NetConfigurationAssignUnicodeString**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignunicodestring)
* [**NetConfigurationClose**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationclose)
* [**NetConfigurationOpenSubConfiguration**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationopensubconfiguration)
* [**NetConfigurationQueryBinary**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerybinary)
* [**NetConfigurationQueryMultiString**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerymultistring)
* [**NetConfigurationQueryLinkLayerAddress**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerylinklayeraddress)
* [**NetConfigurationQueryString**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerystring)
* [**NetConfigurationQueryUlong**](/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationqueryulong)
