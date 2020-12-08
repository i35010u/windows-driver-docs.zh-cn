---
title: SoftwareInfo XML 示例
description: SoftwareInfo XML 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52d311fea2b759b01c2f11d5b70afec9b54f23af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830359"
---
# <a name="softwareinfo-xml-example"></a>SoftwareInfo XML 示例

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

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
