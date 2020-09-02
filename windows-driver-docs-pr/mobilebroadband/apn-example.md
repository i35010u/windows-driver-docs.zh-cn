---
title: APN 示例
description: APN 示例
ms.assetid: 3cf74bc4-a334-4213-8138-ebfc91b459e8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b844b35ea0e5aa34e93c111f28b5d4ee2a32784
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304306"
---
# <a name="apn-example"></a>APN 示例


以下 XML 文档使用 [APN XML 架构](apn-schema-definition.md) 指定服务的接入点信息：

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<OperatorList 
  <Operator name="Contoso">
    <HardwareIdList>
      <HardwareId id="MBAE:0:XSDR^EREDER^F">
      </HardwareId>
    </HardwareIdList>
    <ConnectionInfoList>
      <ConnectionInfo AccessString="ContosoAPN" Username="user" Password="pass" FriendlyName="Prepaid Contoso Mobile Broadband" Internet="Y" Purchase="N" AutoConnectOrder="1"/>
    </ConnectionInfoList>
  </Operator>
</OperatorList>
```

 

 





