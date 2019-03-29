---
title: 短信设备存储限制
description: 短信设备存储限制
ms.assetid: b2491562-352e-4881-99c7-98d43aeec64b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976c7b48b996848c3cdfa9bac7292e56724dbe1b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568310"
---
# <a name="sms-device-storage-limits"></a>短信设备存储限制


SMS 客户端应用程序应使用短信设备存储为消息队列。 在设备上的总 SMS 存储各不相同，但设备存储空间通常限制为 30 的消息。

移动宽带短信平台旨在仍然能够通过释放 SMS 设备存储空间，同时最大程度的用户数据删除接收新传入的 SMS 消息。

如果 SMS 存储已满，则设备无法接收新的 SMS 消息。 Windows 会自动从设备存储空间来确保能够接收新传入的 SMS 数据，例如重要移动网络运营商通知中删除旧的 SMS 消息。

我们的建议如下：

-   SMS 客户端应用程序应使用本地应用程序存储维护而不是依靠 SMS 存储设备的消息历史记录。

-   SMS 客户端应用程序不应在读取上删除消息。 SMS 客户端应用程序，应让 Windows 设备的存储已满时自动删除旧的消息。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 SMS 应用程序](developing-sms-apps.md)

 

 






