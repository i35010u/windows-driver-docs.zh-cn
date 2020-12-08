---
title: "\"移动计划网关\" 页"
description: "\"移动计划网关\" 页"
keywords:
- Windows Mobile 计划移动运营商
ms.date: 07/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 8ce9d5406937fc94e1d08aac84bf979411e53f08
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832961"
---
# <a name="mobile-plans-gateway-page"></a>"移动计划网关" 页

## <a name="overview"></a>概述

移动计划应用为在目录中启用的每个移动运营商托管一个网关页面。 "网关" 页在 "欢迎" 步骤中显示给最终用户。 它包含移动运营商的基本品牌元素，还包含多个链接和隐私免责声明。 "网关" 页还包含一个用于调用移动运营商 web 门户的按钮。

## <a name="enhanced-gateway-page"></a>增强网关页

这是移动计划应用版本 **5.1902.331.0** 或更高版本中支持的一项可选功能。

移动运营商可以通过指定页面的内容和样式来自定义 "网关" 页。 这可确保他们能够突出显示其产品和独特品牌价值。

### <a name="enhanced-gateway-page-content"></a>增强的网关页内容

"增强网关" 页是使用模板和预定义元素指定的。 突出显示的元素由移动运算符定义。

![增强的网关页模板](images/enhanced_gateway_page_template.png)

### <a name="enhanced-gateway-page-templates"></a>增强的网关页模板

"增强网关" 页上显示的自定义内容是使用包含以下元素的 JSON 文件定义的：

```JSON
{ // Root object
  "promotionTemplates": [
    { // PromotionTemplate
      "id": 0,
      "backgroundColor": "0x000000FF", // Black
      "bodyFontColor": "0xFFFFFFFF", // White
      "bodyText": "Stay connected from virtually anywhere.",
      "buttonColor": "0x00B0F0FF", // Light Blue
      "buttonFontColor": "0xFFFFFFFF", // White
      "buttonText": "Get started",
      "hyperlinkFontColor": "0x00B0F0FF", //Light Blue
      "images": [
        { // Image
          "uri": "https://picsum.photos/id/1/740/480",
          "width": 740,
          "height": 480,
        }
      ]
    }
  ]
}
```

下表描述了上一示例中的每个 JSON 元素。

| JSON 元素 | 字段名称 | 说明 | 示例 |
| --- | --- | --- | --- |
| 根对象 | promotionTemplates | 要用于 "增强网关" 页的模板列表。 可以为每个移动运营商定义一个或多个模板。 | 空值 |
| PromotionTemplate | id | 每个模板的唯一字符串标识符。 仅定义一个模板时的默认值应为 "0" | 123 |
|   | backgroundColor | 网关页面背景的颜色。 此字段是格式为的十六进制字符串 `0xRRGGBBAA` 。 如果未定义，将使用白色作为默认值。 | 0x000000FF |
|   | bodyFontColor | 正文文本的颜色。 这是格式为的十六进制字符串 `0xRRGGBBAA` 。 如果未定义，将使用黑色作为默认值。 | 0xFFFFFFFF |
|   | bodyText | 客户端语言的本地化正文文本。 请注意，不能更改免责声明文本。| 随时随地保持连接状态。 |
|   | buttonColor | 启动移动运营商 web 门户的 "继续" 按钮的颜色。 此字段是格式为的十六进制字符串 `0xRRGGBBAA` 。 如果未定义，则使用用户选择的系统突出显示颜色作为默认值。 | 0x00B0F0FF |
|   | buttonFontColor | "继续" 按钮上的文本颜色。 此字段是格式为的十六进制字符串 `0xRRGGBBAA` 。 如果未定义，将使用白色作为默认值。 | 0xFFFFFFFF |
|   | buttonText | "继续" 按钮的本地化文本。 | 入门 |
|   | hyperlinkFontColor | 超链接的颜色。 此字段是格式为的十六进制字符串 `0xRRGGBBAA` 。 如果未定义，则使用用户选择的系统突出显示颜色作为默认值。 | 0x00B0F0FF |
|   | images | 要用于模板的图像。 支持不同的大小。 如果包括多个大小，则移动计划应用将使用屏幕分辨率的最佳大小。 最大图像大小为 1200 x 600 像素，文件格式为 *png*。| https://picsum.photos/id/1/740/480 |

### <a name="sample-enhanced-gateway-page"></a>示例 "增强网关" 页

![移动运营商网关页](images/mobile_operator_gateway_page.png)

### <a name="using-multiple-gateway-page-templates"></a>使用多个网关页模板

移动运营商可以选择定义多个网关页面模板。 如果完成此操作，移动计划服务将在运行时调用移动运营商 API，以请求应向用户显示的模板的 ID。

由于请求包括配置文件和设备的标识符，因此移动运营商可以为不同的用户段定义多个模板。 这可用于进行 A/B 测试，或向邀请用户注册的新用户显示一个模板，并使用不同的模板返回用户购买额外余额。 网关页面模板还可以与移动计划通知结合，以创建高度针对性的 campgains。

> [!NOTE]
> 如果设备没有适用于移动运营商的活动配置文件，则不会发出请求，并且默认情况下将使用模板 ID "0"。

Get 产品/服务请求返回向用户显示的模板 ID。

![移动计划获取提供 Callflow](images/mobile_plans_get_offers_callflow.png)

### <a name="getoffers-api-specification"></a>GetOffers API 规范

在 `GetOffers` 显示移动运营商网关页面之前调用 API。 移动计划服务是此请求的代理。

```HTTP
GET https://{offerUri}sims/{simmri}/offers?limit=1&imei=1234
```

- 在移动运营商的服务配置过程中， *{offerUri}* 是 offerUri 值载入。

终结点有两个查询参数：
- *限制*，这是必需的，它指定要返回的产品/服务的数量。
- *imei* 是可选的，它指定客户端的 imei。

响应是一个 JSON 对象，其中包含一个名为 " *产品/服务* " 的属性，其中包含一个产品/服务列表。 此列表中的产品/服务数最多 *限制* 请求。 此列表中的每个产品/服务都是一个具有单个属性 *gatewayId* 的对象，该对象必须标识移动运营商的服务配置中的现有网关。

下面是使用此终结点进行交互的示例：

```HTTP
GET https://moendpoint.com/v1/sims/iccid:8988247000100003319/offers?limit=1&imei=1234
X-MS-DM-TransactionId: "MSFT-12345678-1234-1234-1234-123456789abc"

HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: "MSFT-12345678-1234-1234-1234-123456789abc"
{
  "offers" : [
   {
      "gatewayId": "0"
    }
  ]
}
```

## <a name="standard-gateway-page"></a>标准网关页

如果未定义增强网关页面，则会向最终显示 "标准网关" 页。 如果为移动运营商的增强网关页面加载内容时出现问题，则 "标准网关" 页还可以显示为降级的 experiend。

"标准网关" 页使用的是移动运营商无法自定义的基本模板。

![标准网关页](images/standard_gateway_page.png)
