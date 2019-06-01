---
title: 移动计划旧回调通知
description: 本主题介绍了计划移动应用支持通知回调
ms.assetid: 5077A3EA 379C 4EB5 A05B BA1585E9594D
keywords:
- Windows Mobile 计划旧版回调通知，移动计划旧实现移动运营商
ms.date: 05/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6559d5e8437163f25bfc7cd5ca10fcc70d8d4209
ms.sourcegitcommit: 335096107bfc92718d9ba809527214113c993da7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455866"
---
# <a name="mobile-plans-legacy-callback-notifications"></a>移动计划旧回调通知

> [!NOTE]
> 此页介绍移动计划旧回调通知。 请将此用作参考仅，未实现今后此代码。

## <a name="inline-profile-delivery"></a>内联配置文件交付

下图显示了移动计划程序如何支持而无需控制离开 MODirect 门户下载配置文件的高级别流。

![移动计划内联配置文件下载序列图](images/dynamo_inline_profile_flow.PNG)

在门户的配置文件下载、 安装和激活发生准备就绪 MO 直接门户时，应调用`MobilePlansInlineProfile.notifyInlineProfileDownload`。

### <a name="mobileplansinlineprofilenotifyinlineprofiledownload"></a>MobilePlansInlineProfile.notifyInlineProfileDownload

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
| activationCode | 字符串 | 正在下载 esim 卡配置文件激活代码。 配置文件的 ICCID 推断从配置文件元数据。 |

以下 Javascript 函数显示要通知的内联配置文件下载的应用程序的 API 的示例应开始。

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

请参阅[购买元数据属性](mobile-plans-callback-notifications.md#purchase-metadata-properties-details)有关详细信息`puchaseMetadata`对象。

## <a name="adding-balance-legacy"></a>添加余额 （旧版）

当用户完成购买 MO 直接门户中的通过将更多的数据添加到他们的帐户 （由于用户 esim 卡上使用当前配置文件需要进行任何配置文件下载） 时，应调用 MO 门户`MobilePlans.notifyBalanceAddition`API 将控制权返回给移动计划应用程序。

### <a name="mobileplansnotifybalanceaddition"></a>MobilePlans.notifyBalanceAddition

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
| iccid | 字符串 | 向其分配数据 ICCID。 如果此 ICCID 未处于活动状态，计划移动应用激活相应的配置文件。|

下面的 Javascript 函数显示示例的 API 来通知用户已完成使用配置文件的购买的应用程序已可用，但不是一定是活动，esim 卡上。

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

请参阅[购买元数据属性](mobile-plans-callback-notifications.md#purchase-metadata-properties-details)有关详细信息`puchaseMetadata`对象。

## <a name="other-legacy-callback-notifications"></a>其他旧回调通知

应使用以下语法使用 JavaScript 发送到计划移动应用的通知：

```javascript
DataMart.notifyPurchaseResult(notificationPayload);
```

Esim 卡通知有效负载的示例如下所示：

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

物理 SIM 通知有效负载的示例如下所示：

```javascript
let notificationPayload = new Object();
notificationPayload.ver = '1';
notificationPayload.purchaseResult = "{\"userAccount\":\"New\",\"purchaseInstrument\":\"New\",\"line\":\"New\",\"moDirectStatus\":\"Complete\",\"planName\":\"MyPlan\"}";
notificationPayload.success = true;
notificationPayload.transactionId = 'MSFT_ecf5a4d6-024c-46c3-8fcd-2c1f0deed572';
notificationPayload.iccid = '8988247000101997790';

DataMart.notifyPurchaseResult(JSON.stringify(notificationPayload));
```

Esim 卡，其中用户放弃不成功的事务的情况下个月门户通知有效负载的示例如下所示。 若要实现适用于特定实现的所有情况下，请参阅后面的示例表。

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

从其发送通知的月门户 URI 必须是中的安全*https*协议。 您可以指定该主机，但不是一定是未来保留一定的灵活性的完整路径。

下表介绍通知的 JSON 有效负载中的每个字段：

| JSON 字段         | 在任务栏的搜索框中键入    | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | 示例                                |
| ------------------ | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| success            | 布尔 | **True**如果用户购买 MO 直接计划。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `“success”:true`                     |
| iccid              | 字符串  | 对于 esim 卡，这指示 ICCID 客户端必须用于使用月直接购买的计划。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `iccid:”8988247000100297655”`        |
| activationCode     | 字符串  | 要检索的 esim 卡配置文件的激活代码。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `“ActivationCode”`                   |
| transactionId      | 字符串  | MO 门户收到作为查询参数时在门户启动的事务 ID。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `transctionId= rRi8OzhI3EiR02nm.2.0.1` |
| purchaseResult     | 字符串  | 包含与 MO 门户的用户交互的详细信息。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                        |
| userAccount        | 枚举    | 此字段为必需字段。 <p>可能值：</p><ul><li>新建：指示用户已创建了新的用户帐户。</li><li>现有:指示用户记录的现有用户帐户。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul>                                                                                                                                                                                                                                                                                                                 | `“userAccount”:”New”`              |
| purchaseInstrument | 枚举    | 此字段为必需字段。 <p>可能值：</p><ul><li>新建：指示用户使用新的一种付款方式。</li><li>现有:指示用户使用已在文件的现有付款方法。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul>                                                                                                                                                                                                                                                                                                             | `“purchaseInstrument”:”New”`       |
| 行               | 枚举    | 此字段为必需字段。 <p>可能值：</p><ul><li>新建：指示 SIM 卡已添加的用户帐户。</li><li>现有:指示是否传输的现有行到设备。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul>                                                                                                                                                                                                                                                                                                                     | `“line”:”New”`                     |
| moDirectStatus     | 枚举    | 此字段为必需字段。 <p>可能值：</p><ul><li>完成：指示用户已成功完成购买。</li><li>服务错误：表示用户无法完成购买由于月服务错误。</li><li>InvalidSIM:表示传递给在门户 ICCID 时不正确。</li><li>LogOnFailed:表示用户无法登录到 MO 门户。</li><li>PurchaseFailed:指示在购买由于计费错误而失败。</li><li>ClientError:指示无效的参数已传递到门户。</li><li>None:指示用户已结束而无需特定错误的事务。</li></ul> | `“moDirectStatus”:”Complete”`      |
| planName           | 字符串  | 对于成功的事务，此字段不能为空，并且必须提供一个描述性的计划名称。 对于失败的事务，此字段必须是空字符串。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `“planName”:”prepaid_3GperMonth”`  |
