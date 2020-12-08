---
title: WindowsInfo XML 示例
description: WindowsInfo XML 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77150376eb6d88de70629b46fe0af98d09279c01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838853"
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
