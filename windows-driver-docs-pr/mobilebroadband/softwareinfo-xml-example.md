---
title: SoftwareInfo XML 示例
description: SoftwareInfo XML 示例
ms.assetid: 3ee92b21-ed4e-4ed9-9199-3f43f2f8ec00
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd0d12ed67003e4ea8db9b1ecef1a300942ec890
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323684"
---
# <a name="softwareinfo-xml-example"></a>SoftwareInfo XML 示例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

以下 XML 文档使用[SERVICEINFO XML 架构](serviceinfo-xml-schema.md)指定 Contoso 无线服务的属性：

``` syntax
<?xml version="1.0" encoding="utf-8" standalone="yes"?>

<SoftwareInfo xmlns="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/SoftwareInfo">

  <DeviceCompanionApplications>
    <Package>
      <Identity Name="64022CONTOSO.ContosoDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" />
      <Applications>
        <Application Id="DeviceAppForPrinters">
          <DeviceNotificationHandlers>
            <DeviceNotificationHandler EventID="NotificationHandler" EventAsset="Fabrikam.OperatorApp. NotificationHandler" />
          </DeviceNotificationHandlers>
        </Application>
      </Applications>
    </Package>
  </DeviceCompanionApplications>

  <PrivilegedApplications>
    <Package>
      <Identity Name="64022CONTOSO.ContosoDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" AccessCustomDriver="false" />
    </Package>
  </PrivilegedApplications>

</SoftwareInfo>
```

 

 





