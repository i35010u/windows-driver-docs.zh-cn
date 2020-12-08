---
title: 短信设备存储限制
description: 短信设备存储限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aca894688deabd6303ebc96f7a436489111b83a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830355"
---
# <a name="sms-device-storage-limits"></a>短信设备存储限制


SMS 客户端应用应使用 SMS 设备存储作为消息队列。 设备上的 SMS 存储总数有所不同，但设备存储通常限制为30条消息。

移动宽带 SMS 平台旨在维持在最大程度减少用户数据删除的情况下，通过释放 SMS 设备存储空间来接收新的传入 SMS 消息的功能。

如果 SMS 存储已满，则设备无法接收新的 SMS 消息。 Windows 将自动从设备存储中删除旧的 SMS 消息，以确保能够接收新的传入 SMS 数据，如重要的移动网络操作员通知。

建议如下：

-   SMS 客户端应用应使用本地应用存储来维护消息历史记录，而不是依赖于设备 SMS 存储。

-   SMS 客户端应用程序不应在读取时删除消息。 当设备存储已满时，SMS 客户端应用应允许 Windows 自动删除旧的消息。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发短信应用](developing-sms-apps.md)

 

 






