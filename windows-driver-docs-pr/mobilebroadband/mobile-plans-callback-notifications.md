---
title: 移动计划回调通知
description: 本主题介绍了计划移动应用支持通知回调
ms.assetid: A3CE0B7D-80C5-4A98-8615-250A3C760B85
keywords:
- Windows Mobile 计划回调通知，移动计划实现的移动运营商
ms.date: 05/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5d93561092bac4024e8c537b7af5f6e22cfe7f9c
ms.sourcegitcommit: 335096107bfc92718d9ba809527214113c993da7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455228"
---
# <a name="mobile-plans-callback-notifications"></a>移动计划回调通知

## <a name="overview"></a>概述

用户完成 MO 门户流后，MO 门户必须返回到计划移动应用的控件。 这是通过使用与 MO 门户的用户交互的结果为应用程序发出通知。

MO 门户支持的事务包括但不限于以下：

- 销售新 esim 卡配置文件 （发出一个激活代码）。
- 激活订阅。
- 购买新的数据计划 （流失或预付）。
- 正在取消订阅。

> [!NOTE]
> 从主机中定义应返回此回调[服务配置](mobile-plans-service-configuration.md)。

## <a name="immediate-esim-profile-download-and-activation"></a>即时 esim 卡配置文件下载和激活

下图显示了移动计划程序如何支持而无需控制离开 MODirect 门户下载配置文件的高级别流。

![移动计划内联配置文件下载序列图](images/mobile_plans_inline_profile_flow.png)

这是的演变[内联配置文件传递](mobile-plans-legacy-callback-notifications.md#inline-profile-delivery)，其现已记录的旧文档页中。

### <a name="mobileplansinlineoperationsnotifyprofiledownloadpurchasemetadata-activationcode"></a>MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData, activationCode)

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
| activationCode | 字符串 | 激活代码，以用于下载 esim 卡配置文件

| 返回值的类型 | 描述 |
| --- | --- |
| MobilePlansOperationContext | 具有标识符添加到与此唯一下载操作的匹配的对象。

开始下载 esim 卡配置文件的过程。 在调用后立即将控制权返回到 MO 门户中。 要显示顶部的通知的窗体中的月门户上的配置文件下载的进度，将显示用户界面。 MO 门户可以继续在此过程中导航

以下 Javascript 函数显示要通知的应用程序的配置文件下载应该开始的 api 示例

```Javascript
var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.registrationChangedScript = "onRegistrationChanged";
    MobilePlansInlineOperations.profileActivationCompleteScript = "onActivationComplete";
    MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData , "1$smdp.address$matchingID");
```

请参阅[购买元数据属性](#purchase-metadata-properties-details)puchaseMetadata 对象有关的详细信息。

### <a name="listening-for-network-registration-changes"></a>侦听网络注册更改

若要侦听的网络注册更改`MobilePlansInlineProfileDownload.registrationChangedScript`必须设置为所需字符串的 Javascript 函数的名称的字符串为`registrationArgs`。

注册参数是一个字符串，表示一个 JSON 对象。

#### <a name="profileregistrationcompleteargs"></a>ProfileRegistrationCompleteArgs

| 属性名 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| networkRegistrationState | 字符串 | 表示当前网络注册状态的字符串。 此属性的值所示`MobilePlansNetworkRegistrationState`。 |
| iccid | 字符串 | ICCID 网络注册状态已更改。 |

#### <a name="mobileplansnetworkregistrationstate"></a>MobilePlansNetworkRegistrationState

| 属性名 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| 无 | 字符串 | 没有连接。 |
| 取消注册 | 字符串 | 设备未注册，不搜索网络提供程序。 |
| 正在搜索 | 字符串 | 设备未注册，并搜索网络提供程序。 |
| 主页 | 字符串 | 设备已打开的家庭网络提供程序。 |
| 漫游 | 字符串 | 设备处于漫游的网络提供商。 |
| 合作伙伴 | 字符串 | 设备处于漫游的合作伙伴网络提供商。 |
| 被拒绝 | 字符串 | 设备被拒绝注册。 |

以下 Javascript 示例显示了如何实现网络注册更改事件的侦听器。

```Javascript
function onRegistrationChanged(registrationArgs) {
    var registrationObj = JSON.parse(registrationArgs);
    if(registrationObj.networkRegistrationState == MobilePlansNetworkRegistrationState.home ||
       registrationObj.networkRegistrationState == MobilePlansNetworkRegistrationState.roaming ||
       registrationObj.networkRegistrationState == MobilePlansNetworkRegistrationState.partner)
    {
        Log('Registration Successful!');
    }
}
```

### <a name="listening-for-profile-activation"></a>侦听配置文件激活

若要侦听的配置文件激活事件`MobilePlansInlineProfileDownload.profileActivationCompleteScript`必须设置为所需字符串的 Javascript 函数的名称的字符串为`activationArgs`。

`activationArgs`是一个字符串，表示 JSON 对象。

#### <a name="profileactivationcompleteargs"></a>ProfileActivationCompleteArgs

| 属性名 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| activationResult | 字符串 | 激活的结果。 此属性的值所示`MobilePlansActivationError`。 |
| iccid | 字符串 | 已激活的配置文件的 ICCID。 |

#### <a name="mobileplansactivationerror"></a>MobilePlansActivationError

| 属性名 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| success | 字符串 | 指示操作成功。 |
| notAuthorized | 字符串 | 指示该操作未获得授权。 |
| notFound | 字符串 | 指示找不到指定的 esim 卡配置文件。 |
| policyViolation | 字符串 | 指示该操作违反了策略。 |
| insufficientSpaceOnCard | 字符串 | 指示要完成该操作的卡片上没有足够的存储空间。 |
| serverFailure | 字符串 | 指示操作期间发生服务器故障。 |
| serverNotReachable | 字符串 | 指示不会在操作期间访问服务器。 |
| timeoutWaitingForUserConsent | 字符串 | 指示该操作在超时期限内未被授予用户同意。 |
| incorrectConfirmationCode | 字符串 | 指示在操作期间提供错误的确认代码。 |
| confirmationCodeMaxRetriesExceeded | 字符串 | 指示在操作期间提供错误的确认代码并允许没有更多的重试。 |
| cardRemoved | 字符串 | 指示已删除 SIM 卡。 |
| cardBusy | 字符串 | 指示 SIM 卡正忙。 |
| 其他 | 字符串 | 指示更具体状态并不表示的状态。 |
| cardGeneralFailure | 字符串 | 指示卡错误发生了阻止下载、 安装或无法成功完成其他操作。 |
| confirmationCodeMissing | 字符串 | 指示确认代码需要下载 esim 卡配置文件。 |
| invalidMatchingId | 字符串 | 指示激活代码或发现的事件中的匹配 ID 已被拒绝。 |
| noEligibleProfileForThisDevice | 字符串 | 指示找不到与此设备兼容的 esim 卡配置文件。 例如，找到一个配置文件需要 LTE 支持，但该设备仅支持 3g。 |
| operationAborted | 字符串 | 指示该操作已中止。 |
| eidMismatch | 字符串 | 指示移动运营商服务器上的 esim 卡配置文件已分配的个设备具有不同 esim 卡事件 ID。 |
| profileNotAvailableForNewBinding | 字符串 | 指示用户正在尝试下载的已声明或下载的 esim 卡配置文件。 |
| profileNotReleasedByOperator | 字符串 | 指示 esim 卡配置文件可用，但它未尚未标记为移动运营商发布供下载。 可以下载仅发布配置文件，因此，MO 需要将该配置文件标记为已发布。 |
| operationProhibitedByProfileClass | 字符串 | 指示 esim 卡配置文件类不允许的操作。 |
| profileNotPresent | 字符串 | 指示找不到 esim 卡配置文件。 |
| noCorrespondingRequest | 字符串 | 指示无法找到没有对应的请求。 |
| unknownError | 字符串 | 指示 LPA 返回未知错误。 |
| lpaInitializationError | 字符串 | 指示尝试初始化 LPA 时发生错误。 |
| modemNotFound | 字符串 | 指示没有蜂窝调制解调器已在设备上找到。 |
| localSettingsAccessFailed | 字符串 | 指示访问应用程序的本地设置失败。 |
| invalidJson | 字符串 | 指示调用计划移动应用时，MO 门户已提供无效的 JSON。 |
| invalidActivationCode | 字符串 | 指示 MO 门户具有无效的激活代码。 |
| invalidIccid | 字符串 | 指示 MO 门户具有无效的 ICCID。 |

以下 Javascript 示例显示了如何实现配置文件激活事件的侦听器。

```Javascript
function onActivationComplete(activationArgs) {
    var activationObj = JSON.parse(activationArgs);
    if(activationObj.activationResult == MobilePlansActivationError.success)
        Log('Activation Success');
}
```

## <a name="deferred-esim-profile-download-and-activation"></a>延迟 esim 卡配置文件下载和激活

下图显示了如何移动计划程序支持延迟的下载的 esim 卡配置文件而无需离开 MODirect 门户的控件的高级别流。

![移动计划延迟的配置文件下载序列图](images/mobile_plans_delay_profile_flow.png)

### <a name="mobileplansinlineoperationsnotifyprofiledownloadpurchasemetadata-activationcode-downloaddelay"></a>MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData, activationCode, downloadDelay)

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
| activationCode | 字符串 | 激活代码或 SM-DP + 配置文件所在的地址
| downloadDelay | uint | 要尝试下载 esim 卡配置文件之前等待的分钟数

| 返回值的类型 | 描述 |
| --- | --- |
| MobilePlansOperationContext | 具有标识符添加到与此唯一下载操作的匹配的对象。

在调用后立即将控制权返回到 MO 门户中。 将显示用户界面，以通知用户，将安装一个配置文件。 之后`downloadDelay`分钟发生，通知将显示给用户，邀请他们以开始下载配置文件的过程。

以下 Javascript 函数显示 API 以通知应用程序应以延迟的配置文件下载的示例

```Javascript
var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.registrationChangedScript = "onRegistrationChanged";
    MobilePlansInlineOperations.profileActivationCompleteScript = "onActivationComplete";
    MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData , "1$smdp.address$matchingID", 15);
```

请参阅[购买元数据属性](#purchase-metadata-properties-details)puchaseMetadata 对象有关的详细信息。

请参阅[侦听网络注册更改](#listening-for-network-registration-changes)上面一节。

请参阅[侦听的配置文件激活](#listening-for-profile-activation)上面一节。

## <a name="cancel-esim-profile-download"></a>取消 esim 卡配置文件下载

到目前为止，这适用于[延迟 esim 卡配置文件下载](#deferred-eSIM-profile-download-and-activation)方案中，但它无法用于将来的用户的情况。

下图显示了如何移动计划程序而无需离开 MODirect 门户控件支持取消的 esim 卡配置文件下载的高级别流。

![移动计划取消 esim 卡配置文件下载序列图](images/mobile_plans_cancel_profile_download_flow.png)

### <a name="mobileplansinlineoperationsnotifyoperationcancelmobileplansoperationcontext"></a>MobilePlansInlineOperations.notifyOperationCancel(MobilePlansOperationContext)

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| operationContext | Object | 此对象包含唯一标识的上一个操作的信息 |

再向用户显示 toast 通知，告知他们，下载已准备好开始，可以取消此操作。

以下 Javascript 函数显示要取消的异步操作的 API 的示例。

```Javascript
var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.registrationChangedScript = "onRegistrationChanged";
    MobilePlansInlineOperations.profileActivationCompleteScript = "onActivationComplete";
    var op = MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData , "1$smdp.address$matchingID", 15);
    MobilePlansInlineOperations.notifyOperationCancel(op);
```

## <a name="asynchronous-connectivity"></a>异步连接

下图显示了有关如何移动计划程序支持延迟的连接高级别流。

![移动计划延迟的连接序列图](images/dynamo_async_connectivity_flow.png)

用户已成功完成购买，需要从移动运营商 MO 直接门户的配置文件下载后，门户将通知计划移动应用程序，它应触发延迟的连接流使用`MobilePlans.notifyPurchaseWithProfileDownload`API。

### <a name="mobileplansnotifypurchasewithprofiledownload"></a>MobilePlans.notifyPurchaseWithProfileDownload

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
| activationCode | 字符串 | 正在下载 esim 卡配置文件激活代码。 配置文件的 ICCID 推断从配置文件元数据。 |
| networkRegistrationInterval | 无符号的整数 | 移动运营商向用户预配连接到所需的时间。 计划移动应用程序尝试在网络内注册指定的时间间隔，以分钟为单位。 **请注意**这一次舍入为最接近的 15 分钟间隔。 例如，如果此值设置为 5 分钟，则应用程序尝试重新注册到该网络在大约 15 分钟后 （但可能需要花费更长）。 如果设置为"0"，设备将尝试立即注册。 |

以下 Javascript 函数显示 API 来通知用户购买需要连接延迟预配的应用程序的示例。

 ```Javascript
function finishPurchaseWithDownload() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.new;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.complete;
        metadata.line = MobilePlansLineType.new;
        metadata.planName = "2GB Monthly";
        MobilePlans.notifyPurchaseWithProfileDownload(metadata, "1$smdp.address$matchingID", 15);
}
```

请参阅[购买元数据属性](#purchase-metadata-properties-details)puchaseMetadata 对象有关的详细信息。

## <a name="adding-balance"></a>添加余额

当用户通过将更多的数据添加到其帐户完成购买 MO 直接门户中的时，应调用 MO 门户`MobilePlansInlineOperations.notifyBalanceAddition`API 将控制权返回给计划移动应用。 这可用于*物理 SIM*或*esim 卡配置文件*其中已安装在设备中。

下图显示了如何移动计划程序支持添加均衡的高级别流。

![移动计划添加 balancesequence 关系图](images/mobile_plans_add_balance_flow.png)

### <a name="mobileplansinlineoperationsnotifybalanceadditionpurchasemetadata"></a>MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData)

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |

| 返回值的类型 | 描述 |
| --- | --- |
| MobilePlansOperationContext | 具有标识符添加到与此唯一下载操作的匹配的对象。

MO 时月想要向给定帐户添加余额，应调用`MobilePlansInlineOperations.notifyBalanceAddition`API。

以下 Javascript 函数显示 API 来通知已余额添加该应用程序的示例。

```Javascript
function NotifyMobilePlans() {
    var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData);
}
```

请参阅[购买元数据属性](#purchase-metadata-properties-details)有关详细信息`puchaseMetadata`对象。

## <a name="adding-balance-and-activate-esim-profile"></a>添加余额和激活 esim 卡配置文件

当用户通过将更多的数据添加到其帐户完成购买 MO 直接门户中的时，应调用 MO 门户`MobilePlansInlineOperations.notifyBalanceAddition`API 将控制权返回给计划移动应用。 这可用于*esim 卡配置文件*其中已安装在设备中。 ICCID 参数指示应激活的 esim 卡配置文件。

下图显示了如何移动计划程序支持添加与 iccid 信息均衡的高级别流。

![移动计划添加 balancesequence 关系图](images/mobile_plans_add_balance_iccid_flow.png)

### <a name="mobileplansinlineoperationsnotifybalanceadditionpurchasemetadata-iccid"></a>MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData, iccid)

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
| iccid | 字符串 | 这应设为活动状态后的余额添加 ICCID

| 返回值的类型 | 描述 |
| --- | --- |
| MobilePlansOperationContext | 具有标识符添加到与此唯一下载操作的匹配的对象。

如果已知的配置文件的 ICCID，还可以对非活动配置文件进行的余额添加。 使用`MobilePlansInlineOperations.notifyBalanceAddition`与 ICCID 将通知的余额添加计划移动以及使移动计划切换到与提供的 ICCID 相对应的配置文件的活动配置文件。

以下 Javascript 函数显示 API 来通知已余额添加该应用程序的示例。

```Javascript
function NotifyMobilePlans() {
    var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData, "8900000000000000001");
}
```

请参阅[购买元数据属性](#purchase-metadata-properties-details)有关详细信息`puchaseMetadata`对象。

## <a name="canceling-purchase-flow"></a>取消购买流

如果用户取消购买流在 MO 门户中，则必须调用门户`MobilePlans.notifyCancelledPurchase`API 来将控制权返回给计划移动应用。

### <a name="mobileplansnotifycancelledpurchase"></a>MobilePlans.notifyCancelledPurchase

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |

以下 Javascript 函数显示 API 来通知用户已取消购买的应用程序的示例。

 ```Javascript
function finishPurchaseWithCancellation() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.new;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.cancelled;
        metadata.line = MobilePlansLineType.bailed;
        metadata.planName = "";
        MobilePlans.notifyCancelledPurchase(metadata);
    }
```

请参阅[购买元数据属性](#purchase-metadata-properties-details)有关详细信息`puchaseMetadata`对象。

## <a name="purchase-metadata-properties-details"></a>购买元数据属性的详细信息

下表描述采购元数据中使用的详细信息。

| 属性名 | 在任务栏的搜索框中键入 | 描述 | 示例 |
| --- | --- | --- | --- |
| userAccount | 字符串 | 可能值： <ul><li>新建：指示用户已创建了新的用户帐户。</li><li>现有:指示用户记录的现有用户帐户。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul> | "userAccount":"New" |
| purchaseInstrument | 字符串 | 可能值： <ul><li>新建：指示用户已创建了新的用户帐户。</li><li>现有:指示用户记录的现有用户帐户。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul> | "purchaseInstrument":"New" |
| 行 | 字符串 | 可能值： <ul><li>新建：指示 SIM 卡已添加的用户帐户。</li><li>现有:指示用户传输到设备的某一现有行。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul> | "line":New" |
| moDirectStatus | 字符串 | 可能值： <ul><li>完成：指示用户已成功完成购买。</li><li>服务错误：表示用户无法完成购买由于月服务错误。</li><li>InvalidSIM:表示传递给在门户 ICCID 时不正确。</li><li>LogOnFailed： 表示用户无法登录到 MO 门户。</li><li>PurchaseFailed:指示在购买由于计费错误而失败。</li><li>ClientError:指示无效的参数已传递到门户。</li>BillingError:指示已具有用户计费的错误。</li></ul> | "moDirectStatus":"Complete" |
| planName | 字符串 | 对于成功的事务，此字段不能为空，并且必须提供一个描述性的计划名称。 对于失败的事务，此字段必须是空字符串。 | "planName":"每月 2 GB"|

## <a name="legacy-callback-notifications"></a>旧的回调通知

请参阅其中记录所有旧的回调的特定页[此处](mobile-plans-legacy-callback-notifications.md)
