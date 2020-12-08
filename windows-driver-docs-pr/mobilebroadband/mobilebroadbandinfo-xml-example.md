---
title: MobileBroadbandInfo XML 示例
description: MobileBroadbandInfo XML 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2656212017e385102020cdde2170301f44ca8b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805307"
---
# <a name="mobilebroadbandinfo-xml-example"></a>MobileBroadbandInfo XML 示例

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

以下 XML 文档使用 [MOBILEBROADBANDINFO xml 架构](mobilebroadbandinfo-xml-schema.md) 指定服务的移动宽带特定信息：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<MobileBroadbandInfo xmlns="http://schemas.microsoft.com/windows/2010/12/DeviceMetadata/MobileBroadbandInfo">
  <NetworkConfiguration>
    <MobileBroadbandProfiles>
      <Purchase>PurchaseProfile.xml</Purchase>
      <Internet>OperatingProfile.xml</Internet>
    </MobileBroadbandProfiles>
    <AllowStandardUserPinUnlock>true</AllowStandardUserPinUnlock>
  </NetworkConfiguration>
  <ProvisioningEngine>
    <TrustedCertificates>
      <TrustedCertificate>
        <SubjectName>CN=Contoso, OU=Contosodev, O=Contoso, C=US</SubjectName>
        <IssuerName>CN= Contoso SA Root CA, OU=Contosodev, O=Contoso, C=US</IssuerName>
      </TrustedCertificate>
    </TrustedCertificates>
  </ProvisioningEngine>
</MobileBroadbandInfo>
```
