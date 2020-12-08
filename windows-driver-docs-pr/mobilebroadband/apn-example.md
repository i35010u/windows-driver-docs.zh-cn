---
title: APN 示例
description: APN 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d61f9389f012b81bbe5522a2c770e94f6c6fe546
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782535"
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

 

 





