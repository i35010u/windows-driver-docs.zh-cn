---
title: 访问配置信息
description: 访问配置信息
ms.assetid: ABEC75AE-9CE3-4574-B388-BC48D2BC8154
keywords:
- NetAdapterCx 访问 NetCx 访问配置信息的配置信息
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1980dd36326717ce7d1b2cdd7d7790c236f6a387
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363673"
---
# <a name="accessing-configuration-information"></a>访问配置信息

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx 类扩展插件支持一组提供对客户端驱动程序注册表参数访问的函数。

通常情况下，客户端驱动程序读取配置信息从其[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。

对于 NetAdapter 对象，开始通过调用[ **NetAdapterOpenConfiguration** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapteropenconfiguration)若要获取配置对象的句柄。  然后，您可以查询它：

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

打开并正在查询网络设备的配置对象是类似：

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

有`NetConfiguration*`函数用于查询 ULONG 数据、 字符串、 多字符串 （类似于 REG_MULTI_SZ）、 二进制 blob 和软件配置的网络地址：

* [**NetConfigurationAssignBinary**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationassignbinary)
* [**NetConfigurationAssignMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationassignmultistring)
* [**NetConfigurationAssignUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationassignulong)
* [**NetConfigurationAssignUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationassignunicodestring)
* [**NetConfigurationClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationclose)
* [**NetConfigurationOpenSubConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationopensubconfiguration)
* [**NetConfigurationQueryBinary**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationquerybinary)
* [**NetConfigurationQueryMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationquerymultistring)
* [**NetConfigurationQueryLinkLayerAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationquerylinklayeraddress)
* [**NetConfigurationQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationquerystring)
* [**NetConfigurationQueryUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netconfiguration/nf-netconfiguration-netconfigurationqueryulong)
