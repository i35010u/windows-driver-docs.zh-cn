---
title: 计划 Windows 10 的移动设备体验
description: 本主题介绍 Windows 设备体验之后移动计划激活。
ms.assetid: E97AD441-86F7-439C-9800-7DD93AAC0545
keywords:
- 计划 Windows 移动设备体验，移动计划移动运营商
ms.date: 03/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: bc34176a2626e104e047490877fc68bd27fc964b
ms.sourcegitcommit: 1a1a78575e89bf8cd713bf1dac8a698db3cddfe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58845556"
---
# <a name="mobile-plans-windows-10-device-experience"></a>计划 Windows 10 的移动设备体验

本主题介绍了移动计划程序产品/服务以确保该移动运营商的客户体验符合移动运营商产品/服务的功能。

## <a name="basic-device-experience"></a>基本设备体验

本部分介绍用于配置内容的选项*查看我的帐户*链接将显示 Windows 连接管理器中也已知，也称为网络浮出控件。

*查看我的帐户*链接无法配置为：

- 启动 web 浏览器并打开定义的 web 页。
- 启动计划移动应用并打开移动计划 Web 门户。

 一旦您已决定在其中一个选项，请请求 COSA 数据库更新，以实现正确的行为。 有关详细信息，请参阅[规划你的桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。

以下设置也适用于上面的选项：

- *AccountExperienceURL*。 此参数定义 web 页。
- *AppID*。 此参数定义的应用程序启动。 若要使用计划移动应用，配置_Microsoft.OneConnect_8wekyb3d8bbwe ！应用_。

下图显示了网络浮出控件的示例：

<img src="images/mobile_plans_network_flyout_basic.png" alt="Windows Connection Manager showing basic MO" title="显示基本月 Windows 连接管理器" width="250" />

## <a name="enhanced-device-experience"></a>增强的设备体验

通过实施增强的设备体验，可以向客户提供以下优势：

- 客户可以了解多少数据不可用，以及其订阅到期，网络浮出控件中之前的剩余时间量。
- 客户可以排名靠前注册其预付订阅通过移动连接，即使它们用完预付余额或其订阅已过期。
- 你可以管理网络飞出式产品/服务基于客户的订阅状态。

这些体验之上构建[基本的设备体验](#basic-device-experience)，这是设备网络浮出控件中的默认体验。

### <a name="network-flyout-user-experience"></a>网络浮出控件的用户体验

根据从收到的信息`GetBalance`API 调用网络浮出控件的行为不同，该技术增强了用户体验。

网络浮出控件具有以下元素：

1. 连接与某一数据计划。 这将启动计划移动应用。
2. 查看我的帐户。 行为根据[基本的设备体验](#basic-device-experience)。
3. 余额信息。 显示余额可用，以提供您`GetBalance`响应。

下图显示了这些网络浮出控件元素。 使用数据连接与一个对应的计划、 查看我的帐户对应于 B，和余额信息对应于 c。

<img src="images/dynamo_prepaid_network_flyout_5_getbalance.png" alt="Windows Connection Manager showing behavior depending on GetBalance API calls" title="Windows 连接管理器显示具体取决于 GetBalance API 调用的行为" width="600" />

若要提供网络浮出控件中正确的信息，MOs 提供*类型*并*平衡*（dataRemainingMB 和 timeRemaining） 中定义的信息[GetBalance API](#getbalance-api)部分。

下表提供了之间的引用`GetBalance`响应类型和网络浮出控件中显示的内容。

| GetBalance 响应类型 | 显示网络浮出控件... |
| --- | --- |
| MODIRECT | "查看我的帐户"，仅使用不平衡的信息 |
| MODIRECTPAYG | "查看我的帐户"并进行平衡信息 |
| NONE | "连接与某一数据计划" |
| NOTSUPPORTED | "查看我的帐户"仅 |

## <a name="getbalance-api"></a>GetBalance API

> [!IMPORTANT]
> 请申请[Windows COSA 更新后，获取余额](#how-to-enable-get-balance-in-windows-cosa)在 Windows 中。

`GetBalance` API 查询当前订阅状态、 是否移动计划体验是在设备上可用的控件，并显示预付订阅的网络浮出控件中的剩余数据和时间。 下图显示的高级流`GetBalance`API。

<img src="images/mobile_plans_get_balance_api_flow.png" alt="GetBalance API flow" title="GetBalance API 流" width="600" />

### <a name="resource-model"></a>资源模型

计划移动服务和月服务之间的通信涉及到操作在下图中的资源。 以下关系图的表中的每个资源的说明。

<img src="images/mobile_plans_get_balance_resource.png" alt="GetBalance API resource model diagram" title="GetBalance API 资源模型关系图" width="600" />

#### <a name="sim-resource"></a>SIM 资源

> [!NOTE]
> SIM 资源当前不支持"创建，""读取"、"更新"或"删除"操作。

| JSON 属性 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
| Iccid | 字符串 | 已创建的配置文件的 ICCID。 |

#### <a name="balance-resource"></a>平衡资源

| JSON 属性 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
|id |字符串| 移动运营商内部 id，用于跟踪的事务 |
在任务栏的搜索框中键入 | 枚举 | 可能值： <ul><li>MODIRECT:指示如果用户余额 MO 直接。</li><li>MODIRECTPAYG:指示如果用户余额 MO 直接 PAYG。</li><li>NONE:指示用户已不平衡。 当剩余余额为 0，但该计划未过期时，我们希望收到"NONE"，以便用户可以购买数据计划。</li><li>NOTSUPPORTED:指示 sim 卡不支持的移动计划体验。 时 SIM 不应在使用"NOTSUPPORTED"* 移动计划支持的范围。 我们将关闭网络浮出控件中的计划移动体验，并收到此类型的计划移动应用中返回的一般性错误消息。</li></ul> |
| dataRemainingInMB | Double | 将计划保留在当前用户的数据，以 mb 为单位。 |
| timeRemaining | 字符串 | 中指定的持续时间[ISO 8601](https://go.microsoft.com/fwlink/p/?linkid=866182)。 |

### <a name="headers"></a>标头

从计划移动服务到 mobile 提供程序的终结点的每个请求中，可能包含以下标头。

| 标头名称 | ReplTest1 | 描述 |
| --- | --- | --- |
| X-MS-DM-TransactionId | 字符串 | 若要唯一标识此请求/响应交互之间移动计划服务和月服务 TransactionId。 |
| 授权 （可选） | 字符串 | 密苏里州 （可选） 提供一个基本身份验证字符串 |

### <a name="error-codes"></a>错误代码

下表定义的 HTTP 响应中应使用的错误代码。

| 错误代码 | 描述 |
| --- | --- |
| HTTP 200 （正常） | 已成功完成该操作。 此代码还应该用于指示用户是否应执行的指定位置中有 0 平衡使用 dataRemainingInMB = 0 和 timeRemaining ="PT0S"使用 HTTP 200。 |
  HTTP 201 （已创建） | 指示已成功完成该操作和资源已成功创建。 |
| HTTP 400 （错误请求） | 使用无效的查询参数、 标头无效，或有效负载无效。 在响应正文中，应指示不正确的参数。 例如，如果指定了无效的 fieldsTemplate，必须返回此错误代码的响应正文中的详细信息。 |
| HTTP 401 （未经授权） | 身份验证凭据不正确或无效。 这可能时传递的基本身份验证凭据不正确。 |
| HTTP 403 （禁止访问） | 客户端证书是不受信任或无效。 如果 MTLS 一部分包含的客户端证书无效，应返回 HTTP 403。 |
| HTTP 404 （找不到） | 该资源不存在时，MO 服务应返回此错误。 这可能不正确的 ICCID 发送时。 这不应该用于指示用户不指示使用 HTTP 200 （正常） 的指定位置中具有一种平衡。 |
| HTTP 409 （冲突） | 如果 TransactionId 重复，使用。 |
| HTTP 429 (太多的请求) | 月服务使用它来指示计划移动服务中指定的时间内发送过多的请求。 在响应中，MO 服务必须使用重试间隔标头以指示资源的时间之后计划移动服务应重试。 在响应正文中，可以提供可选的详细信息。 |
| HTTP 500 （内部错误） | 出现意外情况的月服务上。 月服务应该包含错误，只要有可能的原因，使它可用于根据需要进一步调试。 |

### <a name="getbalance-api-specification"></a>GetBalance API 规范

`GetBalance`网络浮出控件显示在 Windows 设备时调用 API。 计划移动服务是为此通信的代理。

此调用通过 HTTP 请求，其中*moBaseUrl*是月托管服务的终结点并*sim id*是 ICCID:

```HTTP
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US HTTP/1.1
```

查询参数：

| 查询参数名称 | ReplTest1 | 描述 |
| --- | --- | --- |
| 位置 | 字符串 | 可选。 用户余额正在查询的位置。 如果未指定，应所有活动的余额。 **请注意**位置参数是区分大小写。 |
| limit | 整型 |可选。 要返回的余额的最大计数。 如果未指定，则应返回所有余额。 |
| fieldsTemplate | 枚举 |指定必须在资源中返回的字段的列表。 <p>可能值：</p><ul><li>Basic:*类型*， *dataRemainingInMB*，并*timeRemaining*中平衡资源必须返回。</li><li>完整:必须返回平衡资源中的所有属性。</li></ul> |

以下一系列示例显示的调用流`GetBalance`API。

#### <a name="example-1-returning-the-first-balance-that-is-available-for-the-user-in-us"></a>示例 1：返回可用于美国用户的第一个余额

```HTTP
GET https://moendpoint.com/v1/sims/iccid: 8988247000100003319/balances?fieldsTemplate=basic&limit=1&location=us HTTP/1.1
X-MS-DM-TransactionId: “MSFT-12345678-1234-1234-1234-123456789abc”
```

HTTP 响应：

```HTTP
HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: “12345”

{
“balances”: [
    {
         “id”: “23445”,
         “type”: “MODIRECTPAYG”,
         “dataRemaininginMB”: 123.0,
         “timeRemaining”: “P23DT23H”
    }
  ]
}
```

如果成功，则此方法将返回用户的平衡。

JSON 的响应：

| 数据 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
| 余额 | 集合 | 余额的集合。 |

#### <a name="example-2-the-expected-response-for-a-sim-that-is-in-the-cosa-iccid-range-but-should-not-be-supported-by-mobile-plans"></a>示例 2：SIM COSA ICCID 范围内，但不应受移动计划预期的响应

HTTP 请求：

```html
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US
HTTP/1.1
```

JSON 的响应：

```json
HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: “12345”

{
“balances”: [
    {
         “id”: “23445”,
         “type”: “NOTSUPPORTED”,
         “dataRemaininginMB”: 0.0,
         “timeRemaining”: “PT0S”
    }
  ]
}
```

### <a name="authentication"></a>身份验证

计划移动服务和移动运营商服务之间的通信必须使用相互传输层安全性 (MTLS) 进行身份验证。 Microsoft 提供了证书，用于验证到请求者的标识**moBaseUrl**。

Microsoft 在载入流程期间提供的证书。

### <a name="how-to-enable-get-balance-in-windows-cosa"></a>如何启用 Windows COSA 中获取余额

它需要在要启用 Windows 设备上的获取余额支持的 Windows COSA 数据库中配置以下设置。

以下 COSA 设置是必需的：

- SupportDataMarketplace （必须设置为"是"）
- DataMarketplaceRoamingUIEnabled
- SIM ICCID 范围 （ICCID 范围 – 开始和 ICCID 范围-结束）

有关受支持的所有字段的详细信息，请参阅桌面 COSA 仅设置上[桌面 COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

若要下载 COSA/APN 更新电子表格，请单击[此处](https://go.microsoft.com/fwlink/p/?linkid=851213)。

## <a name="walled-garden"></a>围墙的花园

*围墙花园*是利用数据在运行时支持你的客户的关键。 它使他们能够访问 MO 直接门户，即使没有如 Wi-fi 替代的 internet 连接。 这将使使用者可以购买额外的数据计划和管理其订阅。

> [!NOTE]
> 移动计划体系结构不支持为 Walled Garden 终结点的 IP 范围。 主机名必须用于列入白名单。

MO 直接 web 门户和`GetBalance`API 终结点必须也是此 Walled Garden 的一部分。

### <a name="walled-garden-endpoints"></a>围墙的花园终结点

有只有少量的需始终是向最终用户可访问的终结点。 下表定义 Walled Garden 所需的终结点。

| URL | HTTP/HTTPS |
| --- | --- |
| service.datamart.windows<span></span>.com | https |
| dogfood.datamart.windows<span></span>.com | https |
| windows.policies.live<span></span>.net | https |
| ctldl.windowsupdate<span></span>.com | http |
| cdp1.public-trust<span></span>.com | http |
| ocsp.omniroot<span></span>.com | http |
| vassg142.ocsp.omniroot<span></span>.com | http |
| vassg142.crl.omniroot<span></span>.com | http |
| mscrl.microsoft<span></span>.com | http |
| crl.microsoft<span></span>.com | http |
| msftconnecttest<span></span>.com | http |
| crl3.digicert<span></span>.com | http |
| Ocsp.digicert<span></span>.com | http |
| login.live<span></span>.com | http + https |
| storagetos.datamart.windows<span></span>.com | http + https |
| mps.datamart.windows<span></span>.com | http + https |
| mps-service.datamart.windows<span></span>.com | http + https |
| staging.datamart.windows<span></span>.com | http + https |
| mps-staging.datamart.windows<span></span>.com | http + https |