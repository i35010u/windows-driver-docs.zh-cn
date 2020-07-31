---
title: 移动计划帐户管理
description: 本主题介绍了移动计划的 Windows 帐户管理体验。
ms.assetid: E97AD441-86F7-439C-9800-7DD93AAC0545
keywords:
- Windows Mobile 计划帐户管理，移动计划移动运营商
ms.date: 03/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: f58c0c0f50e4b99855603e112ea5e3e113dc04c6
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402294"
---
# <a name="mobile-operator-account-management-in-windows-10"></a>Windows 10 中的移动运营商帐户管理

本主题介绍 Windows 提供的移动运营商帐户管理体验，可以使用移动计划进行扩展。

## <a name="basic-account-management-experience"></a>基本帐户管理体验

本部分介绍用于配置在 Windows 连接管理器中显示的 "*我的帐户*" 链接（也称为网络飞出）的选项。

"*查看我的帐户*" 链接可以配置为：

- 启动 web 浏览器并打开已定义的网页。
- 启动移动计划应用，并打开移动运营商 web 门户。

 确定了其中一个选项后，请请求 COSA 数据库更新以实现正确的行为。 有关详细信息，请参阅[计划桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。

以下设置适用于上述选项：

- *AccountExperienceURL*。 此参数定义 web 页。
- *AppID*。 此参数定义要启动的应用程序。 若要使用移动计划应用，请配置_OneConnect_8wekyb3d8bbwe！应用_。

下图显示了网络弹出窗口的示例：

<img src="images/mobile_plans_network_flyout_basic.png" alt="Windows Connection Manager showing basic MO" title="显示基本 MO 的 Windows 连接管理器" width="250" />

## <a name="enhanced-account-management-experience"></a>增强的帐户管理体验

通过实现增强的帐户管理体验，你可以为客户提供以下好处：

- 客户可在网络飞出中查看有多少数据可用以及剩余的时间量。
- 客户可以通过移动连接来向上提升其预付款订阅，即使它们的预付余额不足或订阅已过期。
- 你可以根据客户的订阅状态管理网络飞出产品。

这些体验在[基本帐户管理体验](#basic-account-management-experience)的基础上构建，这是设备网络弹出窗口中的默认体验。

### <a name="network-flyout-user-experience"></a>网络飞出用户体验

根据从 API 调用接收的信息 `GetBalance` ，网络飞出的行为会有所不同，从而增强了用户体验。

网络浮出控件包含以下元素：

1. 连接数据计划。 这会启动移动计划应用。
2. 查看我的帐户。 的行为取决于[基本帐户管理体验](#basic-account-management-experience)。
3. 余额信息。 显示您的响应中提供的余额 `GetBalance` 。

下图显示了这些网络飞出元素。 与数据计划连接与 A 相对应，"查看我的帐户" 与 B 对应，余额信息与 C 对应。

<img src="images/dynamo_prepaid_network_flyout_5_getbalance.png" alt="Windows Connection Manager showing behavior depending on GetBalance API calls" title="根据 GetBalance API 调用显示行为的 Windows 连接管理器" width="600" />

若要在网络弹出窗口中提供正确的信息，MOs 提供了[GETBALANCE API](#getbalance-api)部分中定义的*类型*和*平衡*（dataRemainingMB 和 timeRemaining）信息。

下表提供了 `GetBalance` 响应类型和网络飞出中显示的内容的引用。

| GetBalance 响应类型 | 网络浮出控件显示 .。。 |
| --- | --- |
| MODIRECT | "仅查看我的帐户"，无余额信息 |
| MODIRECTPAYG | "查看我的帐户" 和余额信息 |
| 无 | "使用数据计划进行连接" |
| NOTSUPPORTED | 仅 "查看我的帐户" |

## <a name="getbalance-api"></a>GetBalance API

> [!IMPORTANT]
> 请请求[WINDOWS COSA 更新以在 Windows 中启用获取平衡](#how-to-enable-get-balance-in-windows-cosa)。

`GetBalance`API 查询当前订阅状态，控制设备上的移动计划体验是否可用，并在网络飞出中显示预付订阅的剩余数据和时间。 下图显示了该 API 的高级别流 `GetBalance` 。

<img src="images/mobile_plans_get_balance_api_flow.png" alt="GetBalance API flow" title="GetBalance API 流" width="600" />

### <a name="resource-model"></a>资源模型

移动计划服务与移动运营商 API 之间的通信涉及操作下图中的资源。 每个资源的说明位于关系图后面的表中。

<img src="images/mobile_plans_get_balance_resource.png" alt="GetBalance API resource model diagram" title="GetBalance API 资源模型关系图" width="600" />

#### <a name="sim-resource"></a>SIM 资源

> [!NOTE]
> SIM 资源当前不支持 "创建"、"读取"、"更新" 或 "删除" 操作。

| JSON 属性 | 类型 | 描述 |
| --- | --- | --- |
| Iccid | 字符串 | 已创建的配置文件的 ICCID。 |

#### <a name="balance-resource"></a>平衡资源

| JSON 属性 | 类型 | 描述 |
| --- | --- | --- |
|id |字符串| 移动运营商内部 id，用于跟踪事务 |
类型 | 枚举 | 可能的值： <ul><li>MODIRECT：指示用户余额是否为 MO Direct。</li><li>MODIRECTPAYG：指示用户余额是否为 MO Direct PAYG。</li><li>无：指示用户没有余额。 如果余额为0但计划未过期，我们希望收到 "NONE"，以便用户可以购买数据计划。</li><li>NOTSUPPORTED：指示移动计划体验不支持 SIM。 如果 SIM 不应处于 * 移动计划支持的范围内，则使用 "NOTSUPPORTED"。 我们会关闭网络飞出中的移动计划体验，并在收到此类型时在移动计划应用中返回一般性错误消息。</li></ul> |
| dataRemainingInMB | 双精度 | 当前用户计划中剩余的数据（以 MB 为单位）。 |
| timeRemaining | 字符串 | [ISO 8601](https://go.microsoft.com/fwlink/p/?linkid=866182)中指定的持续时间。 |

### <a name="headers"></a>头文件

将移动计划服务的每个请求中的以下标头包含到移动提供商的终结点。

| 标头名称 | 值 | 说明 |
| --- | --- | --- |
| X-MS-TransactionId | 字符串 | 用于唯一标识移动计划服务与 MO 服务之间的请求/响应交互的 TransactionId。 |
| 授权（可选） | 字符串 | MO 提供的基本身份验证字符串（可选）。 |

### <a name="error-codes"></a>错误代码

下表定义了应在 HTTP 响应中使用的错误代码。

| 错误代码 | 说明 |
| --- | --- |
| HTTP 200 （正常） | 操作已成功完成。 此代码还应该用于指示用户是否在指定位置有0余额，应使用 dataRemainingInMB = 0 并将 timeRemaining = "PT0S" 与 HTTP 200 一起完成。 |
  HTTP 201 （已创建） | 指示操作已成功完成且资源已成功创建。 |
| HTTP 400 （错误的请求） | 用于无效的查询参数、无效的标头或无效有效负载。 在响应正文中，应指示不正确的参数。 例如，如果指定了无效的 fieldsTemplate，则必须返回此错误代码，并在响应正文中返回详细信息。 |
| HTTP 401（未授权） | 身份验证凭据不正确或无效。 如果传递的基本身份验证凭据不正确，则会发生这种情况。 |
| HTTP 403 （禁止访问） | 客户端证书不受信任或无效。 如果作为 MTLS 一部分包含的客户端证书无效，则应返回 HTTP 403。 |
| HTTP 404 （找不到） | 当资源不存在时，MO 服务应返回此错误。 发送不正确的 ICCID 时，可能会出现这种情况。 不应使用此设置来指示用户在指定位置没有余额，这是使用 HTTP 200 （OK）指示的。 |
| HTTP 409 （冲突） | 如果重复 TransactionId，则使用。 |
| HTTP 429 （请求过多） | 由 MO 服务用来指示移动计划服务在指定的时间内发送过多的请求。 在响应中，MO 服务必须使用后重试标头来指示移动计划服务应重试该资源的时间。 在响应正文中，可以提供可选的详细信息。 |
| HTTP 500 （内部错误） | MO 服务出现意外情况。 MO 服务应尽可能包含错误原因，以便可以根据需要将其用于进一步调试。 |

### <a name="getbalance-api-specification"></a>GetBalance API 规范

`GetBalance`当 Windows 设备中显示 "网络" 弹出窗口时，将调用 API。 移动计划服务是此通信的代理。

此调用是使用 HTTP 请求完成的，其中*moBaseUrl*是 MO 托管服务的终结点， *SIM id*是 ICCID：

```HTTP
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US HTTP/1.1
```

查询参数：

| 查询参数名称 | 值 | 说明 |
| --- | --- | --- |
| location | 字符串 | 可选。 正在查询用户平衡的位置。 如果未指定，则应为所有活动余额。 **注意**Location 参数区分大小写。 |
| limit | Integer |可选。 要返回的余额的最大计数。 如果未指定，则应返回所有余额。 |
| fieldsTemplate | 枚举 |指定必须在资源中返回的字段列表。 <p>可能的值：</p><ul><li>基本：必须返回余额资源中的*类型*、 *dataRemainingInMB*和*timeRemaining* 。</li><li>Full：必须返回余额资源中的所有属性。</li></ul> |

以下一系列示例显示了 API 的调用流 `GetBalance` 。

#### <a name="example-1-returning-the-first-balance-that-is-available-for-the-user-in-us"></a>示例1：返回可用于美国用户的第一次余额

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

响应 JSON：

| 数据 | 类型 | 描述 |
| --- | --- | --- |
| 余额 | 集合 | 余额的集合。 |

#### <a name="example-2-the-expected-response-for-a-sim-that-is-in-the-cosa-iccid-range-but-should-not-be-supported-by-mobile-plans"></a>示例2： COSA ICCID 范围内的、但移动计划不应支持的 SIM 的预期响应

HTTP 请求：

```html
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US
HTTP/1.1
```

响应 JSON：

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

移动计划服务与移动运营商 API 之间的通信必须使用相互传输层安全性（MTLS）进行身份验证。 Microsoft 提供了一个证书，供你用来验证请求者的身份**moBaseUrl**。

Microsoft 在载入过程中提供证书。

### <a name="how-to-enable-get-balance-in-windows-cosa"></a>如何在 Windows COSA 中启用获取平衡

需要在 Windows COSA 数据库中配置以下设置，以便在 Windows 设备上启用获取平衡支持。

以下 COSA 设置是必需的：

- SupportDataMarketplace （必须设置为 "是"）
- DataMarketplaceRoamingUIEnabled
- SIM ICCID 范围（ICCID 范围–开始和 ICCID 范围–结束）

有关所有受支持字段的详细信息，请参阅 Desktop COSA only settings on [DESKTOP COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

下载[COSA/APN 更新电子表格](https://go.microsoft.com/fwlink/p/?linkid=851213)。
