---
title: 移动计划实现
description: 本主题介绍移动计划程序的实现步骤。
ms.assetid: 283E45EF-D421-429B-A9AF-BED64BB670B0
keywords:
- Windows Mobile 计划实现中，移动计划实现的移动运营商
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: f28374cc27e63dd16044cc28f700d8971db4b974
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547006"
---
# <a name="mobile-plans-implementation"></a>移动计划实现

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

本主题介绍 MO 直接门户设计策略和指导，以使用移动计划，以及实现将承载您的计划移动应用中经历的 Web 服务 API 所需的工作。

## <a name="mo-web-portal"></a>MO web 门户

MO 直接使用 web 门户可以移动运营商连接解决方案直接提供给 Windows 用户可以通过在计划移动应用中托管的组织有序的 web 体验。 您需要创建以下设计策略在 web 体验，并实现 web 服务 API，以使其可访问。 

有关 Web 门户的流和引用设计的详细信息，请参阅[Web 门户的流和引用设计](mobile-plans-appendix.md#web-portal-flow-and-reference-design)。

### <a name="web-service-api-hosting-mo-direct-web-portal"></a>Web 服务 API 托管 MO 直接 web 门户 

计划移动应用程序将使用[WebView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.WebView)控件以承载 MO 直接体验。 应用程序只信任由计划移动服务返回的内容。

启动 web 视图时, *EID*，*市场*，和上一个*ICCID*如果可用传递。 下面的示例显示了 esim 卡这些启动三个参数。

```c#
MyWebView.ScriptNotify += MyWebView_ScriptNotify;

List<Uri> allowedUris = new List<Uri>();

allowedUris.AddRange(AllowedNotifyUris);

MyWebView.AllowedScriptNotifyUris = allowedUris;

MyWebView.Navigate(“https://moportal.com?eid=\”eid\”& iccid=8988247000100003319&market=us&transactionId=cvcvcv&location=us”);
```

下面的示例演示为物理 SIM 启动参数： *iccid*，*市场*，并*位置*。 为简便起见，具有已 excised 前面的代码行。

```c#
...

MyWebView.Navigate(“https://moportal.com? iccid=8988247000100003319&market=us&transactionId=waoigFfX00yGH3Vb.1&location=us”);
```

Web 服务 API 必须忽略它可能会收到从计划移动应用程序的额外参数。 这提供了灵活性，以便将引入新功能而不会中断计划移动体验。 如果实现了新的参数，新的参数会被提前告知合作伙伴。

下表介绍可用于 esim 卡和物理 Sim 的启动参数。

| 参数名称 | 描述 | 示例 |
| --- | --- | --- |
| 事件 id | Esim 卡标识符。 这是发送仅当存在 esim 卡时。 | `eid= 89033024010400000100000000009136` |
| iccid | 物理 SIM 所需的参数。 Esim 卡的可选参数。 指定可用 ICCID 上物理 sim。 | `iccid=8988247000100003319` |
| iccids | 可选参数。 Esim 卡仅在指定的 ICCID 的可用配置文件中的列表。 如果有任何 ICCID 的匹配 MO esim 卡上可用，将不会发送此参数。 | `iccids=8988247000100003319, 988247000100003555` |
| 位置 | 用户的当前物理位置与国家/地区级粒度。 | `location=us` | 
| transactionId | 用于在调试会话的事务 ID。 提供商应记录此项，并将其发送通知有效负载中。 最大大小为 64 个字符。  | `transactionId=waoigFfX00yGH3Vb.1` |
| market | 在 PC 中的区域设置的两字母 ISO 代码。 | `market=us` |

可使用 Accept-language 标头，如下表中所述发送用户的语言首选项。

| 标头名称 | 描述 | 示例 |
| --- | --- | --- |
| Accept-Language | 用户的当前语言设置。 如果可能，MO 门户应呈现中指定的语言的内容。 | `Accept-Language: en-us` |

### <a name="mo-direct-flow-diagram"></a>MO 直接流关系图

Esim 卡 MO 直接为以下的高级数据流关系图说明了用户不具有安装 MO 配置文件，而购买从 MO 门户计划。

<img src="images/dynamo_implementation_mo_direct_flow_no_profile.png" alt="MO Direct flow where user has no MO profile" title="MO 直接流，其中用户具有无模式配置文件" width="800" />

下图显示 MO 直接的高级流时用户具有 esim 卡配置文件，或在其设备中使用物理 SIM。

<img src="images/dynamo_implementation_mo_direct_flow_with_sim.png" alt="MO Direct flow where user has an eSIM or physical SIM" title="在用户具有 esim 卡或物理 SIM MO 直接流" width="400" />

### <a name="control-handoff-to-the-mobile-plans-app"></a>控件切换到计划移动应用

用户完成购买流，通过在成功购买或取消购买后 MO 门户必须返回到计划移动应用的控件。 这是通过使用与 MO 门户的用户交互的结果为应用程序发出通知。 可以使用以下语法使用 JavaScript 发送通知：

```javascript
DataMart.notifyPurchaseResult(notificationPayload);
```

Esim 卡通知有效负载的示例如下所示：

```json
{
"ver":"1",
"purchaseResult":
“{
\"userAccount\":\"New\",
\"purchaseInstrument\":\"New\",
\"line\":\"New\",
\"moDirectStatus\":\"Complete\",
\"planName\":\"MyPlan\"
}”,
"success":true,
"Iccid":"8988247000100297655",
"activationCode":"activationCode",
"transactionId":"CDE2882E-BD5E-485F-B921-D0D60BBCF7FF"
}
```

物理 SIM 通知有效负载的示例如下所示：

```json
{
"ver":"1",
"purchaseResult":
{
\"userAccount\":\"New\",
\"purchaseInstrument\":\"New\",
\"line\":\"New\",
\"moDirectStatus\":\"Complete\",
\"planName\":\"MyPlan\"
},
"success":true,
"iccid":”8988247000100297655”,
"transactionId":"CDE2882E-BD5E-485F-B921-D0D60BBCF7FF"
}
```

从其发送通知的月门户 URI 必须是安全的 https 协议中。 下表介绍通知的 JSON 有效负载中的每个字段：

| JSON 字段 | 在任务栏的搜索框中键入 | 描述 | 示例 |
| --- | --- | --- | --- |
| success | 布尔 | 如果用户购买 MO 直接计划，则为 true。 | `“success”:true` |
| iccid | 字符串 | 对于 esim 卡，这指示 ICCID 客户端必须用于使用月直接购买的计划。 | `iccid:”8988247000100297655”` |
| activationCode | 字符串 | 要检索的 esim 卡配置文件的激活代码。 | `“ActivationCode”` |
| transactionId | 字符串 | 事务 ID MO 门户作为查询参数时收到门户已启动。 | `transctionId= rRi8OzhI3EiR02nm.2.0.1` | 
| purchaseResult | JSON | 包含与 MO 门户的用户交互的详细信息。 |   |
| userAccount | 枚举 | 此字段为必需字段。 <p>可能值：</p><ul><li>新建：指示用户已创建了新的用户帐户。</li><li>现有:指示用户记录的现有用户帐户。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None：指示用户未到达此步骤。</li></ul> | `“userAccount”:”New”` |
| purchaseInstrument | 枚举 | 此字段为必需字段。 <p>可能值：</p><ul><li>新建：指示用户已创建了新的用户帐户。</li><li>现有:指示用户记录的现有用户帐户。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None：指示用户未到达此步骤。</li></ul> | `“purchaseInstrument”:”New”` |
| 行 | 枚举 | 此字段为必需字段。 <p>可能值：</p><ul><li>新建：指示 SIM 卡已添加的用户帐户。</li><li>现有:指示是否传输的现有行到设备。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None：指示用户未到达此步骤。</li></ul> | `“line”:”New”` |
| moDirectStatus | 枚举 | 此字段为必需字段。 <p>可能值：</p><ul><li>完成：指示用户已成功完成购买。</li><li>服务错误：表示用户无法完成购买由于月服务错误。</li><li>InvalidSIM:表示传递给在门户 ICCID 时不正确。</li><li>LogOnFailed:表示用户无法登录到 MO 门户。</li><li>PurchaseFailed:指示在购买由于计费错误而失败。</li><li>ClientError:指示无效的参数已传递到门户。</li><li>BillingError:指示已具有用户计费的错误。</li></ul> | `“moDirectStatus”:”Complete”` |
| planName | 字符串 | 对于成功的事务，此字段必须不为空，并提供一个描述性的计划名称。 对于失败的事务，此字段必须是空字符串。 | `“planName”:”prepaid_3GperMonth”` |

### <a name="web-portal-design-policies"></a>Web 门户设计策略

若要确保在 Windows 上的最佳用户体验，你应遵循本部分中的策略开发 MO 直接体验时。 这些政策是补充条款和条件移动计划合作伙伴附录[Windows 应用开发人员协议](https://msdn.microsoft.com/library/windows/apps/hh694058)并[Microsoft Store 策略](https://msdn.microsoft.com/library/windows/apps/dn764944)。

#### <a name="business-functions"></a>业务功能

| 策略 | 引起或建议 |
| --- | --- |
| MO 直接体验必须满足中提供的国家/地区的所有适用法律和法规要求。 MO 直接门户中显示任何内容必须遵守所有适用法律。 | 必需 |
| 提供通过 MO 亲身体验产品必须是用于网络连接的产品/服务。 | 必需 |
| 用户完成购买流程后，通过 MO 亲身体验提供的网络连接产品必须立即激活。 | 必需 |
| 提供通过 MO 直接体验的网络连接产品必须清除服务的详细信息。 任何特定条款必须是服务的可供用户查看之前的月直接体验的购买。 | 必需 |
| 客户支持联系信息必须可供 MO 直接体验中的用户访问。 | 必需 |
| 隐私策略必须可供用户查看月直接体验中。 | 必需 |
| 月，可以是月直接体验、 单独的专用帐户管理门户中或专用的月应用程序中，提供的帐户管理体验应使用户能够执行操作，如取消其当前的数据计划订阅。 | 必需 |
| 用户将收到订单确认后已成功购买 MO 直接体验从数据计划。 | 推荐 |


#### <a name="security"></a>安全性

| 策略 | 引起或建议 |
| --- | --- |
| MO 直接体验不得交付或安装任何第三方拥有或经过品牌打造的应用程序或模块。 | 必需 |
| 用户退出 MO 直接体验之前，用户必须是安全地从注销 MO 直接门户。 | 必需 |
| MO 直接门户 URI 和所有请求或发往和来自 MO 直接门户通知，必须都使用安全 HTTPS 协议。 | 必需 |
| 所有 MO 门户资源和引用必须都使用安全 HTTPS 协议。 | 必需 |

#### <a name="advertising"></a>广告

| 策略 | 引起或建议 |
| --- | --- |
| MO 直接门户不显示任何播发、 赞助的内容、 视频、 大型图像、 动画或映射。 | 必需 |

#### <a name="capabilities"></a>功能

| 策略 | 引起或建议 |
| --- | --- |
| MO 直接体验所需最小功能是使用户能够注册到移动运营商的帐户购买数据计划。 | 必需 |
| MO 直接门户必须立即启动并仍能响应用户输入之前在用户退出 MO 直接体验。 | 必需 |
| 在调用之后，MO 直接门户必须有并且之前保留用户焦点： <ul><li>MO 直接流已完成并且焦点已返回到计划移动应用程序中，返回由移动运营商</li></ul><p>或者</p><ul><li>用户已取消 MO 直接流。</li></ul> | 必需 |
| MO 直接门户不得显示任何弹出窗口、 打开任何其他窗口，或将用户重定向到其他网站或应用程序，除如完成采购流程所需。 | 必需 |
| MO 直接门户必须处理所有合法错误和异常，如拒绝支付方法的后端故障等。处理错误或异常后，MO 直接门户必须保留响应的用户可以退出并返回到 Microsoft Store。 | 必需 |
| 如果用户遇到一个错误，可以修复与用户操作，建议显示移动运营商客户支持信息并显示错误消息。 | 推荐 |

#### <a name="usability"></a>可用性

| 策略 | 引起或建议 |
| --- | --- |
| MO 直接门户默认帧大小为 800 x 600。 采用响应式 web 设计，以便可以自动调整以适应 web 控制帧，当用户调整大小时计划移动应用上个月直接门户的内容。 | 必需 |
| 应该优化加载时间和数据加载 MO 直接体验的消耗。 | 必需 |
| MO 直接体验应该非常简单的和易于屏幕导航需要与指导原则。  | 必需 |
| 上个月直接门户应提供与计划移动应用，不让人困惑的用户或提醒用户的整体体验集成，此 UI 元素是一个嵌入式的 web 控件。 例如，应为月直接门户中的没有最小关闭/最大值按钮。 | 必需 |
| MO 直接门户中的 web 页面的布局应为干净且轻松地导航。 用户可以向后导航和向前浏览 MO 直接门户使用月直接体验的 UI 元素中的 web 页面。 有关详细信息，请参阅[Web 门户的流和引用设计](mobile-plans-appendix.md#web-portal-flow-and-reference-design)。 | 必需 |
| MO 直接门户必须在 Web 控件内正常运行，并调用后，它必须不会干扰用户的交互与计划移动应用在任何时间。 | 必需 |
| MO 直接门户不必须使用太多图像、 横幅，耗时较长的文本、 外部链接、 等杂乱。 | 必需 |
| 屏幕上直接 MO 体验中的取消按钮应可供用户退出时适用的流。 | 推荐 |
| 移动运营商可以选择的配色方案和表示品牌的字体最佳。 请确保所有可视化元素良好地协同工作，并加强了品牌。 | 推荐 |

#### <a name="localization"></a>本地化

| 策略 | 引起或建议 |
| --- | --- |
| MO 直接门户应能够接收并理解用户的区域设置传递由计划移动服务以适当语言显示的内容。 | 必需 |
| 移动运营商可能会对他们想要支持的语言中的月直接门户进行本地化。 | 推荐 |
| 尽管数据计划可用性区域之间各异，MO 直接门户提供的体验应为所有语言的支持，以合理方式类似。 | 推荐 |

#### <a name="accessibility"></a>辅助功能

| 策略 | 引起或建议 |
| --- | --- |
| MO 直接门户应为已禁用的用户提供可访问性，并且遵守适用于管辖权地，移动运营商实现，并使 MO 直接体验的可访问性准则。 | 推荐 |