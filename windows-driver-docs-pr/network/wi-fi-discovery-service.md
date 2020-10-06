---
title: Wi-Fi 发现服务概述
description: Wi-Fi 发现服务概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9120d5b1ece092f7c592d0e1ab13d88c8a4542b
ms.sourcegitcommit: 93c924b8f409fc7f704cc67cc026d70b8ad25d30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91739491"
---
# <a name="wi-fi-discovery-service-overview"></a>Wi-Fi 发现服务概述

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]

Wi-fi 发现服务使用户能够通过将移动电话流量卸载到 Wi-fi 热点来降低数据成本。 发现服务从提供程序（如移动运营商和其他源）聚合 Wi-fi 热点数据，以生成已知 Wi-fi 热点目录。 使用此目录，用户可以获取附近位置附近的热点信息。

移动运营商可以通过发送 HTTP POST 请求或使用 Microsoft 提供的命令行工具将热点数据提交给服务。

## <a name="instructions"></a>Instructions

Wi-fi 热点数据必须采用 [Wi-fi 热点数据提交格式](wi-fi-hotspot-data-submission-format.md)中所述的格式。

发现服务要求在一批中提交所有提供者的热点。 每个批处理可包含多个包含较小数据量的提交请求。 例如，包含1000热点的批处理可以通过发送10个提交请求（每个请求都包含100热点的数据）上传到发现服务。 为每个提交请求分配相同的批处理号。 最终提交请求必须包含 `X-FinalBatchRequest` 设置为批处理中的热点总数的标头。 在收到具有此标头的提交请求之前，不会处理该批。 如果标头与该批中的作用点数目不匹配，则不会处理提交。

### <a name="submitting-hotspot-data-by-using-http-post"></a>使用 HTTP POST 提交热点数据

下面的示例演示了一个典型的提交请求。 如果 `X-FinalBatchRequest` 标头和数值为 "1"，则表示此批处理中只有一个作用点，这是最终提交请求。 因此，这是唯一的提交请求。 如果批处理包含多个热点，则应为所有提交请求（最后一个）删除此行。

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

当在目标服务器上接收到消息时， **SubmitHotspots** 将验证该请求并对发送方进行身份验证，然后将热点数据发送到发现服务。

### <a name="submitting-hotspot-data-by-using-the-command-line-tool"></a>使用命令行工具提交热点数据

WifiProviderExe.exe 是 Microsoft 提供的一个命令行工具，它采用热点数据文件作为输入，将其转换为所需的格式，并将其上传到指定的发现服务服务器。

若要运行 WiFiProvider.exe，请使用以下语法：

```cmd
WifiProviderExe –DataFile filename -ProviderId GUID -ServiceEndpoint URL -CustomTransformer filename.dll [-MappingFile filename.xml] [-CertFile filename.pfx] [-CertPassword password] [-CertSubject name]
```

例如：

```cmd
WifiProviderExe -DataFile "file.txt" -ProviderId 00000000-0000-0000-0000-000000000000 -ServiceEndpoint "https://submitwifiservice.windowsphone.com/v1/SubmitHotspots" -CustomTransformer "transformer.dll"
```

下表包含 WiFiProvider.exe 的可能参数的列表。

| 参数 | 说明 |
| --- | --- |
| DataFile | 必需。 包含热点数据的文件的名称。 |
| ProviderId | 必需。 GUID)  (Microsoft 分配的提供程序 ID。 |
| ServiceEndpoint | 必需。 要将热点数据上传到的发现服务服务器的 URL。 |
| CustomerTransformer | 必需。 包含转换器的程序集的名称。 | 
| MappingFile | 可选。 映射文件，该文件将提供程序的热点数据映射到发现服务所需的格式。 |
| CertFile | 可选。 一个指针，指向包含用于身份验证的证书 () 的实际 pfx 文件。 使用此身份验证方法时，必须指定证书密码参数 (**CertPassword**) 。 |
| CertPassword | 可选。 在 **CertFile**中指定的证书的密码。 |
| CertSubject | 可选。 证书的主题名称。 它位于当前用户的 "我的证书存储" 中。 使用此身份验证机制时， **CertFile** 和 **CertPassword** 不是必需的。 但是，必须为证书创建私钥，并在访问控制列表中，向将使用该证书的帐户授予对密钥的访问权限。 |

#### <a name="transformers"></a>Transformers

热点数据可以采用任何格式。 但是，需要指定一个 "数据转换器"，命令行工具可对其进行访问，以将热点数据转换为发现服务所需的格式。

下表显示了通过命令行工具提供的示例转换器。 它们可用于将特定数据格式转换为所需的格式。

| 转换器 | 数据格式 | 说明 |
| --- | --- | --- |
| Microsoft.Wps.WifiService.ProviderSdk.JsonHotspotDataTransformer.dll | JSON | 数据必须符合 [Wi-fi 热点数据提交格式](wi-fi-hotspot-data-submission-format.md)中指定的 JSON 格式。 |
| Microsoft.Wps.WifiService.ProviderSdk.JsonHotspotDataTransformer.dll | 简单 Excel | 您必须提供一个映射文件。 |

#### <a name="mapping-files"></a>映射文件

如果你的热点数据采用简单的 Excel 格式，则必须提供将 Excel 文件中的列映射到相应的必需 JSON 元素的 XML 文件。 以下列表显示允许的列名：

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
* PostalCode
* CountryOrRegion
* Bssids
* ProviderHotspotId
* IsPublic
* IsFree
* PhoneNumbers

下面的示例显示了映射文件的一部分。 每个 **MappingRule** 元素将 Excel 列 (**PartnerColumnName** 和 **PartnerColumnNumber**) 与所需的 JSON 元素 (**MicrosoftColumnName**) 关联。 位于结束规则标记 () 后面的 **ContainsHeaderRow** 元素 `</Rules>` 指示该文件包含一个标题行，该标题行应在读取数据时跳过。

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

