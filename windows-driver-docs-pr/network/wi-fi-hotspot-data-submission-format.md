---
title: Wi-Fi 热点数据提交格式
description: Wi-Fi 热点数据提交格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abe78dbc18f82563b1835c12a36ba33accac982c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567053"
---
# <a name="wi-fi-hotspot-data-submission-format"></a>Wi-Fi 热点数据提交格式

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

热点数据提交到发现服务必须是以 JavaScript 对象表示法 (JSON)，并且必须使用以下元素。

| 元素 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
| BatchId | GUID | 一个提供程序可以拆分到多个提交包含多个热点的单个提交。 每次提交分配相同的 BatchId GUID。 |
| ProviderId | GUID | 由 Microsoft，提供程序 ID 将分配给该提供程序。 |
| TransactionId | int | 批处理中每个请求的是递增的数字。 用于 degbugging 目的。 |
| 热点 |  | 热点上传的列表。 |
| 添加 |  | 完整地址属性，其中包括以下子元素：**地址**，**市/县**， **StateOrProvince**， **PostalCode**，并且**CountryOrRegion**。 |
| Bssids| List\<string> | 构成了该热点 BSSIDs 的列表。 每个 BSSID 包含八个中的两个数字十六进制值格式如下：*00:aa:bb:cc:dd:ee*。 |
| free | 布尔 | 一个布尔值，该值指示是否免费热点。 |
| pub | 布尔 | 一个布尔值，该值指示是否为公共热点。 |
| Loc |  | 完整位置属性，其中包括以下子元素：**纬度**，**经度**， **RadialUncertainty**，**海拔高度**，并且**AltitudeUncertainty**。 |
| name | string | 热点的友好名称。 |
| phid | string | 提供程序的热点 id。 用于调试目的。 |
| 运行 | uint | 热点的范围。 |
| ssid | string | 热点的 SSID。 |
| phone | string | 与热点相关联的所有电话号码的列表。 |

**注意**

* 标头和及其子元素 (**ProviderId**， **BatchId**，并**TransactionId**) 所需。
* 热点列表不能为空。
* 如果指定了位置元素则**纬度**并**经度**所需。
* 如果未指定位置元素，则必须指定至少一个 BSSID。 否则为将返回一条警告，发现服务将不处理热点。

下面的示例演示单个热点的完整数据：

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

发现服务返回简单的响应，也采用 JSON 格式，其中包括用于调试目的和发现服务验证热点数据时生成的警告的列表的活动 ID。 发现服务返回的所有字符串都编码为 utf-8。

下表显示了发现服务响应的 JSON 元素。

| 元素 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
| ActivityId | string | 必需。 这是一个字符串，该提供程序可用来帮助调试问题。 |
| 警告 | List\<string> | 用户可读的警告的列表。 |

下面的示例显示了热点数据提交到的典型响应：

```JSON
{
     "ActivityId": "d2856c06-e4a1-4434-90e8-ced0c9ee6e10",
     "Warnings": ["Invalid Latitude: 247.67 – Hotspot Id: abcdefg"]
}
```

