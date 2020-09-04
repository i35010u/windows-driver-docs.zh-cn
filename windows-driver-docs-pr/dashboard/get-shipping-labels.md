---
title: 获取发货标签数据
description: Microsoft 硬件 API 中的这些方法可获取注册到开发人员中心帐户的硬件产品的发货标签。
ms.topic: article
ms.date: 10/03/2019
ms.openlocfilehash: a60fefd0e1d2b7acd648dc53e822cfeb75b8b7c6
ms.sourcegitcommit: 4f08f5686c0bbc27d58930b993cbab1a98e3afb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89443919"
---
# <a name="get-shipping-label-data"></a>获取发货标签数据

有关 Microsoft 硬件 API 的简介，包括关于使用 API 的先决条件的简介，请参阅[使用 API 管理硬件提交内容](dashboard-api.md)。

使用 Microsoft 硬件 API 中的以下方法可获取注册到硬件开发人员中心帐户的硬件产品的发货标签。 

```html
https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/
```

在使用这些方法之前，产品和提交内容必须已在你的开发人员中心帐户中存在。 若要创建或管理产品的提交内容，请参阅[管理产品提交内容](manage-product-submissions.md)中的方法。

|说明|方法|URI|
|-|-|-|
|[获取提交内容的所有发货标签的数据](get-all-shipping-labels.md)|GET|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/`|
|[获取提交内容的特定发货标签的数据](get-a-shipping-label.md)|GET|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/{shippingLabelId}`|

## <a name="prerequisites"></a>必备条件

如果尚未开始操作，请先满足 Microsoft 硬件 API 的所有[先决条件](./dashboard-api.md#complete-the-prerequisites-for-using-the-microsoft-hardware-api)，然后尝试使用下述任一方法。

## <a name="data-resources"></a>数据资源

用于获取发货标签数据的 Microsoft 硬件仪表板 API 方法使用以下 JSON 数据资源。

### <a name="shippinglabel-resource"></a>ShippingLabel 资源

此资源表示针对注册到帐户的产品提交内容创建的发货标签。

```json
{
  "id": 1152921504606978422,
  "productId": 14461751976964157,
  "submissionId": 1152921504621467613,
  "publishingSpecifications": {
    "goLiveDate": "2018-04-12T05:28:32.721Z",
    "visibleToAccounts": [
      27691110, 27691111
    ],
    "isAutoInstallDuringOSUpgrade": true,
    "isAutoInstallOnApplicableSystems": true,
    "isDisclosureRestricted": false,
    "publishToWindows10s": false,
    "additionalInfoForMsApproval": {
      "microsoftContact": "abc@microsoft.com",
      "validationsPerformed": "Validation 1",
      "affectedOems": [
        "OEM1", "OEM2"
      ],
      "isRebootRequired": false,
      "isCoEngineered": true,
      "isForUnreleasedHardware": true,
      "hasUiSoftware": false,
      "businessJustification": "This is a business justification"
    }
  },
  "recipientSpecifications": {
    "receiverPublisherId": "27691110",
    "enforceChidTargeting": true
  },
  "targeting": {
    "hardwareIds": [
      {
        "bundleId": "amd64",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_SERVER_X64_RS5_FULL",
        "pnpString": "hid\\vid_dummy256f&pid_dummyc62f",
        "distributionState": "pendingAdd"
      }
    ],
    "chids": [
      {
        "chid": "346511cf-ccee-5c6d-8ee9-3c70fc7aae83",
        "distributionState": "pendingAdd"
      }
    ],
    "restrictedToAudiences": [
      "00000000-0000-0000-0000-000000000000",
      "00000000-0000-0000-0000-000000000001"
      ],
    "inServicePublishInfo": {
      "flooring": "RS1",
      "ceiling": "RS3"
    },
    "coEngDriverPublishInfo": {
      "flooringBuildNumber": 17135,
      "ceilingBuildNumber": 17139
    }  
  },
  "workflowStatus": {
    "currentStep": "finalizePublishing",
    "state": "completed",
    "messages": [],
    "errorReport": ""
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978422",
      "rel": "self",
      "method": "GET"
    }
  ],
  "name": "Shipping Label Name",
  "destination": "windowsUpdate"
}
```

此资源具有以下值：

| 值 | 类型 | 说明 |
|:--|:--|:--|
|ID|长整型|发货标签的 ID|
|productId|长整型|与此发货标签关联的专用产品 ID|
|submissionId|长整型|与此发货标签关联的提交内容 ID|
|publishingSpecifications|对象|有关更多详细信息，请参阅[发布规范对象](#publishing-specifications-object)|
|recipientSpecifications|对象数组|有关更多详细信息，请参阅[接收方规范对象](#recipient-specifications-object)|
|目标设定|对象|有关更多详细信息，请参阅[目标对象](#targeting-object)|
|workflowStatus|对象|此对象描述此发货标签的工作流状态。 有关更多详细信息，请参阅[发货标签工作流状态对象](#shipping-label-workflow-status-object)|
|links|对象数组|有关详细信息，请参阅[链接对象](get-product-data.md#link-object)。|
|name|字符串|发货标签的名称|
|destination|字符串|指示发货标签的目标。 可能的值为（括号中为说明）： <ul><li>anotherPartner（此发货标签用于与其他合作伙伴共享提交内容） </li><li>windowsUpdate（此发货标签用于发布到 Windows 更新） </li><li>notSet</li></ul>|

### <a name="publishing-specifications-object"></a>发布规范对象

此对象表示有关如何将对象发布到 Windows 更新的规范。 仅当发货标签的 *destination* 为 *windowsUpdate* 时，才可以使用/需要此对象

```json
{
  "goLiveDate": "2018-04-12T05:28:32.721Z",
  "visibleToAccounts": [
    27691110,
    27691111
  ],
  "isAutoInstallDuringOSUpgrade": true,
  "isAutoInstallOnApplicableSystems": true,
  "isDisclosureRestricted": false,
  "publishToWindows10s": false,
  "additionalInfoForMsApproval": {
    "microsoftContact": "abc@microsoft.com",
    "validationsPerformed": "Validation 1",
    "affectedOems": [
      "OEM1",
      "OEM2"
    ],
    "isRebootRequired": false,
    "isCoEngineered": true,
    "isForUnreleasedHardware": true,
    "hasUiSoftware": false,
    "businessJustification": "This is a business justification"
  }
}
```

此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|goLiveDate|日期/时间|该驱动程序在 Windows 更新中可供下载的日期。 如果未提供日期，则认证后立即发布该驱动程序。|
|visibleToAccounts|长整形数组|对驱动程序和发货标签拥有只读权限的 SellerID 列表。 希望合作伙伴注意某个发货标签请求时（例如，代表他们发布驱动程序时），此信息非常有用。|
|isAutoInstallDuringOSUpgrade|布尔值|在操作系统升级期间是否要将该驱动程序传送到适用的计算机。|
|isAutoInstallOnApplicableSystems|布尔值|是否自动将驱动程序传送到适用的计算机。|
|isDisclosureRestricted|布尔值|是否要/应该阻止该驱动程序出现在 WSUS 和 Windows 更新目录中。|
|publishToWindows10s|布尔值|是否将该驱动程序发布到 Windows 10 S|
|additionalInfoForMsApproval|对象|有关信息，请参阅 [Microsoft 对象的其他信息](#additional-information-for-the-microsoft-object)。|

### <a name="additional-information-for-the-microsoft-object"></a>Microsoft 对象的其他信息

此对象表示 Microsoft 在评审发货标签时所需的其他一些信息。 仅当发货标签的 *destination* 为 *windowsUpdate*，并且发货标签已标记为 *isAutoInstallDuringOSUpgrade* 或 *isAutoInstallOnApplicableSystems* 时，才可以使用/需要此对象。

```json
{
    "microsoftContact": "abc@microsoft.com",
    "validationsPerformed": "Validation 1",
    "affectedOems": [
      "OEM1",
      "OEM2"
    ],
    "isRebootRequired": false,
    "isCoEngineered": true,
    "isForUnreleasedHardware": true,
    "hasUiSoftware": false,
    "businessJustification": "This is a business justification"
}
```
此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|microsoftContact|字符串|与你配合处理此请求的 Microsoft 发起人的电子邮件地址|
|validationsPerformed|字符串|有关如何验证驱动程序的说明。 Microsoft 在评审期间将使用此信息。|
|affectedOems|字符串|受此次发布影响的 OEM 的名称列表。 Microsoft 在评审期间将使用此信息。|
|isRebootRequired|布尔值|安装驱动程序后是否需要重新启动。 Microsoft 在评审期间将使用此信息。|
|isCoEngineered|布尔值|该驱动程序是否是用于处理 Windows 现行（尚未发布）内部版本的、联合研发的驱动程序。 Microsoft 在评审期间将使用此信息。|
|isForUnreleasedHardware|布尔值|该驱动程序是否支持新的或未发布的设备。 Microsoft 在评审期间将使用此信息。|
|hasUiSoftware|布尔值|该驱动程序是否部署 UI 和/或软件？ Microsoft 在评审期间将使用此信息。|
|businessJustification|字符串|升级此发布请求的业务理由。 Microsoft 在评审期间将使用此信息。|

### <a name="recipient-specifications-object"></a>接收方规范对象

此对象表示与其他合作伙伴共享的提交内容的详细信息以及共享条件。 仅当发货标签的 *destination* 为 *anotherPartner* 时，才可以使用/需要此对象。

```json
{
    "receiverPublisherId": "27691110",
    "enforceChidTargeting": false
}
```
此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|receiverPublisherId|字符串|与其共享该驱动程序的卖方 ID。 接收方可以下载驱动程序、发布到 Windows 更新以及创建 DUA 包。 接收方不能进一步与其他合作伙伴共享。|
|enforceChidTargeting|布尔值|指示合作伙伴否需要将 CHID 应用到他们为此驱动程序提交内容创建的任何发货标签。 这使你可以在多个合作公司之间共享硬件 ID 时保护用户。|

### <a name="targeting-object"></a>目标对象

此对象表示发布到 Windows 更新时所需的发货标签的目标详细信息。

```json
{
  "hardwareIds": [
    {
      "bundleId": "amd64",
      "infId": "foo.inf",
      "operatingSystemCode": "WINDOWS_v100_SERVER_X64_RS5_FULL",
      "pnpString": "hid\\vid_dummy256f&pid_dummyc62f",
      "distributionState": "pendingAdd"
    }
  ],
  "chids": [
    {
      "chid": "346511cf-ccee-5c6d-8ee9-3c70fc7aae83",
      "distributionState": "pendingAdd"
    }
  ],
  "restrictedToAudiences": [
    "00000000-0000-0000-0000-000000000000",
    "00000000-0000-0000-0000-000000000001"
  ],
  "inServicePublishInfo": {
    "flooring": "RS1",
    "ceiling": "RS3"
  },
  "coEngDriverPublishInfo": {
    "flooringBuildNumber": 17135,
    "ceilingBuildNumber": 17139
  }
}
```
此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|hardwareIds|对象数组|有关详细信息，请参阅[硬件 ID 对象](#hardware-id-object)。|
|chids|对象数组|有关详细信息，请参阅 [CHIDs 对象](#chids-object)。|
|restrictedToAudiences|字符串数组|表示受众的字符串数组。 使用受众可将此项发布限制为采用特定配置的计算机。 例如，只会将测试受众传送到装有特定注册表项的客户端。 有关如何识别和管理适用于组织的受众的信息，请参阅[获取受众数据](get-audience-data.md)。|
|inServicePublishInfo|对象|有关更多详细信息，请参阅[服务中发布信息对象](#in-service-publish-information-object)。 目标对象可以包含 inServicePublishInfo 或 coEngDriverPublishInfo，但不能同时包含两者。 |
|coEngDriverPublishInfo|对象|有关更多详细信息，请参阅[联合研发驱动程序发布信息对象](#co-engineering-driver-publish-information-object)。 目标对象可以包含 inServicePublishInfo 或 coEngDriverPublishInfo，但不能同时包含两者。 |

### <a name="hardware-id-object"></a>硬件 ID 对象

此对象表示发货标签需要针对的硬件 ID 的详细信息。 有关更多详细信息，请参阅[硬件 ID](../install/hardware-ids.md)。

```json
{
    "bundleId": "amd64",
    "infId": "foo.inf",
    "operatingSystemCode": "WINDOWS_v100_SERVER_X64_RS5_FULL",
    "pnpString": "hid\\vid_dummy256f&pid_dummyc62f",
    "distributionState": "pendingAdd"
}
```
此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|bundleId|字符串|表示硬件 ID 所在的捆绑套件的 ID。|
|infId|字符串|包含此硬件 ID 的 inf 文件的名称|
|operatingSystemCode|字符串|适用于此特定硬件 ID - 体系结构组合的操作系统代码。 有关可能值，请参阅 [OS 代码列表](get-product-data.md#list-of-operating-system-codes)。|
|pnpString|字符串|所针对的 PNP ID 或硬件 ID。|
|distributionState|字符串|表示此硬件 ID 的当前目标状态。 可能的值为（括号中为说明）：<ul><li>pendingAdd（已针对此硬件 ID 请求添加操作，并且该操作正在进行） </li><li>pendingRemove（已针对此硬件 ID 请求删除（过期）操作，并且该操作正在进行） </li><li>added（已成功将此硬件 ID 添加为此发货标签中的目标） </li><li>notSet（未执行任何操作，或者未针对此硬件 ID 设置状态） </li></ul>|
|action|字符串|此对象仅在更新/修补发货标签时才适用。 可能的值为： <ul><li>添加</li><li>删除</li></ul> |

创建新的发货标签时，硬件 ID 对象应包含捆绑 ID、PNP ID、OS 代码和 INF 名称的有效组合。 若要获取提交内容（包）的这些属性的允许/有效组合，可以在获取提交内容的详细信息时，下载以链接形式提供的驱动程序元数据文件。 有关详细信息，请参阅[驱动程序包元数据](driver-package-metadata.md)。

### <a name="chids-object"></a>CHIDs 对象

此对象表示发货标签需要针对的 CHID（计算机硬件 ID）。 有关更多详细信息，请参阅[使用 CHID](./using-chids.md)。

```json
{
    "chid": "346511cf-ccee-5c6d-8ee9-3c70fc7aae83",
    "distributionState": "pendingAdd"
}
```

此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|chid|GUID|需要针对的 CHID|
|distributionState|字符串|表示此 CHID 的当前目标状态。 可能的值为（括号中为说明）：<ul><li>pendingAdd（已针对此硬件 ID 请求添加操作，并且该操作正在进行） </li><li>pendingRemove（已针对此硬件 ID 请求删除（过期）操作，并且该操作正在进行） </li><li>added（已成功将此硬件 ID 添加为此发货标签中的目标） </li><li>notSet（未执行任何操作，或者未针对此硬件 ID 设置状态） </li></ul>|
|action|字符串|此对象仅在更新/修补发货标签时才适用。 可能的值为： <ul><li>添加</li><li>删除</li></ul> |

### <a name="in-service-publish-information-object"></a>服务中发布信息对象

此对象表示按下限和上限定义的分发范围。 下限表示驱动程序将分发到的最低 Windows 版本，而上限则表示最新版本。 添加下限和上限可以限制驱动程序的分发。
```json
{
  "flooring": "RS1",
  "ceiling": "RS3",

}
```
此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|flooring|字符串|希望驱动程序只在列出的 Windows 10 操作系统或更高版本的操作系统上提供时，请使用此选项。 例如，选择 RS4 下限意味着只在运行 Windows 10 1803 (RS4) 和更高版本的系统提供此驱动程序。 可能的值为： <ul><li>TH</li><li>RS1</li><li>RS2</li><li>RS3</li><li>RS4</li><li>RS5</li><li>19H1</li></ul> 请注意，可能的值将会扩展，以包含最新版本 的 OS。 |
|ceiling|字符串|对此功能的访问受到限制。  希望只为列出的操作系统或更低版本的系统提供某个驱动程序时，请使用此选项。 例如，在 Windows 10 1607 RS1 认证的驱动程序中选择 RS3 上限意味着，永远不会将驱动程序提供给运行 Windows 10 1803 (RS4) 或更高版本的系统。可能的值为： <ul><li>TH</li><li>RS1</li><li>RS2</li><li>RS3</li><li>RS4</li><li>RS5</li><li>19H1</li></ul> 请注意，可能的值将会扩展，以包含最新版本 的 OS。 |

有关这些值的详细信息，请参阅[按 Windows 版本限制驱动程序分发](./limit-driver-distribution.md)。

### <a name="co-engineering-driver-publish-information-object"></a>联合研发驱动程序发布信息对象

此对象表示在为较新和未发布的 Windows 版本开发驱动程序时，按下限和上限定义的分发范围。 此对象仅适用于 Microsoft 联合研发合作伙伴。  下限表示驱动程序将分发到的最低 Windows 版本，而上限则表示最新版本。 添加下限和上限可以限制驱动程序的分发。 
```json
{
  "flooringBuildNumber": 17135,
  "ceilingBuildNumber": 17139
}
```
此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|flooringBuildNumber|数字|发行软件的内部版本号，你只希望在此内部版本号或更高内部版本中提供某个驱动程序。 例如，如果下限需是 10.1.17135，则输入需是 17135。 主要版本 (10.1) 始终自动默认为相应的版本。|
|ceiling|数字|发行软件的内部版本号，你只希望在此内部版本号或更低内部版本中提供某个驱动程序。 例如，如果上限需是 10.1.17139，则输入需是 17139。 主要版本 (10.1) 始终自动默认为相应的版本。|

有关详细信息，请参阅[按 Windows 版本限制驱动程序分发](./limit-driver-distribution.md)。

### <a name="shipping-label-workflow-status-object"></a>发货标签工作流状态对象

此对象表示给定实体的工作流状态。

```json
{
      "currentStep": "Created",
      "state": "completed",
      "messages": []
    }
```

此对象具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
| currentStep | 字符串 | 此实体的整个工作流中的当前步骤名称。 <br>对于发布到 Windows 更新的发货标签，可能的值为（括号中为说明）：<ul><li>Created（正在创建发货标签） </li><li>PreProcessShippingLabel（正在验证目标信息） </li><li>FinalizePreProcessing（完成预处理后正在调用相应的下一步骤） </li><li>PublishJobValidation（正在验证包引入/提交内容是否完整） </li><li>UpdateGeneration（正在生成 WU 的发布详细信息） </li><li>MicrosoftApproval（事务升级/正在进行外部测试） </li><li>Publishing（正在将发布详细信息推送到 WU） </li><li>FinalizePublishing（正在完成发布过程） </li></ul> 对于与其他合作伙伴共享的发货标签，可能的值为（括号中为说明）： <ul><li>Created（正在创建发货标签） </li><li>PreProcessShippingLabel（正在验证目标信息） </li><li>FinalizePreProcessing（完成预处理后正在调用相应的下一步骤） </li><li>PublishJobValidation（正在验证包引入/提交内容是否完整） </li><li>ProcessSharing（正在为接收方生成共享详细信息） </li><li>FinalizeSharing（正在完成共享过程） </li></ul>|
| State | 字符串 | 当前步骤的状态。 可能的值为：<ul><li>notStarted</li><li>started</li><li>失败</li><li>completed</li></ul> |
| Messages | 数组 | 一个字符串数组，用于提供有关当前步骤的消息（尤其是失败的情况下） |

## <a name="error-codes"></a>错误代码

有关错误代码的信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
