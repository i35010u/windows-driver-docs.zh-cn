---
title: 移动计划旧回调通知
description: 本主题介绍移动计划应用支持的回调通知
keywords:
- Windows Mobile 计划旧的回调通知、移动计划旧实现移动运营商
ms.date: 05/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 154a3bef9d7b8d65d02b8a3bce2ad5fe266b0913
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832947"
---
# <a name="mobile-plans-legacy-callback-notifications"></a>移动计划旧回调通知

> [!NOTE]
> 此页面介绍了移动计划旧的回调通知。 请仅将此作为参考，不要再实现此代码。

## <a name="inline-profile-delivery"></a>内联配置文件传递

下图显示了在不使用 MODirect 门户的情况下移动计划程序如何支持下载配置文件的高级流程。

![移动计划内联配置文件下载序列图](images/dynamo_inline_profile_flow.PNG)

当 MO Direct 门户准备好进行配置文件下载、安装和激活时，门户应调用 `MobilePlansInlineProfile.notifyInlineProfileDownload` 。

### <a name="mobileplansinlineprofilenotifyinlineprofiledownload"></a>MobilePlansInlineProfile.notifyInlineProfileDownload

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| purchaseMetadata | 对象 | 此对象包含有关用户购买的元数据。 这包括有关用户帐户、购买方法或仪器的详细信息、用户是否添加新行的详细信息，以及用户所购买的计划的名称。 所有这些都用于报告。 |
| activationCode | String | 用于下载 eSIM 配置文件的激活代码。 配置文件的 ICCID 是从配置文件元数据推断而来的。 |

以下 Javascript 函数显示了一个 API 示例，用于通知应用程序应启动内联配置文件下载。

```Javascript
function NotifyMobilePlans() {
    var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineProfileDownload.registrationChangedScript = "onRegistrationChanged";
    MobilePlansInlineProfileDownload.profileActivationCompleteScript = "onActivationComplete";
    MobilePlansInlineProfileDownload.notifyInlineProfileDownload(purchaseMetaData , "1$smdp.address$matchingID");
}
```

有关对象的详细信息，请参阅 [购买元数据属性](mobile-plans-callback-notifications.md#purchase-metadata-properties-details) `puchaseMetadata` 。

## <a name="adding-balance-legacy"></a> (旧) 添加余额

当用户通过将更多数据添加到其帐户来完成在 MO 直接门户中的购买 (由于用户使用 eSIM) 上的当前配置文件，因此不需要下载配置文件 `MobilePlans.notifyBalanceAddition`

### <a name="mobileplansnotifybalanceaddition"></a>MobilePlans.notifyBalanceAddition

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| purchaseMetadata | 对象 | 此对象包含有关用户购买的元数据。 这包括有关用户帐户、购买方法或仪器的详细信息、用户是否添加新行的详细信息，以及用户所购买的计划的名称。 所有这些都用于报告。 |
| iccid | String | 向其分配数据的 ICCID。 如果此 ICCID 处于非活动状态，则移动计划应用将激活相应的配置文件。|

以下 Javascript 函数显示了一个 API 示例，用于通知应用程序用户已使用已提供的配置文件（但不一定是活动的）在 eSIM 上完成购买。

 ```Javascript
function finishPurchaseWithBalanceAddition() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.none;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.complete;
        metadata.line = MobilePlansLineType.new;
        metadata.planName = "2GB Monthly";
        MobilePlans.notifyBalanceAddition(metadata, "89000000000000000000");
    }
```

有关对象的详细信息，请参阅 [购买元数据属性](mobile-plans-callback-notifications.md#purchase-metadata-properties-details) `puchaseMetadata` 。

## <a name="other-legacy-callback-notifications"></a>其他旧式回调通知

应使用 JavaScript 通过以下语法发送移动计划应用通知：

```javascript
DataMart.notifyPurchaseResult(notificationPayload);
```

ESIM 卡通知负载的示例如下所示：

```javascript
let notificationPayload = new Object();
notificationPayload.ver = '1';
notificationPayload.purchaseResult = "{\"userAccount\":\"New\",\"purchaseInstrument\":\"New\",\"line\":\"New\",\"moDirectStatus\":\"Complete\",\"planName\":\"MyPlan\"}";
notificationPayload.success = true;
notificationPayload.transactionId = 'MSFT_ecf5a4d6-024c-46c3-8fcd-2c1f0deed572';
notificationPayload.activationCode = '1$trl.prod.ondemandconnectivity.com$JO46UQDI07IKQDGG';
notificationPayload.iccid = '8988247000101997790';

DataMart.notifyPurchaseResult(JSON.stringify(notificationPayload));
```

物理 SIM 的通知有效负载的示例如下所示：

```javascript
let notificationPayload = new Object();
notificationPayload.ver = '1';
notificationPayload.purchaseResult = "{\"userAccount\":\"New\",\"purchaseInstrument\":\"New\",\"line\":\"New\",\"moDirectStatus\":\"Complete\",\"planName\":\"MyPlan\"}";
notificationPayload.success = true;
notificationPayload.transactionId = 'MSFT_ecf5a4d6-024c-46c3-8fcd-2c1f0deed572';
notificationPayload.iccid = '8988247000101997790';

DataMart.notifyPurchaseResult(JSON.stringify(notificationPayload));
```

以下是用户在未成功完成事务的情况下放弃了的 eSIM 的通知负载的示例如下所示。 若要实现适用于你的特定实现的所有情况，请参阅示例下的表。

```javascript
let notificationPayload = new Object();
notificationPayload.ver = '1';
notificationPayload.purchaseResult = "{\"userAccount\":\"Bailed\",\"purchaseInstrument\":\"None\",\"line\":\"None\",\"moDirectStatus\":\"None\",\"planName\":\"\"}";
notificationPayload.success = false;
notificationPayload.transactionId = 'MSFT_ecf5a4d6-024c-46c3-8fcd-2c1f0deed572';
notificationPayload.activationCode = '';
notificationPayload.iccid = '';

DataMart.notifyPurchaseResult(JSON.stringify(notificationPayload));
```

要从其发送通知的 MO 门户 URL 必须是安全 *https* 协议。 您可以指定宿主，但不一定是完整路径，这会使将来的灵活性。

下表描述了通知的 JSON 有效负载中的每个字段：

| JSON 字段         | 类型    | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | 示例                                |
| ------------------ | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| success            | 布尔 | 如果用户购买了 MO 直接计划，**则为 True** 。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `“success”:true`                     |
| iccid              | String  | 对于 eSIM，这表示客户端必须使用购买的 MO 直接计划所需的 ICCID。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `iccid:”8988247000100297655”`        |
| activationCode     | String  | 用于检索 eSIM 配置文件的激活代码。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `“ActivationCode”`                   |
| transactionId      | String  | 启动门户时，MO 门户接收的作为查询参数的事务 ID。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `transctionId= rRi8OzhI3EiR02nm.2.0.1` |
| purchaseResult     | String  | 包含与 MO 门户的用户交互的详细信息。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                        |
| 用户帐户        | 枚举    | 此字段为必需字段。 <p>可能的值：</p><ul><li>新：指示用户创建了一个新的用户帐户。</li><li>现有：表示用户使用现有的用户帐户登录。</li><li>帮：指示用户在此步骤结束了购买流程。</li><li>无：表示用户未到达此步骤。</li></ul>                                                                                                                                                                                                                                                                                                                 | `“userAccount”:”New”`              |
| purchaseInstrument | 枚举    | 此字段为必需字段。 <p>可能的值：</p><ul><li>新：指示用户使用了一种新的付款方式。</li><li>现有：指示用户使用了文件上的现有付款方式。</li><li>帮：指示用户在此步骤结束了购买流程。</li><li>无：表示用户未到达此步骤。</li></ul>                                                                                                                                                                                                                                                                                                             | `“purchaseInstrument”:”New”`       |
| line               | 枚举    | 此字段为必需字段。 <p>可能的值：</p><ul><li>新：指示已由用户帐户添加 SIM 卡。</li><li>现有：指示将现有行传输到设备。</li><li>帮：指示用户在此步骤结束了购买流程。</li><li>无：表示用户未到达此步骤。</li></ul>                                                                                                                                                                                                                                                                                                                     | `“line”:”New”`                     |
| moDirectStatus     | 枚举    | 此字段为必需字段。 <p>可能的值：</p><ul><li>Complete：表示用户已成功完成购买。</li><li>ServiceError：指示由于 MO 服务错误，用户无法完成购买。</li><li>InvalidSIM：指示传递到门户的 ICCID 不正确。</li><li>LogOnFailed：指示用户无法登录到 MO 门户。</li><li>PurchaseFailed：指示采购因计费错误而失败。</li><li>关于 microsoft.relay：指示传递到门户的参数无效。</li><li>无：指示用户在未出现特定错误的情况下结束事务。</li></ul> | `“moDirectStatus”:”Complete”`      |
| planName           | String  | 对于成功的事务，此字段不能为空，并且必须提供描述性计划名称。 如果事务未成功，则此字段必须为空字符串。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `“planName”:”prepaid_3GperMonth”`  |
