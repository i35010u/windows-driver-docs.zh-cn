---
title: Wi-Fi 发现服务
description: Wi-Fi 发现服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 008b4f87b21fc8da11193247b952dd0598e924dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382865"
---
# <a name="wi-fi-discovery-service"></a>Wi-Fi 发现服务

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

Wi-fi 发现服务使用户能够通过卸载到 Wi-fi 热点的移动电话网络流量减少数据费用。 从提供程序，如移动运营商，以及其他源生成的已知的 Wi-fi 热点的目录中发现服务聚合的 Wi-fi 热点数据。 通过使用此目录，用户可以获取有关其当前位置附近的热点的信息。

移动运营商可以热点将数据提交到该服务通过发送 HTTP POST 请求，或通过使用由 Microsoft 提供的命令行工具。

## <a name="instructions"></a>说明

Wi-fi 热点数据必须采用格式中所述[Wi-fi 热点数据提交格式](wi-fi-hotspot-data-submission-format.md)。

发现服务需要在单个批处理中提交所有提供程序的热点。 每个批处理可以包含多个较小数量的数据提交请求。 例如，可以通过发送 10 个提交请求，每个包含数据的 100 热点到发现服务上载包含 1,000 热点的批处理。 每个提交请求分配相同的批数。 最后一个提交请求必须包含`X-FinalBatchRequest`标头设置为批处理中的热点的总数。 收到此标头的提交请求之前，不处理批。 如果标头与批处理中的热点数不匹配，未处理的提交。

### <a name="submitting-hotspot-data-by-using-http-post"></a>通过使用 HTTP POST 提交热点数据

下面的示例显示了典型的提交请求。 是否存在`X-FinalBatchRequest`标头和"1"的数值指示此批处理中有一个热点并且这是最后一个提交请求。 因此，这是唯一的提交请求。 如果批中包含多个热点，应为所有提交请求，但最后一个移除此行。

```http
POST https://submitwifiservice.windowsphone.com/v1/SubmitHotspots HTTP/1.1
Content-Type: application/json
X-FinalBatchRequest: 1
 [More headers…]
{
      "Header": {
            "BatchId": "2E20A8DB-9AFA-4A5A-AF6E-5F87DA639C15", 
            "TransactionId": 1, 
            "ProviderId": "FD9E5EE6-75C7-4A54-8B29-45A3FC83AD63"
      }, 
      "Hotspots": {
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

在目标服务器接收消息**SubmitHotspots**验证请求并发送到发现服务的热点数据之前对发件人进行身份验证。

### <a name="submitting-hotspot-data-by-using-the-command-line-tool"></a>通过使用命令行工具提交热点数据

WifiProviderExe.exe 是 Microsoft 的输入数据文件，将其转换为所需的格式，然后将其上传到指定的发现服务服务器热点，提供一个命令行工具。

若要运行 WiFiProvider.exe，使用以下语法：

```cmd
WifiProviderExe –DataFile filename -ProviderId GUID -ServiceEndpoint URL -CustomTransformer filename.dll [-MappingFile filename.xml] [-CertFile filename.pfx] [-CertPassword password] [-CertSubject name]
```

例如：

```cmd
WifiProviderExe -DataFile "file.txt" -ProviderId 00000000-0000-0000-0000-000000000000 -ServiceEndpoint "https://submitwifiservice.windowsphone.com/v1/SubmitHotspots" -CustomTransformer "transformer.dll"
```

下表包含 WiFiProvider.exe 的可能的参数列表。

| 参数 | 描述 |
| --- | --- |
| DataFile | 必需。 包含热点数据文件的名称。 |
| ProviderId | 必需。 Microsoft 分配的提供程序 ID (GUID)。 |
| ServiceEndpoint | 必需。 发现服务服务器热点数据将上载到的 URL。 例如， https://wifi.windowsphone.com/v1/submithotspots |
| CustomerTransformer | 必需。 包含转换器程序集的名称。 | 
| MappingFile | 可选。 将提供程序的热点数据映射到发现服务所需的格式的映射文件。 |
| CertFile | 可选。 指向包含身份验证的证书的实际 pfx 文件的指针。 证书密码参数 (**CertPassword**) 使用此身份验证方法时，必须指定。 |
| CertPassword | 可选。 中指定的证书的密码**CertFile**。 |
| CertSubject | 可选。 证书使用者名称。 该文件位于当前用户的 My 证书存储区。 使用此身份验证机制，当**CertFile**并**CertPassword**不是必需的。 但是，它被需要创建私钥证书，并在访问控制列表中，向授予访问权限的密钥将使用该证书的帐户。 |

#### <a name="transformers"></a>转换器

热点数据可以是任何格式。 但是，它则需要指定"数据转换器"命令行工具可以访问以便将热点数据转换为发现服务所需的格式。

下表显示了使用命令行工具提供示例转换程序。 它们可以用于将特定的数据格式转换为所需的格式。

| 转换器 | 数据格式 | 描述 |
| --- | --- | --- |
| Microsoft.Wps.WifiService.ProviderSdk.JsonHotspotDataTransformer.dll | JSON | 你的数据中指定的 JSON 格式必须符合[Wi-fi 热点数据提交格式](wi-fi-hotspot-data-submission-format.md)。 |
| Microsoft.Wps.WifiService.ProviderSdk.JsonHotspotDataTransformer.dll | 简单的 Excel | 必须提供一个映射文件。 |

#### <a name="mapping-files"></a>映射文件

如果你热点的数据是简单的 Excel 格式，则必须提供将 Excel 文件中的列映射到对应所需的 JSON 元素的 XML 文件。 以下列表显示了允许的列名称：

* 纬度
* 经度
* RadialUncertainty
* 海拔高度
* AltitudeUncertainty
* HotspotName
* SSID
* 范围
* 地址
* 城市
* StateOrProvince
* 邮政编码
* CountryOrRegion
* Bssids
* ProviderHotspotId
* IsPublic
* IsFree
* PhoneNumbers

下面的示例显示了映射文件的一部分。 每个**MappingRule**元素关联的 Excel 列 (**PartnerColumnName**并**PartnerColumnNumber**) 与所需的 JSON 元素 (**MicrosoftColumnName**)。 **ContainsHeaderRow**位于关闭之后的元素规则标记 (`</Rules>`)，指示该文件包含一个标题行，读取数据时应跳过。

```xml
<?xml version="1.0" encoding="utf-8"?>
<MappingRules xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <Rules>
    <MappingRule>
      <PartnerColumnName>english_hotspot_name</PartnerColumnName>
      <PartnerColumnNumber>3</PartnerColumnNumber>
      <MicrosoftColumnName>HotspotName</MicrosoftColumnName> 
    </MappingRule>
    <MappingRule>
      <PartnerColumnName>english_city_name</PartnerColumnName>
      <PartnerColumnNumber>2</PartnerColumnNumber>
      <MicrosoftColumnName>City</MicrosoftColumnName>
    </MappingRule>
    <MappingRule>
      <PartnerColumnName>ssid</PartnerColumnName>
      <PartnerColumnNumber>4</PartnerColumnNumber>
      <MicrosoftColumnName>SSID</MicrosoftColumnName>
    </MappingRule>
    <MappingRule>
      <PartnerColumnName>venue</PartnerColumnName>
      <PartnerColumnNumber>7</PartnerColumnNumber>
      <MicrosoftColumnName>HotspotType</MicrosoftColumnName>
    </MappingRule>
        .
        .
        .
        .    
  </Rules>
  <ContainsHeaderRow>true</ContainsHeaderRow>
</MappingRules>
```

