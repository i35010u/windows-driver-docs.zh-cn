---
title: WindowsInfo XML 示例
description: WindowsInfo XML 示例
ms.assetid: 5933512e-d2bf-437f-abd8-dc3486e07be0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb3d612074c9098834715fb72457da295f6040c
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902424"
---
# <a name="windowsinfo-xml-example"></a>WindowsInfo XML 示例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

下面的 XML 文档使用 [WINDOWSINFO xml 架构](windowsinfo-xml-schema.md) 来指定在元数据包中指定的服务的显示操作：

``` syntax
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<WindowsInfo xmlns="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/"
             xmlns:v2="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/WindowsInfov2">
  <ShowDeviceInDisconnectedState>false</ShowDeviceInDisconnectedState>
</WindowsInfo>
```
