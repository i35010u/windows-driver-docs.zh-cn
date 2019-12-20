---
title: 访问配置信息
description: 访问配置信息
ms.assetid: ABEC75AE-9CE3-4574-B388-BC48D2BC8154
keywords:
- NetAdapterCx 访问配置信息，NetCx 访问配置信息
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96f5273c6752ee32d39a480988bdf807f756347
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210789"
---
# <a name="accessing-configuration-information"></a>访问配置信息

NetAdapterCx 类扩展支持一组可用于访问客户端驱动程序注册表参数的函数。

通常，客户端驱动程序从其[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中读取配置信息。

对于 Get-netadapter 对象，请首先调用[**NetAdapterOpenConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapteropenconfiguration)以获取配置对象的句柄。  然后，可以对其进行查询：

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

有 `NetConfiguration*` 的函数可用于查询 ULONG 数据、字符串、多字符串（类似于 REG_MULTI_SZ）、二进制 blob 和软件可配置的网络地址：

* [**NetConfigurationAssignBinary**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignbinary)
* [**NetConfigurationAssignMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignmultistring)
* [**NetConfigurationAssignUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignulong)
* [**NetConfigurationAssignUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationassignunicodestring)
* [**NetConfigurationClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationclose)
* [**NetConfigurationOpenSubConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationopensubconfiguration)
* [**NetConfigurationQueryBinary**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerybinary)
* [**NetConfigurationQueryMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerymultistring)
* [**NetConfigurationQueryLinkLayerAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerylinklayeraddress)
* [**NetConfigurationQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationquerystring)
* [**NetConfigurationQueryUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netconfiguration/nf-netconfiguration-netconfigurationqueryulong)
