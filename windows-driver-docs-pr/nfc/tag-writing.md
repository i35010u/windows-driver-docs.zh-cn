---
title: 标记写入
description: 标记写入
ms.assetid: 916150D9-9A98-4463-81BE-7F46DF2694F4
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a82a2dc429beba49e724a62f452cf53d31a3103
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827343"
---
# <a name="tag-writing"></a>标记写入


为类别指定了标记写入： General、NFC 和 All。 在每个类别中，驱动程序将仅识别特定类型的标记。

这是允许将消息写入任何 NearFieldProximity 标记的特殊发布。 必须覆盖标记的任何现有有效负载。 仅为 NFC 定义了 Append 语义。 如果客户端想要附加而不是覆盖，则它必须构造一个 NDEF 有效负载，其中包含原始的 NDEF 消息，并将其放入 "NDEF： WriteTag" 发布。 在任何给定时刻，都应使用零个或一个 "\*： WriteTag" 发布。

## <a name="general-tag-writing"></a>常规标记写入


标记写入是一项可选功能，适用于未启用 NFC 的 NFP 提供程序。 驱动程序只能识别以下类型的发布标记类型：

-   "WindowsUri:WriteTag"
-   "WindowsMime:WriteTag"
-   "Windows： WriteTag"

## <a name="nfc-tag-writing"></a>NFC 标记写入


启用 NFC 的 NFP 提供程序需要标记写入支持。 必须满足这些要求。

如果邻近技术被播发为 NFC，则驱动程序必须仅识别适用于发布的以下标记类型：

-   "WindowsUri:WriteTag"
-   "WindowsMime:WriteTag"
-   "Windows： WriteTag"
-   "NDEF:WriteTag"

严格的 NDEF 编码规则按照 NFC 论坛规范使用。 例如，NDEF 消息片段不能写入（即使在有效的 NDEF 消息中）。

**请注意**，对于 NFC 标记  ，如果未对标记进行 NDEF 格式设置，则为 \*发布一条消息。WriteTag，提供程序必须将标记格式化为 NDEF，然后写入负载。

 

## <a name="all-tag-writing"></a>所有标记写入


如果 NFP 提供程序完全支持标记写入，则驱动程序必须满足所列出的所有要求。

### <a name="required-actions"></a>必需的措施

-   驱动程序不得识别任何 "\*： WriteTag" 订阅。
-   如果启用了一个或多个 "\*： WriteTag" 发布，并且驱动程序检测到具有足够可用空间的可写标记，则不能读取标记的现有负载以匹配其他订阅。 这允许标记写入应用抢占可能订阅了标记上的消息的其他应用或服务。
-   对于启用了 NFC 的 NFP 提供程序，在连接到 NFC 论坛设备（而不是 NFC 论坛标记）时，驱动程序不能传输 "\*： WriteTag" 发布。
-   当驱动程序检测到一个或多个 "\*： WriteTag" 发布已启用时，当驱动程序检测到一个可供至少一个负载使用的可用空间时，驱动程序必须只向标记写入一个有效负载。 o 如果有多个发布处于活动状态并且小小，足以写入标记，则最近创建或启用的 "\*： WriteTag" 发布必须是写入的发布。
-   如果在驱动程序当前与具有足够可用空间的可写标记通信的情况下创建或启用 "\*： WriteTag" 发布，驱动程序必须将有效负载写入标记，即使驱动程序之前已写入标记也是如此。
-   驱动程序必须以这种方式向标记写入，才能覆盖以前的内容。
-   如果已成功将 "\*： WriteTag" 有效负载写入到标记，则驱动程序必须触发[**IOCTL\_NFP\_获取该发布\_消息处理的\_下一\_消息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)处理。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

