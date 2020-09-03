---
title: WindowsInfo XML 示例
description: WindowsInfo XML 示例
ms.assetid: 5933512e-d2bf-437f-abd8-dc3486e07be0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b034efd0f3828e214e4366eb6609b487fcd3b5b7
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402740"
---
# <a name="windowsinfo-xml-example"></a>WindowsInfo XML 示例

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

下面的 XML 文档使用 [WINDOWSINFO xml 架构](windowsinfo-xml-schema.md) 来指定在元数据包中指定的服务的显示操作：

``` syntax
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<WindowsInfo xmlns="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/"
             xmlns:v2="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/WindowsInfov2">
  <ShowDeviceInDisconnectedState>false</ShowDeviceInDisconnectedState>
</WindowsInfo>
```
