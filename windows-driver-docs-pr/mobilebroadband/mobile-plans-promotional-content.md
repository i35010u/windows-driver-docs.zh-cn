---
title: 移动计划促销内容
description: 移动计划促销内容
ms.assetid: FB789462-732C-436A-B69C-43940F7F8A77
keywords:
- Windows Mobile 计划促销内容移动运营商
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7dee8cee963f766c18e915f51ea85d0065030deb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546353"
---
# <a name="mobile-plans-promotional-content"></a>移动计划促销内容

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

## <a name="overview"></a>概述

本主题提供移动运营商如何创建和提交计划移动应用中的促销活动内容的说明。

## <a name="promotional-notifications"></a>促销通知

Windows 包括对包含文本、 图像和按钮输入交互式 toast 通知的支持。 计划移动应用允许移动运营商可以触发应用的 toast 通知中显示促销内容。

## <a name="promotional-gateways"></a>促销网关

计划移动应用包括每个移动运营商的登录页。 使用促销要突出显示的品牌或市场活动消息的内容，可以自定义登录页。

### <a name="promotional-gateway-content"></a>促销网关的内容

使用带有以下元素的 JSON 文件定义促销的网关的内容：

```JSON
{ // Root object
  "promotionTemplates": [
    { // PromotionTemplate
      "id": 123,
      "backgroundColor": "0x000000FF", // Black
      "bodyFontColor": "0xFFFFFFFF", // White
      "buttonColor": "0x414243FF", // Grey
      "buttonFontColor": "0xFFFFFFFF", // White
      "bodyText": "We’ll help you find a plan so you can get connected when W-Fi isn’t available",
      "buttonText": "Get started",
      "images": [
        { // Image
          "height": 480,
          "uri": "https://storagetos.datamart.windows.com/MO1/v1/en-US/landing740x480.png",
          "width": 740,
        }
      ]
    }
  ]
}
```

下表描述了上一示例中的每个 JSON 对象。

| JSON 对象 | 字段名称 | 描述 | 示例 |
| --- | --- | --- | --- |
| 根对象 | promotionTemplates | 升级模板要显示在网关页的列表。 为每个移动运营商支持只有一个升级模板。 | 不适用 |
| PromotionTemplate | id | 有关模板的唯一字符串标识符。 | 123 |
|   | backgroundColor | 网关页背景色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义，白色用作默认值。 | 0x000000FF |
|   | bodyFontColor | 正文文本的字体颜色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义的黑色用作默认值。 | 0xFFFFFFFF |
|   | buttonColor | 启动移动运营商门户的"继续"按钮的颜色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义，则用户选择的系统突出显示颜色用作默认值。 | 0x414243FF |
|   | buttonFontColor | "继续"按钮上文本的字体颜色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义，白色用作默认值。 | 0xFFFFFFFF | 
|   | bodyText | 客户端的语言的本地化的正文文本。 | 我们将帮助你查找计划，因此你可以获取连接的 Wi-fi 不可用时。 |
|   | buttonText | "继续"按钮的本地化的文本。 | 立即开始行动 |
|   | images | 若要将模板映像。 支持不同的大小。 如果包含多个大小，计划移动应用使用的最佳大小的屏幕分辨率。 | ![移动计划图面上的登录页示例，780 x 480](images/mobile_plans_surface_landing_780x480.png) |

### <a name="example-promotional-gateway-landing-page"></a>示例促销网关登陆页面

![在计划移动应用中的示例促销网关登陆页面](images/mobile_plans_sample_landing_page.png)