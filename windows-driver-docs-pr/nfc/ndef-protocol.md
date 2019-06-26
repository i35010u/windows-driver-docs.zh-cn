---
title: NDEF 协议
description: NDEF 协议
ms.assetid: 5AF082EC-70D6-4117-BFCE-B28A8DBAC210
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac16b40f415f4bfd381a47b4133e8396678a1bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383590"
---
# <a name="ndef-protocol"></a>NDEF 协议


"NDEF"协议是一种与直接作为映射 NFP 提供程序发布/订阅模型通过 NFC 论坛设备进行交互。 使用此协议的任何客户端将需要了解如何进行编码和解码 NDEF 数据包。 对于发布的消息，客户端将只是将类型指定为"NDEF"，因为 NDEF 消息本身中嵌入类型信息的其余部分。 发布"NDEF"类型可让客户端几乎直接通过 NFC 发送 NDEF 消息传递的访问权限。 若要订阅，客户端会指定"NDEF"后跟: （冒号）。

后跟冒号是六种记录类型之一。

-   空
-   ext
-   MIME
-   URI
-   wkt
-   Unknown

访问接口支持 NDEF 按照基本提供程序要求，以及在本部分中列出的 NDEF 特定于协议的要求。

若要侦听的这些 NDEF 消息，客户端订阅一种受支持的类型，如"NDEF:wkt。Sp"。 每当提供程序检测到的类型匹配的 NDEF 消息，则将 （仍在 NDEF 中编码） 整个 NDEF 消息传递到订阅客户端。 根据约定\[NDEF\]，type NDEF 消息是 NDEF 消息的第一个 NDEF 记录中指定的类型字段进行匹配。 同样，传输 NDEF 消息，客户端发布完整 NDEF 消息指定"NDEF"的协议。

此外，还有一种机制用于订阅所有 NDEF 消息;通过订阅"NDEF"来完成此操作。

## <a name="common-ndef-protocol-driver-requirements"></a>常见 NDEF 协议驱动程序要求


有几个要求常见 NDEF 上的支持 nfc 的 NFP 的所有提供程序的驱动程序。

### <a name="required-actions"></a>所需的操作

-   该驱动程序必须与匹配订阅基于 TNF 和类型字段中指定 NDEF 消息中的第一个 NDEF 记录收到的 NDEF 消息\[NDEF\]。
-   如果一个或多个"\*: WriteTag"启用发布和驱动程序检测到具有足够可用空间，用于匹配的其他订阅的读取的标记都不能现有负载的可写标记。 这允许用于抢占其他应用或服务可能已订阅消息上标记的标记编写应用。
-   对于支持 NFC 的 NFP 提供程序，驱动程序都不能传输"\*: WriteTag"发布时连接到 NFC 论坛设备 （而不是 NFC 论坛标记）。
-   如果一个或多个"\*: WriteTag"在驱动程序检测到具有足够的空间可用于至少一个有效负载的可写标记时间点启用了发布，驱动程序必须写入负载的一个标记。 o 在的多个发布处于活动状态且足够小，无法写入到一个标记，最近创建或启用"\*: WriteTag"发布必须是一个用。
-   如果"\*: WriteTag"驱动程序发布是创建或启用驱动程序当前正在与具有足够的空间可用于有效负载的可写标记之间的通信时，必须向标记中编写有效负载即使驱动程序以前已写入到标记。
-   该驱动程序必须将写入到覆盖以前的内容的方式的标记。
-   如果"\*: WriteTag"有效负载已成功写入到一个标记，该驱动程序必须触发[ **IOCTL\_NFP\_获取\_下一步\_传输\_消息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message) （如上所示） 处理针对该发布。

## <a name="publications-for-ndefwritetag"></a>发布服务器的"NDEF:WriteTag"


这是发布的一种特殊类型的一个或多个 NDEF 消息时要写入的 NFC 论坛标记。

### <a name="required-actions"></a>所需的操作

-   常见"\*: WriteTag"其他部分所述的要求适用。
-   由于 NFC 论坛标记可以包含多个 NDEF 消息，该驱动程序必须正确地接受"NDEF:WriteTag"碰巧具有多个串联的 NDEF 消息负载的形式的发布。

## <a name="publications-for-settagreadonly"></a>发布服务器的"SetTagReadOnly"


此发布允许客户端锁定标记为只读。 提供程序必须只将已格式化的 NDEF 读/写标记转换为读取中。

### <a name="required-actions"></a>所需的操作

-   驱动程序必须首先检查是否已连接的标记 NDEF 兼容。
-   如果一个或多个"\*:。启用 WriteTag"发布和驱动程序检测到可写的标记，该驱动程序必须将写入到标记首先，遵循常见"\*: WriteTag"要求了其他位置，，然后转换 NDEF 读/写标记为只读。

## <a name="empty-ndef-record-ndefempty"></a>空 NDEF 记录：“NDEF:Empty”


没有任何类型、 ID 或在此消息中的有效负载。 它看起来与"NDEF:Empty"类型的订阅不会使从 Windows 客户端的角度毫无意义。

### <a name="required-actions"></a>所需的操作

使用此类型的发布或订阅必须拒绝邻近提供程序驱动程序状态\_无效\_参数。

## <a name="subscriptions-for-all-ndef-types-ndef"></a>对于所有 NDEF 类型的订阅：“NDEF”


客户端可以订阅所有接收的 NDEF 消息。 通常情况下，如果应用程序知道它关注的消息的类型，它将订阅该类型专门。 但是，它是有时订阅每个 NDEF 消息很有用。 例如，可以复制并写入重复 NDEF 标记的应用程序可能会发现这非常有用。

### <a name="required-actions"></a>所需的操作

该驱动程序必须与匹配"NDEF"并收到每个 NDEF 消息的订阅。

## <a name="subscriptions-for-external-ndef-rtd-types-ndefext"></a>对于外部 NDEF RTD 类型的订阅："NDEF:ext。"


供应商可以使用自定义的可扩展 RTD 命名空间来定义其专用消息的内容。 这允许客户端订阅 RTD 外部类型定义不通过 NFC 论坛，但由应用程序或第三方。

一般示例类型："NDEF:ext.&lt;SomeExternalType&gt;"

具体的示例类型：“NDEF:ext.contoso.com:mytype”

### <a name="required-actions"></a>所需的操作

该驱动程序必须与匹配的订阅"NDEF:ext.&lt;SomeExternalType&gt;"仅与接收的 NDEF 消息 TNF 字段值为 0x04 和具有匹配的类型字段"&lt;SomeExternalType&gt;"基于中指定的等效性规则\[NFC RTD\]。

## <a name="subscriptions-for-ndefmime"></a>"NDEF:MIME。"的订阅


消息可以使用 MIME 命名空间定义消息的内容。

一般示例类型：“NDEF:MIME.&lt;SomeMimeType&gt;”

具体的示例类型：“NDEF:MIME.image/jpeg”

### <a name="required-actions"></a>所需的操作

该驱动程序必须与匹配订阅"NDEF:MIME。&lt;SomeMimeType&gt;"仅与接收的 NDEF 消息 0x02 TNF 字段值和具有匹配的类型字段"&lt;SomeMimeType&gt;"中指定的等效性规则基于\[NDEF\]。

## <a name="subscriptions-for-ndefwkt"></a>"NDEF:wkt。"的订阅


消息可以使用 NFC 论坛熟知类型命名空间定义消息的内容。

### <a name="required-actions"></a>所需的操作

-   该驱动程序必须与匹配订阅"NDEF:wkt。&lt;SomeWellKnownType&gt;"仅与接收的 NDEF 消息 0x01 TNF 字段值和具有匹配的类型字段"&lt;SomeWellKnownType&gt;"基于中指定的等效性规则\[NDEF\]。
-   驱动程序都不能验证已知类型，以便将来的已知类型可通过 NFC 论坛而无需驱动程序更新中定义。

## <a name="subscriptions-for-unknown-ndef-type-ndefunknown"></a>未知的 NDEF 类型的订阅：“NDEF:Unknown”


这允许客户端订阅为非类型化的数据有效负载。

### <a name="required-actions"></a>所需的操作

该驱动程序必须与"NDEF:Unknown"仅使用 NDEF TNF 0x05:sp 中指定的字段值的消息的订阅匹配\[NDEF\]。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

