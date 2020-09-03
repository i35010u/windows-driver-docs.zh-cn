---
title: ServiceInfo XML 示例
description: ServiceInfo XML 示例
ms.assetid: b2114044-ca4b-4c1e-ab2e-73f4f56142b5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df4226e9f040a0a0858cd259e8d6157be5ff4f69
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403440"
---
# <a name="serviceinfo-xml-example"></a>ServiceInfo XML 示例

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

以下 XML 文档使用 [SERVICEINFO XML 架构](serviceinfo-xml-schema.md) 指定 Contoso 无线服务的属性：

``` syntax
<DeviceInfo xmls="http://schemas.microsoft.com/windows/2010/05/DeviceMetadata/ServiceInfo">
    <ServiceCategoryList>
        <ServiceCategory>Network.MobileBroadband </ServiceCategory>
    </ServiceCategoryList>
    <ServiceName> </ServiceName>
    <ServiceDescription1>Fabrikam Wireless 3G network</ServiceDescription1>
    <ServiceDescription2></ServiceDescription2>
    <ServiceNumber>D4A5C6D5-8135-4A0D-9B9D-016F5D7D9F45  </ServiceNumber>
    <ServiceProvider>Contoso Wireless</ServiceProvider>
    <ServiceIcon>Contoso.ico</ServiceIcon>
    <ServiceSpecificExtension namespace="http://schemas.microsoft.com/windows/2010/12/DeviceMetadata/MobileBroadbandInfo">MobileBroadbandInfo.xml</ServiceSpecificExtension>
</ServiceInfo>
```
