---
title: WindowsInfo XML 示例
description: WindowsInfo XML 示例
ms.assetid: 5933512e-d2bf-437f-abd8-dc3486e07be0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4acfab86a850273fa47fab1b2f4b72f7a13601f5
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323632"
---
# <a name="windowsinfo-xml-example"></a>WindowsInfo XML 示例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

下面的 XML 文档使用[WINDOWSINFO xml 架构](windowsinfo-xml-schema.md)来指定在元数据包中指定的服务的显示操作：

``` syntax
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<WindowsInfo xmlns="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/"
             xmlns:v2="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/WindowsInfov2">
  <ShowDeviceInDisconnectedState>false</ShowDeviceInDisconnectedState>
</WindowsInfo>
```

 

 





