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
ms.openlocfilehash: 4560f2c8c8d3ee7bad36137f4b70483d59a86b7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380729"
---
# <a name="tag-writing"></a>标记写入


标记写入指定的类别：常规、 NFC，和全部。 在每个类别的驱动程序将识别某些类型的标记。

这些是允许一条消息写入到任何 NearFieldProximity 标记的特殊发布。 必须覆盖任何现有标记的负载。 追加语义仅为 NFC 定义。 如果客户端想要追加而不是覆盖，它必须构造包含原始 NDEF 消息 NDEF 负载并将其放入"NDEF:WriteTag"发布。 它是预期 （但不是会强制执行） 的零个或一个"\*: WriteTag"发布将在任意给定时刻处于活动状态。

## <a name="general-tag-writing"></a>常规标记写入


标记编写是不是 NFC 已启用的 NFP 提供程序的可选功能。 驱动程序可能会识别以下标记类型为仅发布：

-   “WindowsUri:WriteTag”
-   “WindowsMime:WriteTag”
-   “Windows:WriteTag”

## <a name="nfc-tag-writing"></a>NFC 标记写入


Nfc 的 NFP 提供程序需要的标记写入支持。 必须满足这些要求。

如果邻近技术公布为 NFC，驱动程序必须识别以下标记类型为仅发布：

-   “WindowsUri:WriteTag”
-   “WindowsMime:WriteTag”
-   “Windows:WriteTag”
-   “NDEF:WriteTag”

根据 NFC 论坛规范使用严格 NDEF 编码规则。 例如，NDEF 消息片段都不能写入 （甚至后跟一个有效的 NDEF 消息）。

**请注意**  的 NFC 标记，如果标记不是 NDEF 格式化并为发布一条消息\*。WriteTag，提供程序必须格式化为 NDEF 标记，然后写入负载。

 

## <a name="all-tag-writing"></a>标记的所有写入


如果标记写入在所有受 NFP 提供程序，该驱动程序必须满足所有列出的要求。

### <a name="required-actions"></a>所需的操作

-   驱动程序都不能识别任何"\*: WriteTag"的订阅。
-   如果一个或多个"\*: WriteTag"启用发布和驱动程序检测到具有足够可用空间，用于匹配的其他订阅的读取的标记都不能现有负载的可写标记。 这允许用于抢占其他应用或服务可能已订阅消息上标记的标记编写应用。
-   对于支持 NFC 的 NFP 提供程序，驱动程序都不能传输"\*: WriteTag"发布时连接到 NFC 论坛设备 （而不是 NFC 论坛标记）。
-   如果一个或多个"\*: WriteTag"在驱动程序检测到具有足够的空间可用于至少一个有效负载的可写标记时间点启用了发布，驱动程序必须写入负载的一个标记。 o 在的多个发布处于活动状态且足够小，无法写入到一个标记，最近创建或启用"\*: WriteTag"发布必须是一个用。
-   如果"\*: WriteTag"驱动程序发布是创建或启用驱动程序当前正在与具有足够的空间可用于有效负载的可写标记之间的通信时，必须向标记中编写有效负载即使驱动程序以前已写入到标记。
-   该驱动程序必须写入的方式，会覆盖以前的内容中的标记。
-   如果"\*: WriteTag"有效负载已成功写入到一个标记，该驱动程序必须触发[ **IOCTL\_NFP\_获取\_下一步\_传输\_消息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message) （如上所示） 处理针对该发布。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

