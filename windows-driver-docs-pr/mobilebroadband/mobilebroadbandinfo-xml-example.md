---
title: MobileBroadbandInfo XML 示例
description: MobileBroadbandInfo XML 示例
ms.assetid: 605566a2-55d7-456c-8999-e3bb626527fd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f9a8909d099fec4a06bbdaac827aa17df5808a4
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323672"
---
# <a name="mobilebroadbandinfo-xml-example"></a>MobileBroadbandInfo XML 示例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

以下 XML 文档使用[MOBILEBROADBANDINFO xml 架构](mobilebroadbandinfo-xml-schema.md)指定服务的移动宽带特定信息：

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

 

 





