---
title: SoftwareInfo XML 示例
description: SoftwareInfo XML 示例
ms.assetid: 3ee92b21-ed4e-4ed9-9199-3f43f2f8ec00
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ab08e3b1df63ed0528d3d6896c2609280767c4e
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902642"
---
# <a name="softwareinfo-xml-example"></a>SoftwareInfo XML 示例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

以下 XML 文档使用 [SERVICEINFO XML 架构](serviceinfo-xml-schema.md) 指定 Contoso 无线服务的属性：

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
