---
title: 移动计划回拨通知
description: 本主题介绍移动计划应用支持的回调通知
ms.assetid: A3CE0B7D-80C5-4A98-8615-250A3C760B85
keywords:
- Windows Mobile 计划回拨通知，移动计划实现移动运营商
ms.date: 05/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: f778f8bcdc7ae093d846af6196d9d90969e3c773
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402292"
---
# <a name="mobile-plans-callback-notifications"></a>移动计划回拨通知

## <a name="overview"></a>概述

用户完成移动运营商 web 门户中的激活流后，门户必须提供信号，使移动计划应用知道流已完成。 这是通过向应用程序发出通知来完成的，该应用程序包含用户与 web 门户交互的结果。

Web 门户支持的事务包括但不限于以下各项：

- 发出新 eSIM 配置文件（使用激活代码）。
- 将设备与新的或现有的订阅相关联。
- 购买新的数据计划（损失较大或预付）。
- 为预付计划购买额外的数据。
- 取消订阅。

> [!NOTE]
> 必须从移动运营商的[服务配置](mobile-plans-service-configuration.md)中定义的主机返回回调通知。

## <a name="inline-profile-download-and-connectivity"></a>内联配置文件下载和连接

在后台执行 eSIM 配置文件下载时，应使用回拨方法，同时在移动运营商 web 门户中保留用户。 这使得门户可以在配置文件下载完成后显示其他内容，如帐户管理页面。 此外，如果配置文件允许设备在激活时立即在手机网络上注册，则无需时间延迟。


下图显示了内联配置文件下载回调的调用流：

![移动计划内联配置文件下载序列图](images/mobile_plans_inline_profile_flow.png)

这是旧版[内联配置文件传递](mobile-plans-legacy-callback-notifications.md#inline-profile-delivery)回调的修改版本，可在用于文档的附录中找到。 建议移动运营商使用以上修改后的回叫方法。

### <a name="mobileplansinlineoperationsnotifyprofiledownloadpurchasemetadata-activationcode"></a>MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData, activationCode)

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户购买的元数据。 这包括有关用户帐户、购买方法或仪器的详细信息、用户是否添加新行的详细信息，以及用户所购买的计划的名称。 它们用于业务报告。 |
| activationCode | 字符串 | 用于下载 eSIM 配置文件的激活代码

| 返回值类型 | 描述 |
| --- | --- |
| MobilePlansOperationContext | 一个对象，其中包含与此唯一下载操作匹配的标识符。

在收到回拨通知后，将开始下载 eSIM 配置文件。 控件将在调用后立即返回到 web 门户。 将显示 UI，以显示在 web 门户顶部呈现的作为 popup 元素的配置文件下载进度。 在此过程中，可以继续导航 web 门户。

以下 Javascript 函数显示一个 API 示例，用于通知应用程序配置文件下载应开始：

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

有关 puchaseMetadata 对象的详细信息，请参阅[购买元数据属性](#purchase-metadata-properties-details)。

### <a name="listening-for-network-registration-changes"></a>侦听网络注册更改

若要侦听网络注册更改， `MobilePlansInlineProfileDownload.registrationChangedScript` 必须将设置为采用字符串的 Javascript 函数的名称字符串 `registrationArgs` 。

注册参数是表示 JSON 对象的字符串。

#### <a name="profileregistrationcompleteargs"></a>ProfileRegistrationCompleteArgs

| 属性名称 | 类型 | 描述 |
| --- | --- | -- |
| networkRegistrationState | 字符串 | 一个表示当前网络注册状态的字符串。 此属性的值可在中查看 `MobilePlansNetworkRegistrationState` 。 |
| iccid | 字符串 | 网络注册状态已更改的 ICCID。 |

#### <a name="mobileplansnetworkregistrationstate"></a>MobilePlansNetworkRegistrationState

| 属性名称 | 类型 | 描述 |
| --- | --- | -- |
| 无 | 字符串 | 无连接。 |
| 撤消 | 字符串 | 设备未注册并且未搜索网络提供程序。 |
| 正在搜索 | 字符串 | 设备未注册，正在搜索网络提供程序。 |
| 主页 | 字符串 | 设备在家庭网络提供商上。 |
| 移动 | 字符串 | 设备位于漫游网络提供商上。 |
| 伙伴 (partner) | 字符串 | 设备位于漫游伙伴网络提供商上。 |
| 拒绝 | 字符串 | 已拒绝注册设备。 |

以下 Javascript 示例显示如何为网络注册更改事件实现侦听器。

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

若要侦听配置文件激活事件， `MobilePlansInlineProfileDownload.profileActivationCompleteScript` 必须将设置为采用字符串的 Javascript 函数的名称字符串 `activationArgs` 。

`activationArgs`是表示 JSON 对象的字符串。

#### <a name="profileactivationcompleteargs"></a>ProfileActivationCompleteArgs

| 属性名称 | 类型 | 描述 |
| --- | --- | -- |
| activationResult | 字符串 | 激活的结果。 此属性的值可在中查看 `MobilePlansActivationError` 。 |
| iccid | 字符串 | 已激活的配置文件的 ICCID。 |

#### <a name="mobileplansactivationerror"></a>MobilePlansActivationError

| 属性名称 | 类型 | 描述 |
| --- | --- | -- |
| success | 字符串 | 指示操作成功。 |
| notAuthorized | 字符串 | 指示操作未获得授权。 |
| notFound | 字符串 | 指示找不到指定的 eSIM 配置文件。 |
| policyViolation | 字符串 | 指示该操作违反策略。 |
| insufficientSpaceOnCard | 字符串 | 指示卡上没有足够的存储空间来完成此操作。 |
| serverFailure | 字符串 | 指示在操作过程中发生服务器故障。 |
| serverNotReachable | 字符串 | 指示在操作过程中无法访问服务器。 |
| timeoutWaitingForUserConsent | 字符串 | 指示未在操作的超时期限内授予用户同意。 |
| incorrectConfirmationCode | 字符串 | 指示在操作过程中提供了错误的确认代码。 |
| confirmationCodeMaxRetriesExceeded | 字符串 | 指示在操作过程中提供了错误的确认代码，但不允许重试。 |
| cardRemoved | 字符串 | 指示已删除 SIM 卡。 |
| cardBusy | 字符串 | 指示 SIM 卡处于繁忙状态。 |
| 其他 | 字符串 | 指示对于更具体的状态不考虑的状态。 |
| cardGeneralFailure | 字符串 | 指示发生了阻止下载、安装或其他操作成功完成的卡错误。 |
| confirmationCodeMissing | 字符串 | 指示下载 eSIM 配置文件时需要确认代码。 |
| invalidMatchingId | 字符串 | 指示已拒绝激活代码或发现的事件中的匹配 ID。 |
| noEligibleProfileForThisDevice | 字符串 | 表示找不到与此设备兼容的 eSIM 配置文件。 例如，发现需要支持 LTE 的配置文件，但设备仅支持3G。 |
| operationAborted | 字符串 | 指示操作中止。 |
| eidMismatch | 字符串 | 指示移动运营商服务器上的 eSIM 配置文件已分配给与设备具有的不同 eSIM EID。 |
| profileNotAvailableForNewBinding | 字符串 | 指示用户正在尝试下载已声明或下载的 eSIM 配置文件。 |
| profileNotReleasedByOperator | 字符串 | 指示 eSIM 配置文件可用，但尚未将其标记为 "已发布" 以供移动运营商下载。 只能下载已发布的配置文件，因此 MO 需要将配置文件标记为 "已发布"。 |
| operationProhibitedByProfileClass | 字符串 | 指示该 eSIM 配置文件类不允许该操作。 |
| profileNotPresent | 字符串 | 指示找不到 eSIM 配置文件。 |
| noCorrespondingRequest | 字符串 | 指示找不到相应的请求。 |
| unknownError | 字符串 | 指示 LPA 返回了一个未知错误。 |
| lpaInitializationError | 字符串 | 指示在尝试初始化 LPA 时出错。 |
| modemNotFound | 字符串 | 指示在设备上找不到移动电话调制解调器。 |
| localSettingsAccessFailed | 字符串 | 指示访问应用的本地设置失败。 |
| invalidJson | 字符串 | 指示在调用移动计划应用时，MO 门户提供了无效的 JSON。 |
| invalidActivationCode | 字符串 | 指示 MO 门户具有无效激活代码。 |
| invalidIccid | 字符串 | 指示 MO 门户指定了无效的 ICCID。 |

下面的 Javascript 示例演示如何为配置文件激活事件实现侦听器。

```Javascript
function onActivationComplete(activationArgs) {
    var activationObj = JSON.parse(activationArgs);
    if(activationObj.activationResult == MobilePlansActivationError.success)
        Log('Activation Success');
}
```

## <a name="delayed-esim-profile-download-and-activation"></a>延迟 eSIM 配置文件下载和激活

下图显示了移动计划应用如何支持延迟下载和激活 eSIM 配置文件的调用流。 当在 SM + 服务器上不提供 eSIM 配置文件，并且只能在一段时间后下载，则应使用此功能。 下载并激活配置文件后，设备应能够在移动电话网络上注册。

![移动计划延迟的配置文件下载序列图](images/mobile_plans_delay_profile_flow.png)

### <a name="mobileplansinlineoperationsnotifyprofiledownloadpurchasemetadata-activationcode-downloaddelay"></a>MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData, activationCode, downloadDelay)

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户购买的元数据。 这包括有关用户帐户、购买方法或仪器的详细信息、用户是否添加新行的详细信息，以及用户所购买的计划的名称。 所有这些都用于报告。 |
| activationCode | 字符串 | 配置文件所在的激活代码或 SM + 地址
| downloadDelay | uint | 尝试下载 eSIM 配置文件之前要等待的分钟数

| 返回值类型 | 描述 |
| --- | --- |
| MobilePlansOperationContext | 一个对象，其中包含与此唯一下载操作匹配的标识符。

在调用后立即将控制权返回给移动运营商门户。 将显示 "UI"，通知用户稍后将安装配置文件。 此 `downloadDelay` 分钟后，将向用户显示一条通知，邀请他们开始下载配置文件的过程。

以下 Javascript 函数举例说明了如何通知应用程序配置文件下载延迟应该开始的 API

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

有关 puchaseMetadata 对象的详细信息，请参阅[购买元数据属性](#purchase-metadata-properties-details)。

请参阅上面[的 "侦听网络注册更改](#listening-for-network-registration-changes)" 部分。

请参阅上面[的侦听配置文件激活](#listening-for-profile-activation)部分。

## <a name="cancel-esim-profile-download"></a>取消 eSIM 配置文件下载

这适用于延迟的 eSIM 配置文件下载方案，但也可用于将来的用例。

下图显示了在没有控件离开 MODirect 门户的情况下，移动计划程序如何支持取消 eSIM 配置文件下载。

![移动计划取消 eSIM 配置文件下载序列图](images/mobile_plans_cancel_profile_download_flow.png)

### <a name="mobileplansinlineoperationsnotifyoperationcancelmobileplansoperationcontext"></a>MobilePlansInlineOperations.notifyOperationCancel(MobilePlansOperationContext)

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| operationContext | Object | 此对象包含唯一标识上一个操作的信息 |

此操作可在用户看到 toast 通知之前取消，通知他们下载已准备好开始。

以下 Javascript 函数显示了用于取消异步操作的 API 示例。

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

下图显示了移动计划应用如何支持延迟连接的高级别流。 如果 SM + 服务器已可供释放 eSIM 配置文件，则应使用此回调方法，但设备需要等待一段时间，然后才能尝试注册到移动电话网络。

![移动计划延迟连接序列图](images/dynamo_async_connectivity_flow.png)

用户成功完成激活流后，web 门户会通知移动计划应用它应使用 API 触发延迟连接流 `MobilePlans.notifyPurchaseWithProfileDownload` 。

### <a name="mobileplansnotifypurchasewithprofiledownload"></a>MobilePlans.notifyPurchaseWithProfileDownload

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户购买的元数据。 这包括有关用户帐户、购买方法或仪器的详细信息、用户是否添加新行的详细信息，以及用户所购买的计划的名称。 所有这些都用于报告。 |
| activationCode | 字符串 | 用于下载 eSIM 配置文件的激活代码。 配置文件的 ICCID 是从配置文件元数据推断而来的。 |
| networkRegistrationInterval | 无符号的整数 | 移动运营商设置与用户的连接所需的时间。 移动计划应用尝试在指定的时间间隔内注册到网络，以分钟为单位。 **注意**此时间将舍入为最接近的15分钟时间间隔。 例如，如果设置为5分钟，应用程序将在大约15分钟后尝试重新注册到网络（但可能需要更长时间）。 如果设置为 "0"，则设备将立即尝试注册。 |

以下 Javascript 函数显示一个 API 示例，用于通知应用程序用户购买要求延迟预配连接。

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

有关 puchaseMetadata 对象的详细信息，请参阅[购买元数据属性](#purchase-metadata-properties-details)。

## <a name="adding-balance"></a>添加余额

当用户通过在现有帐户中添加更多余额来完成在 web 门户中的购买时，web 门户应调用 `MobilePlansInlineOperations.notifyBalanceAddition` API 返回到移动计划应用的控制。 这可用于已安装到设备中的*物理 SIM*或*eSIM 配置文件*。

下图显示了移动计划应用如何支持添加余额的高级流。

![移动计划添加 balancesequence 关系图](images/mobile_plans_add_balance_flow.png)

### <a name="mobileplansinlineoperationsnotifybalanceadditionpurchasemetadata"></a>MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData)

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户购买的元数据。 这包括有关用户帐户、购买方法或仪器的详细信息、用户是否添加新行的详细信息，以及用户所购买的计划的名称。 所有这些都用于报告。 |

| 返回值类型 | 描述 |
| --- | --- |
| MobilePlansOperationContext | 一个对象，其中包含与此唯一下载操作匹配的标识符。

当移动运营商要将余额添加到给定帐户时，web 门户应调用该 `MobilePlansInlineOperations.notifyBalanceAddition` API。

以下 Javascript 函数显示一个 API 示例，用于通知应用程序已进行了余额增加。

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

有关对象的详细信息，请参阅[购买元数据属性](#purchase-metadata-properties-details) `puchaseMetadata` 。

## <a name="adding-balance-and-activate-esim-profile"></a>添加余额并激活 eSIM 配置文件

当用户通过将更多数据添加到现有帐户来完成 web 门户中的 purcahse 时，web 门户应调用 `MobilePlansInlineOperations.notifyBalanceAddition` API 返回到移动计划应用的控制。 这可以用于设备上已安装的*eSIM 配置文件*。 ICCID 参数指示应激活哪个 eSIM 配置文件。

下图显示了移动计划应用如何支持向 iccid 信息添加余额的调用流。

![移动计划添加 balancesequence 关系图](images/mobile_plans_add_balance_iccid_flow.png)

### <a name="mobileplansinlineoperationsnotifybalanceadditionpurchasemetadata-iccid"></a>MobilePlansInlineOperations. notifyBalanceAddition （purchaseMetaData，iccid）

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户购买的元数据。 这包括有关用户帐户、购买方法或仪器的详细信息、用户是否添加新行的详细信息，以及用户所购买的计划的名称。 所有这些都用于报告。 |
| iccid | 字符串 | 应在余额增加后变为活动状态的 ICCID

| 返回值类型 | 描述 |
| --- | --- |
| MobilePlansOperationContext | 一个对象，其中包含与此唯一下载操作匹配的标识符。

如果配置文件的 ICCID 已知，还可以将余额添加到非活动配置文件。 使用 `MobilePlansInlineOperations.notifyBalanceAddition` WITH ICCID 将告知应用余额增加，并将活动配置文件切换到与所提供的 ICCID 对应的配置文件。

以下 Javascript 函数显示一个 API 示例，用于通知应用程序已进行了余额增加。

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

有关对象的详细信息，请参阅[购买元数据属性](#purchase-metadata-properties-details) `puchaseMetadata` 。

## <a name="canceling-purchase-flow"></a>正在取消采购流

如果用户在 web 门户中取消激活流，则门户必须调用 `MobilePlans.notifyCancelledPurchase` API，以将控制权返回给移动计划应用。

### <a name="mobileplansnotifycancelledpurchase"></a>MobilePlans.notifyCancelledPurchase

| 参数名称 | 类型 | 描述 |
| --- | --- | -- |
| purchaseMetadata | Object | 此对象包含有关用户购买的元数据。 这包括有关用户帐户、购买方法或仪器的详细信息、用户是否添加新行的详细信息，以及用户所购买的计划的名称。 所有这些都用于报告。 |

以下 Javascript 函数显示一个 API 示例，用于通知应用程序用户已取消购买。

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

有关对象的详细信息，请参阅[购买元数据属性](#purchase-metadata-properties-details) `puchaseMetadata` 。

## <a name="purchase-metadata-properties-details"></a>购买元数据属性详细信息

下表描述了在购买元数据中使用的详细信息。

| 属性名称 | 类型 | 描述 | 示例 |
| --- | --- | --- | --- |
| 用户帐户 | 字符串 | 可能的值： <ul><li>新：指示用户创建了一个新的用户帐户。</li><li>现有：表示用户使用现有的用户帐户登录。</li><li>帮：指示用户在此步骤结束了购买流程。</li><li>无：表示用户未到达此步骤。</li></ul> | "用户帐户"： "New" |
| purchaseInstrument | 字符串 | 可能的值： <ul><li>新：指示用户创建了一个新的用户帐户。</li><li>现有：表示用户使用现有的用户帐户登录。</li><li>帮：指示用户在此步骤结束了购买流程。</li><li>无：表示用户未到达此步骤。</li></ul> | "purchaseInstrument"： "New" |
| line | 字符串 | 可能的值： <ul><li>新：指示已由用户帐户添加 SIM 卡。</li><li>现有：指示用户已将现有行传输到设备。</li><li>帮：指示用户在此步骤结束了购买流程。</li><li>无：表示用户未到达此步骤。</li></ul> | "line"：新建 " |
| moDirectStatus | 字符串 | 可能的值： <ul><li>Complete：表示用户已成功完成购买。</li><li>ServiceError：指示由于 MO 服务错误，用户无法完成购买。</li><li>InvalidSIM：指示传递到门户的 ICCID 不正确。</li><li>LogOnFailed：指示用户无法登录到 MO 门户。</li><li>PurchaseFailed：指示采购因计费错误而失败。</li><li>关于 microsoft.relay：指示传递到门户的参数无效。</li>BillingError：指示用户计费出错。</li></ul> | "moDirectStatus"： "Complete" |
| planName | 字符串 | 对于成功的事务，此字段不能为空，并且必须提供描述性计划名称。 如果事务未成功，则此字段必须为空字符串。 | "planName"： "2GB 每月"|

## <a name="legacy-callback-notifications"></a>传统回调通知

请参阅[记录所有旧式回调](mobile-plans-legacy-callback-notifications.md)的特定页面。
