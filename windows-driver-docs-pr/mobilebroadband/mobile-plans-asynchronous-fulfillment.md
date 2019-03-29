---
title: 移动计划异步执行
description: 移动计划异步执行
ms.assetid: 56AB67D6-59A9-4483-B455-2FCC309C8903
keywords:
- Windows Mobile 计划异步执行移动运算符
ms.date: 11/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7eda3efa87bb0811e2f465fe61d5bb3562b3b6e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563929"
---
# <a name="mobile-plans-asynchronous-fulfillment"></a>移动计划异步执行

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

## <a name="overview"></a>概述

本主题提供有关下列任一情况下需要异步执行的移动运营商 API 的详细信息：

- 异步连接： 当移动运营商不能立即向用户授予连接，在用户购买后下载配置文件时。
- 异步的配置文件传递： 当该配置文件不是可供在购买时的下载。

## <a name="asynchronous-connectivity"></a>异步连接

下图显示了如何为高级流程*移动计划*程序支持延迟的连接。

![移动计划延迟的连接序列图](images/dynamo_async_connectivity_flow.png)

用户已成功完成购买，需要从移动运营商 MO 直接门户的配置文件下载后，门户将通知计划移动应用程序，它应触发延迟的连接流使用`MobilePlans.notifyPurchaseWithProfileDownload`API。 

### <a name="mobileplansnotifypurchasewithprofiledownload"></a>MobilePlans.notifyPurchaseWithProfileDownload

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | 对象 | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
| activationCode | 字符串 | 正在下载 esim 卡配置文件激活代码。 配置文件的 ICCID 推断从配置文件元数据。 |
| networkRegistrationInterval | 无符号的整数 | 移动运营商向用户预配连接到所需的时间。 计划移动应用程序尝试在网络内注册指定的时间间隔，以分钟为单位。 **请注意**这一次舍入为最接近的 15 分钟间隔。 例如，如果此值设置为 5 分钟，则应用程序尝试重新注册到该网络在大约 15 分钟后 （但可能需要花费更长）。 |

以下 Javascript 函数显示 API 来通知用户购买需要连接延迟预配的应用程序的示例。

 ```Javascript
function finishPurchaseWithDownload() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.new;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.complete;
        metadata.line = MobilePlansLineType.new;
        metadata.planName = "2GB Monthly";
        MobilePlans.notifyPurchaseWithProfileDownload(metadata, "1$smdp.address$", 15);
}
```

| 属性名 | 在任务栏的搜索框中键入 | 描述 | 示例 |
| --- | --- | --- | --- |
| userAccount | 字符串 | 可能值： <ul><li>新建：指示用户已创建了新的用户帐户。</li><li>现有:指示用户记录的现有用户帐户。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul> | "userAccount":"New" |
| purchaseInstrument | 字符串 | 可能值： <ul><li>新建：指示用户已创建了新的用户帐户。</li><li>现有:指示用户记录的现有用户帐户。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul> | "purchaseInstrument":"New" |
| 行 | 字符串 | 可能值： <ul><li>新建：指示 SIM 卡已添加的用户帐户。</li><li>现有:指示用户传输到设备的某一现有行。</li><li>他：指示用户已在此步骤中的采购流程结束。</li><li>None:指示用户未到达此步骤。</li></ul> | "line":New" |
| moDirectStatus | 字符串 | 可能值： <ul><li>完成：指示用户已成功完成购买。</li><li>服务错误：表示用户无法完成购买由于月服务错误。</li><li>InvalidSIM:表示传递给在门户 ICCID 时不正确。</li><li>LogOnFailed： 表示用户无法登录到 MO 门户。</li><li>PurchaseFailed:指示在购买由于计费错误而失败。</li><li>ClientError:指示无效的参数已传递到门户。</li>BillingError:指示已具有用户计费的错误。</li></ul> | "moDirectStatus":"Complete" |
| planName | 字符串 | 对于成功的事务，此字段不能为空，并且必须提供一个描述性的计划名称。 对于失败的事务，此字段必须是空字符串。 | "planName":"每月 2 GB"|


## <a name="asynchronous-profile-delivery"></a>异步的配置文件交付

下图显示了如何为高级流程*移动计划*程序支持延迟的配置文件下载。

![移动计划延迟配置文件下载序列图](images/dynamo_async_profile_flow.png)

用户已成功完成购买，需要从移动运营商 MO 直接门户的配置文件下载后，门户将通知计划移动应用程序，它应触发延迟的配置文件下载流使用`MobilePlans.notifyPurchaseDelayedProfile`API。 

### <a name="mobileplansnotifypurchasedelayedprofile"></a>MobilePlans.notifyPurchaseDelayedProfile

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | 对象 | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
| profileDownloadDelayInterval | 无符号的整数 | 所需的时间移动运营商创建的用户配置文件的配置文件并将其从 SM DS 下载准备就绪。 计划移动应用下载配置文件从 SM DS 此间隔过后，在分钟。 **请注意**这一次舍入为最接近的 15 分钟间隔。 例如，如果此值设置为 5 分钟，该应用程序会尝试之后大约 15 分钟后 （可能需要更长） 下载到网络|

以下 Javascript 函数显示 API 以通知应用程序用户购买，需要使用 SM DS 延迟的配置文件下载的示例。

 ```Javascript
function finishPurchaseWithSMDS() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.new;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.complete;
        metadata.line = MobilePlansLineType.new;
        metadata.planName = "2GB Monthly";
        MobilePlans.notifyPurchaseDelayedProfile(metadata, 15);
}
```

## <a name="inline-profile-delivery"></a>内联配置文件交付

下图显示了如何为高级流程*移动计划*程序支持而无需控制离开 MODirect 门户下载配置文件。

![移动计划内联配置文件下载序列图](images/dynamo_inline_profile_flow.png)

在门户的配置文件下载、 安装和激活发生准备就绪 MO 直接门户时，应调用`MobilePlansInlineProfile.notifyInlineProfileDownload`。

### <a name="mobileplansinlineprofilenotifyinlineprofiledownload"></a>MobilePlansInlineProfile.notifyInlineProfileDownload

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | 对象 | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
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
    MobilePlansInlineProfileDownload.notifyInlineProfileDownload(purchaseMetaData , "1$smdp.address$"); 
}
```

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

若要侦听的配置文件激活事件`MobilePlansInlineProfileDownload.profileActivationCompleteScript`必须设置为所需字符串的 Javascript 函数的名称的字符串 `activationArgs`

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
| invalidCallback | 字符串 | 指示 MO 门户提供回调无效。 |
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

## <a name="adding-balance"></a>添加余额

当用户完成购买 MO 直接门户中的通过将更多的数据添加到他们的帐户 （由于用户 esim 卡上使用当前配置文件需要进行任何配置文件下载） 时，应调用 MO 门户`MobilePlans.notifyBalanceAddition`API 将控制权返回给移动计划应用程序。

### <a name="mobileplansnotifybalanceaddition"></a>MobilePlans.notifyBalanceAddition

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | 对象 | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |
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

## <a name="canceling-purchase-flow"></a>取消购买流

如果用户取消购买流在 MO 门户中，则必须调用门户`MobilePlans.notifyCancelledPurchase`API 来将控制权返回给计划移动应用。

### <a name="mobileplansnotifycancelledpurchase"></a>MobilePlans.notifyCancelledPurchase

| 参数名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | -- |
| purchaseMetadata | 对象 | 此对象包含有关用户的购买的元数据。 这包括有关用户帐户、 采购方法或检测的详细信息、 详细信息，如果用户添加一个新行，并且用户购买的计划的名称。 所有这些用于报告。 |

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

> [!NOTE]
> 取消和平衡添加流使用`DataMart.notifyPurchaseResult`API 仍受支持。 

## <a name="frequently-asked-questions"></a>常见问题

1. 是*事务 ID*仍然需要？  

    移动运营商不需要返回*事务 ID*传递到门户，但他们需要对存储进行故障排除此值。  

2. 应使用哪个 API 将控制权返回到*移动计划*连接可用时立即？  

    `MobilePlans.notifyPurchaseDelayedProfile`今后在此方案支持的 API。 在此特定情况下， *networkRegistrationInterval*参数应设置为**0**。  

    如果已实现`MobilePlans.notifyPurchaseResult`集成指南中指定的 API 仍受支持。  

3. 是仍所需的 esim 卡激活回调的 ICCID 信息？  

    添加平衡方案中，仅需要 ICCID 信息时`MobilePlans.notifyBalanceAddition`使用 API 回调。  

    如果已实现`MobilePlans.notifyPurchaseResult`集成指南中指定的 API 仍受支持。  

4. 如果仍需要帮助？  

    请与 Microsoft 代表联系。
