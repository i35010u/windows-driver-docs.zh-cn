---
title: 移动计划预付的体验
description: 本主题描述了移动计划程序的可选预付的体验。
ms.assetid: 908AB4DE-A4C8-4758-9632-F7F7381FF737
keywords:
- Windows Mobile 计划预付体验、 移动计划预付体验的移动运营商
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 6f2e01b588a14eac4d9d17a59eff8811a91261d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542001"
---
# <a name="mobile-plans-prepaid-experience"></a>移动计划预付的体验

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

启用增强的预付体验的支持是可选的移动运营人员加入具有移动计划。 本主题介绍的其他主题介绍在此部分中，将重点放在需要更好的预付方案的差异的主要流失体验对增量更改。 

## <a name="overview"></a>概述

通过实现预付的体验，可以向使用者提供以下优势：

- 使用者可以看到的数据量不可用，并直到其订阅过期，网络浮出控件中的剩余时间量。
- 使用者可以排名靠前注册其预付订阅通过移动连接，即使它们用完预付余额或其订阅已过期。
- 你可以管理网络飞出式产品/服务基于使用者的订阅状态。

若要实现预付，执行以下步骤：

1. 更新 Windows COSA 数据库。
2. 实现 API 的 Get 平衡。
3. 实现围墙的花园。
4. 验证获取余额 API 和围墙的花园。
5. 符合 API 负载要求。

## <a name="update-windows-cosa-database"></a>更新 Windows COSA 数据库

若要确保体验正确显示在 Windows 连接管理器中，也称为网络浮出控件，移动计划首先需要更新 Windows COSA 数据库。

> [!TIP]
> 在 Windows 设备上更新 COSA 采用相当长的时间并可能会变得项目约束，因此您应提交此请求尽可能早。

<img src="images/dynamo_prepaid_network_flyout_1_general.png" alt="Windows Connection Manager general example" title="Windows 连接管理器常规示例" width="250" />

更新 COSA 后，点击或单击您网络浮出控件中的连接会将其展开 （显示为"Contoso 移动电话"在下图中） 的更多选项。 当在用户展开移动电话网络连接时，将显示"连接与某一数据计划"选项。 点击或单击此选项将启动计划移动应用。

<img src="images/dynamo_prepaid_network_flyout_2_connect.png" alt="Windows Connection Manager showing Connect with Data Plan option" title="Windows 连接管理器显示连接其中数据计划选项" width="250" />

下图显示了举例说明如何，用户可以看到的数据，还剩预付订阅的时间量。

<img src="images/dynamo_prepaid_network_flyout_3_balance.png" alt="Windows Connection Manager showing remaining time and data" title="Windows 连接管理器显示剩余的时间和数据" width="250" />

### <a name="how-to-request-a-cosa-database-update"></a>如何请求 COSA 数据库更新

COSA 数据库提交过程的信息，请参阅[规划你的桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。 

### <a name="cosa-database-settings-details"></a>COSA 数据库设置详细信息

本部分介绍 COSA 中的哪些设置所需的移动计划载入和建议。

有关受支持的所有字段的详细信息，请参阅桌面 COSA 仅设置上[桌面 COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

若要下载 COSA/APN 更新电子表格，请单击[此处](https://go.microsoft.com/fwlink/p/?linkid=851213)。

以下 COSA 设置是必需的：

- SupportDataMarketplace （必须设置为"是"）
- DataMarketplaceRoamingUIEnabled
- SIM ICCID 范围 （ICCID 范围 – 开始和 ICCID 范围-结束）

以下设置可能适用具体情况取决于特定的业务需求：

- AccountExperienceURL
- BrandingName
- BrandingIcon （图标应提供以及电子表格）
- UseBrandingNameOnRoaming

下图显示示例 MO 带有网络浮出控件中的品牌：

<img src="images/dynamo_prepaid_network_flyout_4_branding.png" alt="Windows Connection Manager showing MO branding" title="Windows 连接管理器显示 MO 品牌" width="250" />

## <a name="get-balance-api"></a>获取余额 API

获取余额 API 查询当前订阅状态，控件移动计划体验是否可用在设备上，以及是否预付订阅的网络浮出控件中显示剩余的数据和时间。 下图显示了获取余额 API 的高级流。 

<img src="images/dynamo_prepaid_get_balance_api_flow.png" alt="Get Balance API flow" title="获取余额 API 流" width="600" />

### <a name="resource-model"></a>资源模型

计划移动服务和月服务之间的通信涉及到操作在下图中的资源。 以下关系图的表中的每个资源的说明。

<img src="images/dynamo_prepaid_get_balance_api_resource_model.png" alt="Get Balance API resource model diagram" title="获取余额 API 资源模型关系图" width="600" />

#### <a name="sim-resource"></a>SIM 资源

> [!NOTE]
> SIM 资源当前不支持"创建，""读取"、"更新"或"删除"操作。

| JSON 属性 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
| activationCode | 字符串 | 在客户端上的 LPA 可用于下载和激活配置文件激活代码。 |
| Iccid | 字符串 | 已创建的配置文件的 ICCID。 |
| eId | 字符串 | Esim 卡的事件 Id。 |

#### <a name="balance-resource"></a>平衡资源

| JSON 属性 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
| 在任务栏的搜索框中键入 | 枚举 | 可能值： <ul><li>MODIRECT:指示如果用户余额 MO 直接。</li><li>MODIRECTPAYG:指示如果用户余额 MO 直接 PAYG。</li><li>NONE:指示用户已不平衡。 当剩余余额为 0，但该计划未过期时，我们希望收到"NONE"，以便用户可以购买数据计划。</li><li>NOTSUPPORTED:指示 sim 卡不支持的移动计划体验。 Sim 卡不应在移动计划支持范围内时，使用"NOTSUPPORTED"。 我们将关闭网络浮出控件中的计划移动体验，并收到此类型的计划移动应用中返回的一般性错误消息。</li></ul> |
| dataRemainingInMB | Double | 将计划保留在当前用户的数据，以 mb 为单位。 |
| timeRemaining | 字符串 | 中指定的持续时间[ISO 8601](https://go.microsoft.com/fwlink/p/?linkid=866182)。 |
| 位置 | 字符串的集合 | 在两个字母 ISO 代码中的位置的数组。 这是来自 MCC 还是反向 IP 查找时没有移动电话网络连接。 |

### <a name="headers"></a>标头

以下标头可能包含在与移动计划服务 Mobile 提供程序的终结点对每个请求。

| 标头名称 | 值 | 描述 |
| --- | --- | --- |
| X-MS-DM-TransactionId | 字符串 | 若要唯一标识此请求/响应交互之间移动计划服务和月服务 TransactionId。 |
| 授权 （可选） | 字符串 | 密苏里州 （可选） 提供一个基本身份验证字符串 |

### <a name="error-codes"></a>错误代码

| 错误代码 | 描述 |
| --- | --- |
| HTTP 200 （正常） | 已成功完成该操作。 此代码还应该用于指示用户是否应执行的指定位置中有 0 平衡使用 dataRemainingInMB = 0 和 timeRemaining ="PT0S"使用 HTTP 200。 |
  HTTP 201 （已创建） | 指示已成功完成该操作和资源已成功创建。 |
| HTTP 400 （错误请求） | 一个无效的使用无效的查询参数、 标头无效或有效负载无效。 在响应正文中，应指示不正确的参数。 例如，如果指定了无效的 fieldsTemplate，必须返回此错误代码的响应正文中的详细信息。 |
| HTTP 401 （未经授权） | 身份验证凭据不正确或无效。 这可能时传递的基本身份验证凭据不正确。 |
| HTTP 403 （禁止访问） | 客户端证书是不受信任或无效。 如果 MTLS 一部分包含的客户端证书无效，应返回 HTTP 403。 |
| HTTP 404 （找不到） | 该资源不存在时，MO 服务应返回此错误。 这可能不正确的 ICCID 发送时。 这不应该用于指示用户不指示使用 HTTP 200 （正常） 的指定位置中具有一种平衡。 |
| HTTP 409 （冲突） | 如果 TransactionId 重复，使用。 |
| HTTP 429 (太多的请求) | 月服务使用它来指示计划移动服务中指定的时间内发送过多的请求。 在响应中，MO 服务必须使用重试间隔标头以指示资源的时间之后计划移动服务应重试。 在响应正文中，可以提供可选的详细信息。 |
| HTTP 500 （内部错误） | 出现意外情况的月服务上。 月服务应该包含错误，只要有可能的原因，使它可用于根据需要进一步调试。 |

### <a name="get-balance-api-specification"></a>获取余额 API 规范

移动计划必须了解原因有多种，其中最重要的是移动计划确定应允许用户根据其当前余额的新计划购买的订阅的状态。 用户还必须能够在任何时候都可以在进行检查其当前余额。

获取余额 API 调用或计划移动应用程序启动时显示网络浮出控件。

以下一系列示例显示获取余额 API 的调用流。

#### <a name="example-1-checking-balance-any-time-within-the-experience"></a>示例 1：检查余额体验内的任意时间

HTTP 请求，其中*moBaseUrl*是月托管服务的终结点并*sim id*是 ICCID:

```html
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US HTTP/1.1
```

查询参数：

| 查询参数名称 | 值 | 描述 |
| --- | --- | --- |
| 位置 | 字符串 | 可选。 用户余额正在查询的位置。 如果未指定，应所有活动的余额。 |
| 限制 | 整型 |可选。 要返回的余额的最大计数。 如果未指定，则应返回所有余额。 |
| fieldsTemplate | 枚举 |指定必须在资源中返回的字段的列表。 <p>可能值：</p><ul><li>Basic:*类型*， *dataRemainingInMB*，并*timeRemaining*中平衡资源必须返回。</li><li>完整:必须返回平衡资源中的所有属性。</li></ul> |

#### <a name="example-2-returning-the-first-balance-that-is-available-for-the-user-in-us"></a>示例 2：返回可用于美国用户的第一个余额

```html
GET https://moendpoint.com/v1/sims/iccid: 8988247000100003319/balances?fieldsTemplate=basic&limit=1&location=us HTTP/1.1
X-MS-DM-TransactionId: “MSFT-12345678-1234-1234-1234-123456789abc”
```

HTTP 响应：

```html
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

#### <a name="example-3-the-expected-response-when-fieldstemplate-is-set-as-full"></a>示例 3：预期的响应 fieldsTemplate 设置为已满时

```html
GET https://moendpoint.com/v1/sims/iccid: 8988247000100003319/balances?fieldsTemplate=full HTTP/1.1
X-MS-DM-TransactionId: “MSFT-12345678-1234-1234-1234-123456789abc”

HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: “MSFT-12345678-1234-1234-1234-123456789abc”

{
“balances”: [
    {
         “id”: “23445”,
         “type”: “MODIRECTPAYG”,
         “dataRemaininginMB”: 123.0,
         “timeRemaining”: “P23DT23H”,
         “locations”: [“US”, “CA”],
         “ms-provisioningDataSet”: [“xxxxx”, “yyyyy”]
    },
    {
         “id”: “12345”,
         “type”: “MODIRECTPAYG”,
         “dataRemaininginMB”: 1367.0,
         “timeRemaining”: “P23DT23H”,
         “locations”: [“UK”, “FR”],
         “ms-provisioningDataSet”: [“xxxxx”, “yyyyy”]
    }
  ]
}
```

#### <a name="example-4-the-expected-response-for-a-sim-that-is-in-the-cosa-iccid-range-but-should-not-be-supported-by-mobile-plans"></a>示例 4:SIM COSA ICCID 范围内，但不应受移动计划预期的响应

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

### <a name="authentication"></a>Authentication

Microsoft 服务和你的服务之间的通信必须使用相互传输层安全性 (MTLS) 进行身份验证。 Microsoft 将提供将用于验证到请求者的标识的证书**moBaseUrl**。

## <a name="walled-garden"></a>围墙的花园

围墙的花园是关键数据不足时，支持你预付的客户。 它使他们能够访问 MO 直接门户，即使没有如 Wi-fi 替代的 internet 连接。 这将使使用者可以购买额外的数据计划和管理其订阅。

MO 直接 web 门户和获取余额 API 终结点必须还属于此 Walled Garden。

有只有少量的需始终是向最终用户可访问的终结点。 下表定义 Walled Garden 所需的终结点。 

| URL | HTTP/HTTPS |
| --- | --- |
| service.datamart.windows<span></span>.com | https |
| dogfood.datamart.windows<span></span>.com | https |
| windows.policies.live<span></span>.net | https |
| ctldl.windowsupdate<span></span>.com | http |
| msftncsi<span></span>.com | http |
| login.live<span></span>.com | http + https |
| storagetos.datamart.windows<span></span>.com | http + https |
| cdp1.public-trust<span></span>.com | http |
| ocsp.omniroot<span></span>.com | http |
| vassg142.ocsp.omniroot<span></span>.com | http |
| vassg142.crl.omniroot<span></span>.com | http |
| mscrl.microsoft<span></span>.com | http |
| crl.microsoft<span></span>.com | http |
| msftconnecttest<span></span>.com | http |
| crl3.digicert<span></span>.com | http |
| Ocsp.digicert<span></span>.com | http |

## <a name="prepaid-implementation-validation"></a>预付的实现验证

本部分介绍测试和验证以确保已准备好将移到集成阶段必须执行的操作。

### <a name="prerequisites"></a>必备条件

1. 安装 Windows 10 中，将用于测试在 PC 上的版本 1607年。
2. 在正式版推出之前获取最新的 Windows 版本通过联接[Windows 预览体验计划](https://go.microsoft.com/fwlink/p/?linkid=866189)。

### <a name="test-cases-to-be-executed"></a>若要执行的测试用例

#### <a name="walled-garden"></a>围墙的花园

1. 当用户没有余额，请确保用户可以访问 Walled Garden 站点中定义[Walled Garden](#walled-garden)。

#### <a name="getting-balance"></a>获取余额

1. Walled Garden 状态用户时，返回的余额必须为零。
2. 当用户已分配 Microbalance 时，返回的余额必须为零。
3. 用户使用的数据，因为必须递减返回的平衡，以反映剩余的数据。
4. 分配的时间内调用后的创建顺序 API 的超时期结束，剩余的时间必须递减以反映剩余的时间。

#### <a name="test-with-expired-mtls-certificate"></a>测试 MTLS 证书已过期

1. 如果没有 MTLS 证书验证 MO Api。
预期的状态：401 未经授权。
2. 验证 MTLS 证书已过期。
预期的状态：401 未经授权。

#### <a name="get-balance-negative-tests"></a>获取余额反向测试

1. 验证使用无效 SIM。
预期的状态：404 找不到。
2. 验证未知的位置或错误的位置字符串/数字开头。
预期的状态：400 （错误请求）。
3. 验证筛选器限制为负数和超出 INT 的限制
预期的状态：400-错误的请求。
筛选器限制 （整数） 的预期状态 200 OK。
4. 验证以获取而无需任何余额*位置*（或空位置）， *fieldTemplate*，*限制*，和许多的多个参数组合。
预期的状态：400 （错误请求） 与任何错误的参数值。
预期状态 200-OK。

## <a name="get-balance-api-load-test"></a>获取余额 API 负载测试

在生产环境中启用获取余额 API 之前，应测试 Microsoft 服务和移动运营商服务，以查看它们是否可以处理预计的负载。 移动运营商需要运行负载测试。  一旦已过，移动计划将执行 6 小时的负载测试按照下一节中的配置。 

此测试配置是从 10,000 Sim 的预计流量生成。 根据 3 次此流量投影计算峰值 RP。

- 将从 25 测试代理执行负载测试。
- 有关将执行负载测试：
    - 使用 100 个不同用户 (#ICCIDs) 与 1 RPS 的 1 小时。
    - 对于 500 个不同用户 (#ICCIDs) 与 1 RPS 的 4 个小时。
    - 1000 个不同用户 (#ICCIDs) 使用 3 个 RP （峰值） 的 1 小时。
- 负载分布跨 Api 可能会按如下所示：

| API | 负载分布 | 预期的 RPS | 峰值 RPS |
| --- | --- | --- | --- |
| GetBalance | 96% | 1 | 3 |

在测试运行期间预期的成功率是：99.9%. 在获得此成功率，MO API 将移动计划生产服务中启用。