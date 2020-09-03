---
title: Wi-Fi 热点数据提交格式
description: Wi-Fi 热点数据提交格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e932867c9ac83abd902587ecef507ecae8bd7ee
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403462"
---
# <a name="wi-fi-hotspot-data-submission-format"></a>Wi-Fi 热点数据提交格式

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]

提交到发现服务的热点数据必须在 JavaScript 对象表示法 (JSON) ，并且必须使用以下元素。

| 元素 | 类型 | 说明 |
| --- | --- | --- |
| BatchId | GUID | 提供程序可以将包含多个热点的单个提交拆分为多个提交。 将为每个提交分配同一个 BatchId GUID。 |
| ProviderId | GUID | 提供程序 ID 将被 Microsoft 分配给提供程序。 |
| TransactionId | int | 批处理中每个请求的递增数。 用于 degbugging 目的。 |
| 热 |  | 要上载的热点列表。 |
| add |  | 完整的 address 属性，其中包括以下子元素： **address**、 **City**、 **StateOrProvince**、 **邮政编码**和 **CountryOrRegion**。 |
| bssids| List\<string> | 构成热点的 BSSIDs 的列表。 每个 BSSID 包含 8 2 位十六进制值，格式如下： *00： aa： bb： cc： dd： ee*。 |
| free | 布尔 | 指示热点是否可用的布尔值。 |
| 酒馆 | 布尔 | 指示热点是否为公共的布尔值。 |
| loc |  | 完整的位置属性，其中包括以下子元素： **纬度**、 **经度**、 **RadialUncertainty**、 **海拔**和 **AltitudeUncertainty**。 |
| name | 字符串 | 作用点的友好名称。 |
| phid | 字符串 | 提供者的热点 ID。 用于调试目的。 |
| 为名 | uint | 作用点的范围。 |
| ssid | 字符串 | 热点的 SSID。 |
| phone | 字符串 | 与热点关联的所有电话号码的列表。 |

**注意**

* 需要 (**ProviderId**、 **BatchId**和 **TransactionId**) 的标头及其子元素。
* 作用点列表不得为空。
* 如果指定 Location 元素，则必须指定 **纬度** 和 **经度** 。
* 如果未指定 Location 元素，则必须至少指定一个 BSSID。 否则，将返回一个警告，并且发现服务将不处理该作用点。

下面的示例演示了单个热点的完整数据：

```JSON
{
      "Header": {
            "BatchId": "BA85A383-5943-4D84-8ACB-B113BDEA3783", 
            "ProviderId": "AE012377-B0B4-4096-B5D5-D7EFBDC170EC", 
            "TransactionId": 1
      }, 
      "Hotspots":[{
            "add": {
                  "Address": "123 abc street", 
                  "City": "Redmond", 
                  "CountryOrRegion": "USA", 
                  "PostalCode": "98052", 
                  "StateOrProvince": "WA"
            },
            "bssids":["00:aa:bb:cc:dd:ee"],
            "free": true, 
            "pub": true, 
            "loc": {
                  "Latitude": 47.01, 
                  "Longitude": 121.1234, 
                  "RadialUncertainty": 300, 
                  "Altitude": 638.34, 
                  "AltitudeUncertainty": 100.0 
            }, 
            "name": "Joes Coffee Shop", 
            "phid": "abcdefg", 
            "ran": 100, 
            "ssid": "JoesCoffee", 
            "phone": ["425-882-8080"]
      }
}
```

发现服务将返回一个简单的响应，也就是 JSON 格式，其中包含用于调试目的的活动 ID 和发现服务验证热点数据时生成的警告的列表。 发现服务返回的所有字符串都以 UTF-8 编码。

下表显示了发现服务响应的 JSON 元素。

| 元素 | 类型 | 说明 |
| --- | --- | --- |
| ActivityId | 字符串 | 必需。 这是一个字符串，提供程序可用于帮助调试问题。 |
| 警告 | List\<string> | 用户可读的警告列表。 |

下面的示例演示对热点数据提交的典型响应：

```JSON
{
     "ActivityId": "d2856c06-e4a1-4434-90e8-ced0c9ee6e10",
     "Warnings": ["Invalid Latitude: 247.67 – Hotspot Id: abcdefg"]
}
```

