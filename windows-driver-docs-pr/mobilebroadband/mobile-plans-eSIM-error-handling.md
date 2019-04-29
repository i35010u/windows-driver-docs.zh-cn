---
title: 移动计划 esim 卡下载错误处理
description: 本主题介绍在移动计划 esim 卡下载错误处理。
ms.assetid: ADBE885A-76E9-4C1E-A729-40ABE58B77E1
keywords:
- Windows Mobile 计划 esim 卡的错误处理，移动计划实现的移动运营商
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: f79b394aa64da93fdf4dba0e0fc9fb62cd20cbc6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357701"
---
# <a name="mobile-plans-esim-download-error-handling"></a>移动计划 esim 卡下载错误处理

## <a name="overview"></a>概述

计划移动应用都尝试修复其中 esim 卡配置文件下载未成功完成的情况下的内置重试解决方案。 但是，在某些情况下，移动运营商干预有必要确保 esim 卡安装在设备上。 移动运营商可以支持 esim 卡中的错误处理其 web 门户以其客户提供愉悦。

## <a name="handling-esim-download-errors"></a>Esim 卡下载错误处理

计划移动应用具有一项功能，用户重新进入门户后，错误代码将传递到 MO 门户。 下面的示例演示应用程序如何通过相关参数。

```HTTP
GET https://moportal.com/?market=US&location=US&transactionId=HADRdRhKI0S5bN4n.1&eid=89033023422130000000000199272786&imei=001102000224082 HTTP/1.1
X-MP-LPAError-Codes: ServerFailure,ServerNotReachable
X-MP-LPAError-TimeStamps: 5/18/2018 11:17:23 PM,5/18/2018 11:27:33 PM
X-MP-LPAError-ICCIDs: 8988247000101997790
```

计划移动应用添加三个标头，如下表中所述。

| 标头名称              | 描述                                                                                                                                                                                                                                                                                                                          | 示例                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| X-MP-LPAError-Codes      | 此字段提供 LPA 内捕获的错误代码。 如果有多个错误，错误代码传递以逗号分隔的列表。 <p>有关可能的错误代码的列表，请参阅[ESimOperationStatus 枚举](https://docs.microsoft.com/uwp/api/windows.networking.networkoperators.esimoperationstatus)。</p> | X-MP-LPAError 的代码：ServerFailure,ServerNotReachable                 |
| X-MP-LPAError-TimeStamps | 此字段提供了在发生错误时的时间戳。 时间戳的格式*日期时间 UTC 偏移量*。 如果有多个错误，以逗号分隔列表的形式传递时间戳。                                                                                                                                 | X-MP-LPAError-时间戳：2018 年 5 月 18 日晚上 11:17:23，2018 年 5 月 18 日晚上 11:27:33 |
| X-MP-LPAError-ICCIDs     | 此字段提供的 esim 卡配置文件的用户尝试下载并安装 ICCID。 返回到计划移动应用传递此 ICCID 控件切换过程中出现。 只有一个 ICCID 被传递。                                                                                                                       | X-MP-LPAError-ICCIDs:8988247000101997790                             |

移动运营商可能选择不支持处理通过计划移动应用程序中，传递的错误，但我们建议执行此操作，因为它可以增强用户体验。

下图显示了向用户显示错误消息的示例：

<img src="images/mobile_plans_implementation_error_message.png" alt="Example of Mobile Plans app eSIM download error" title="示例中的计划移动应用 esim 卡下载错误" width="600" />
