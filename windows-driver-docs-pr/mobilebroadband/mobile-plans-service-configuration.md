---
title: 计划移动服务配置
description: 本主题介绍移动计划程序的配置步骤。
ms.assetid: 95122BBB-0466-4130-9209-7EC6545DFD4D
keywords:
- Windows Mobile 计划配置中，移动计划配置移动操作员
ms.date: 02/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 771d2674cff145f064aa960b7d18417c08aacfdf
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903659"
---
# <a name="mobile-plans-service-configuration"></a>计划移动服务配置

本主题介绍如何在 Windows Mobile 计划支持的连接设备上构建基础。 它详细介绍了如何配置 esim 卡配置文件，以确保获得最佳使用者体验，以及如何提供可确保移动计划的服务配置信息正确呈现体验在 Windows 设备上。

## <a name="esim-profile-configuration-requirements"></a>esim 卡配置文件配置要求

你必须准备 esim 卡配置文件满足以下要求：

- Esim 卡配置文件不能锁定的 PIN。
- 必须从你 SM 中删除的 esim 卡配置文件-DP + 服务器直到接收确认配置文件下载已成功完成。 可重复使用的激活代码以重试下载相同的配置文件时下载此前在尝试已失败。
- Esim 卡配置文件不能"不删除"执行停用"策略设置。
- 激活代码不能包含任何前缀如"LPA:"。
- MO 直接流后立即提供了该激活代码。
- 激活代码不得要求"确认代码"。

### <a name="esim-profile-testing"></a>esim 卡配置文件测试

应移动运营商执行验证以确保可以在不同的 Windows 设备上安装其 esim 卡配置文件。 为此，建议源一些 esim 卡支持的设备，并使用 Windows 设置应用来下载、 安装和激活配置文件。

## <a name="service-configuration"></a>服务配置

计划移动服务必须引入一些配置信息，以支持移动运营商。 若要开始配置过程，请发送电子邮件至[Mobile 计划实现支持](mailto:mpimplementation@microsoft.com)。

### <a name="minimum-configuration-information"></a>最小的配置信息

1. 想要用于你的产品的品牌名称。
2. 品牌徽标。 所需的分辨率为 300 x 300 像素。 映像也应该是完整出血以不透明。
3. 你的解决方案支持的国家/地区的列表。 请使用[ISO 3166 代码](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)创建列表 （用逗号分隔）。
4. MO 直接门户 URI （不支持本地化）。 这应该是*https*地址。 不支持端口号。
5. 一种通知 URI。 这是从何处的主机地址的 Javascript 回调函数 ([回调通知](mobile-plans-callback-notifications.md)) 将会运行。 这应该是*https*地址。 不支持端口号。
6. ICCID 范围或你想要想要将与相关联的范围*移动计划*。

下图显示了一个示例，用于*标准网关页*计划移动应用中。 "A"批注对应于该品牌徽标提交，和"B"批注与品牌名称相对应。

<img src="images/mobile_plans_configuration_mo_page.png" alt="Mobile Plans mobile operator page - asset usage example" title="移动计划移动运营商页-资产使用情况示例" width="600" />

### <a name="enhanced-gateway-page"></a>增强的网关页

这是在计划移动应用程序版本中支持的可选功能**5.1902.331.0**或更高版本。

可以使用移动运营商品牌外观和感觉，以突出显示其产品/服务增强标准登录页面。

#### <a name="enhanced-gateway-content"></a>内容增强网关

增强的网关内容定义包含以下元素中使用的 JSON 文件：

```JSON
{ // Root object
  "promotionTemplates": [
    { // PromotionTemplate
      "id": 0,
      "backgroundColor": "0x000000FF", // Black
      "bodyFontColor": "0xFFFFFFFF", // White
      "buttonColor": "0x414243FF", // Grey
      "buttonFontColor": "0xFFFFFFFF", // White
      "bodyText": "We’ll help you find a plan so you can get connected when W-Fi isn’t available",
      "buttonText": "Get started",
      "hyperlinkColor": "0xBB8CF9FF", //Purple
      "images": [
        { // Image
          "height": 480,
          "uri": "https://content.windows.com/MO1/landing740x480.png",
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
| 根对象 | promotionTemplates | 升级模板要显示在网关页的列表。 为每个移动运营商支持只有一个升级模板。 | 不可用 |
| PromotionTemplate | id | 有关模板的唯一字符串标识符。 | 123 |
|   | backgroundColor | 网关页背景色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义，白色用作默认值。 | 0x000000FF |
|   | bodyFontColor | 正文文本的字体颜色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义的黑色用作默认值。 | 0xFFFFFFFF |
|   | buttonColor | 启动移动运营商门户的"继续"按钮的颜色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义，则用户选择的系统突出显示颜色用作默认值。 | 0x414243FF |
|   | buttonFontColor | "继续"按钮上文本的字体颜色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义，白色用作默认值。 | 0xFFFFFFFF |
|   | bodyText | 客户端的语言的本地化的正文文本。 | 我们将帮助你查找计划，因此你可以获取连接的 Wi-fi 不可用时。 |
|   | buttonText | "继续"按钮的本地化的文本。 | 立即开始行动 |
|   | hyperlinkColor | 在网关页的超链接将使用此颜色。 此字段是采用的格式的十六进制字符串`0xRRGGBBAA`。 如果未定义，将使用默认超链接颜色。 | 0xBB8CF9FF |
|   | images | 若要将模板映像。 支持不同的大小。 如果包含多个大小，计划移动应用使用的最佳大小的屏幕分辨率。 最大图像大小为 1200 x 600 像素，文件格式*png*。| ![移动计划图面上的登录页示例，780 x 480](images/mobile_plans_surface_landing_780x480.png) |

#### <a name="example-enhanced-gateway-landing-page"></a>示例增强网关登陆页面

![在计划移动应用中的示例增强网关登陆页面](images/mobile_plans_sample_landing_page.png)