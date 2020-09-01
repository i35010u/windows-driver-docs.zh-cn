---
title: 移动计划 eSIM 配置文件下载错误处理
description: 本主题介绍移动计划中的 eSIM 下载错误处理。
ms.assetid: ADBE885A-76E9-4C1E-A729-40ABE58B77E1
keywords:
- Windows Mobile 计划 eSIM 错误处理，移动计划实现移动运营商
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5f3d55d68b8a4f6b2ddcb6d6737129d17ceeeac1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207327"
---
# <a name="mobile-plans-esim-profile-download-error-handling"></a>移动计划 eSIM 配置文件下载错误处理

## <a name="overview"></a>概述

移动计划应用包含一个内置重试解决方案，该解决方案将尝试修复 eSIM 配置文件下载未成功完成的情况。 但是，在某些情况下，需要移动运营商的干预才能确保设备上已安装 eSIM 卡。 移动运营商可以支持在其 web 门户中使用 eSIM 错误处理来感到满意其使用者。

## <a name="handling-esim-download-errors"></a>处理 eSIM 下载错误

移动计划应用包含一项功能，该功能在用户重新进入门户后将错误代码传递到 MO 门户。 下面的示例演示应用如何传递相关 azuredeploy-paremeters.json。

```HTTP
GET https://moportal.com/?market=US&location=US&transactionId=HADRdRhKI0S5bN4n.1&eid=89033023422130000000000199272786&imei=001102000224082 HTTP/1.1
X-MP-LPAError-Codes: ServerFailure,ServerNotReachable
X-MP-LPAError-TimeStamps: 5/18/2018 11:17:23 PM,5/18/2018 11:27:33 PM
X-MP-LPAError-ICCIDs: 8988247000101997790
```

移动计划应用添加三个标头，下表对此进行了说明。

| 标头名称              | 说明                                                                                                                                                                                                                                                                                                                          | 示例                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| LPAError-      | 此字段提供 LPA 中捕获的错误代码。 如果存在多个错误，则以逗号分隔的列表形式传递错误代码。 <p>有关可能的错误代码的列表，请参阅 [ESimOperationStatus 枚举](/uwp/api/windows.networking.networkoperators.esimoperationstatus)。</p> | LPAError： ServerFailure，ServerNotReachable                 |
| LPAError-时间戳 | 此字段提供发生错误时的时间戳。 时间戳的格式为 *日期时间 UTC 偏移量*。 如果存在多个错误，则时间戳将作为以逗号分隔的列表进行传递。                                                                                                                                 | LPAError-时间戳： 5/18/2018 11:17:23 PM，5/18/2018 11:27:33 PM |
| LPAError-Iccid     | 此字段提供用户尝试下载和安装的 eSIM 配置文件的 ICCID。 发生控制切换时，此 ICCID 被传递回移动计划应用。 只传递了一个 ICCID。                                                                                                                       | LPAError-Iccid：8988247000101997790                             |

移动运营商可能选择不支持处理移动计划应用传递的错误，但建议这样做，因为这样可以增强用户体验。

下图显示了向用户显示的错误消息的示例：

<img src="images/mobile_plans_implementation_error_message.png" alt="Example of Mobile Plans app eSIM download error" title="移动计划应用卡下载错误示例" width="600" />