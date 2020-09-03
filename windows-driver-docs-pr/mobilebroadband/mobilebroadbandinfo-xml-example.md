---
title: MobileBroadbandInfo XML 示例
description: MobileBroadbandInfo XML 示例
ms.assetid: 605566a2-55d7-456c-8999-e3bb626527fd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4227073db876e23d4d72165e235800a3e1e1adcf
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402780"
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
