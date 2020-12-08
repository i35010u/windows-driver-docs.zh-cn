---
title: NDEF 协议
description: NDEF 协议
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f6b78db5144b24bd19b808cf61fc0675378e000
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813551"
---
# <a name="ndef-protocol"></a>NDEF 协议


"NDEF" 协议是直接与 NFC 论坛设备交互的一种方法，可通过 NFP 提供商发布/订阅模型进行映射。 使用此协议的任何客户端都需要理解如何编码和解码 NDEF 数据包。 对于发布消息，客户端只需将类型指定为 "NDEF"，因为其余类型信息嵌入在 NDEF 消息本身中。 发布 "NDEF" 类型可让客户端几乎直接传递访问通过 NFC 发送 NDEF 消息。 若要订阅，客户端将指定 "NDEF"，后跟 "：" (冒号) 。

冒号后面是六种记录类型中的一种。

-   空
-   宋体
-   MIME
-   URI
-   wkt
-   未知

提供程序通过遵循此部分中列出的基本提供程序要求以及特定于 NDEF 协议的要求来支持 NDEF。

若要侦听这些 NDEF 消息，客户端需要订阅其中一种受支持的类型，如 "NDEF： wkt"。Sp "。 只要提供程序检测到与类型匹配的 NDEF 消息，就会将整个 NDEF 消息 (仍在 NDEF) 进行编码，并将其传送到订阅客户端。 根据 NDEF 中的 \[ 约定 \] ，要与 NDEF 消息匹配的 "类型" 是 NDEF 消息的第一个 NDEF 记录中指定的类型字段。 同样，若要传输 NDEF 消息，客户端将发布一个完整的 NDEF 消息，并指定 "NDEF" 协议。

还有一种机制，用于订阅所有 NDEF 消息;这是通过订阅 "NDEF" 来完成的。

## <a name="common-ndef-protocol-driver-requirements"></a>常见的 NDEF 协议驱动程序要求


对于所有启用 NFC 的 NFP 提供程序的驱动程序，NDEF 支持都有几个常见的要求。

### <a name="required-actions"></a>必需的措施

-   驱动程序必须根据 NDEF 中指定的 NDEF 消息中第一个 NDEF 记录的 TNF 和 TYPE 字段，将收到的 NDEF 消息与订阅 \[ 匹配 \] 。
-   如果启用了一个或多个 " \* ： WriteTag" 发布，并且驱动程序检测到具有足够可用空间的可写标记，则不能读取标记的现有负载以匹配其他订阅。 这允许标记写入应用抢占可能订阅了标记上的消息的其他应用或服务。
-   对于启用了 NFC 的 NFP 提供程序，连接到 NFC 论坛设备时，驱动程序不能传输 " \* ： WriteTag" 发布 (与 Nfc 论坛标记) 不同。
-   当驱动程序检测到一个或多个 " \* ： WriteTag" 发布已启用时，如果驱动程序检测到一个可供至少一个负载使用的可用空间，则驱动程序必须只向标记写入一个有效负载。 o 如果有多个发布处于活动状态并且小小，足以写入标记，则最近创建或启用的 " \* ： WriteTag" 发布必须是写入的发布。
-   如果在 \* 驱动程序当前与具有足够可用空间的可写标记通信的情况下创建或启用 "： WriteTag" 发布，则驱动程序必须将有效负载写入标记，即使驱动程序之前已写入标记也是如此。
-   驱动程序必须以这种方式向标记写入，才能覆盖以前的内容。
-   如果 \* 已成功将 "： WriteTag" 有效负载写入到标记，则驱动程序必须触发 [**IOCTL \_ NFP \_ 获取 \_ 下一次 \_ 传输的 \_ 消息**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message) 处理 () 该发布中指定的。

## <a name="publications-for-ndefwritetag"></a>"NDEF： WriteTag" 的发布


这是一种特殊类型的发布，允许将一个或多个 NDEF 消息写入 NFC 论坛标记。

### <a name="required-actions"></a>必需的措施

-   \*其他地方所述的常见 "： WriteTag" 要求适用。
-   由于 NFC 论坛标记可能包含多个 NDEF 消息，因此驱动程序必须正确接受 "NDEF： WriteTag" 发布，这种情况下，有多个串联 NDEF 消息作为负载。

## <a name="publications-for-settagreadonly"></a>用于 "SetTagReadOnly" 的发布


此发布允许客户端将标记锁定为只读。 提供程序必须将已设置格式的 NDEF read/write 标记转换为只读。

### <a name="required-actions"></a>必需的措施

-   驱动程序必须首先检查连接的标记是否 NDEF 兼容。
-   如果一个或多个 " \* ：WriteTag "已启用发布，并且驱动程序检测到可写标记，驱动程序必须首先向标记写入，遵循 \* 其他地方所述的常见"： WriteTag "要求，然后将 NDEF 读/写标记转换为只读。

## <a name="empty-ndef-record-ndefempty"></a>空 NDEF 记录： "NDEF： Empty"


此消息中没有类型、ID 或有效负载。 这似乎是 "NDEF： Empty" 类型的订阅在 Windows 客户端的观点上并没有任何意义。

### <a name="required-actions"></a>必需的措施

具有此类型的订阅或发布必须由 "状态无效" 参数的邻近感应提供程序驱动程序拒绝 \_ \_ 。

## <a name="subscriptions-for-all-ndef-types-ndef"></a>所有 NDEF 类型的订阅： "NDEF"


客户端可以订阅所有接收的 NDEF 消息。 通常情况下，如果应用程序知道它感兴趣的消息类型，则会专门订阅该类型。 但是，订阅每个 NDEF 消息有时会很有用。 例如，可以复制和写入重复 NDEF 标记的应用程序可能会发现这非常有用。

### <a name="required-actions"></a>必需的措施

驱动程序必须将 "NDEF" 的订阅与它收到的每个 NDEF 消息匹配。

## <a name="subscriptions-for-external-ndef-rtd-types-ndefext"></a>外部 NDEF RTD 类型的订阅： "NDEF： ext"。


供应商可以使用自定义的可扩展 RTD 命名空间来定义其专用消息的内容。 这允许客户端订阅由 NFC 论坛定义的并由应用或第三方定义的 RTD 外部类型。

泛型示例类型： "NDEF： ext。 &lt;SomeExternalType &gt; "

具体示例类型： "NDEF:ext： mytype"

### <a name="required-actions"></a>必需的措施

驱动程序必须与 "NDEF： ext" 的订阅匹配。 &lt;SomeExternalType &gt; "仅使用收到的 NDEF 消息，其 TNF 字段值为0x04，并且具有 &lt; &gt; 基于 NFC RTD 中指定的等效规则匹配" SOMEEXTERNALTYPE "的类型字段 \[ \] 。

## <a name="subscriptions-for-ndefmime"></a>"NDEF： MIME" 的订阅。


消息可以使用 MIME 命名空间定义消息的内容。

泛型示例类型： "NDEF： MIME。 &lt;SomeMimeType &gt; "

具体示例类型： "NDEF： MIME/jpeg"

### <a name="required-actions"></a>必需的措施

驱动程序必须与 "NDEF： MIME" 的订阅匹配。 &lt;&gt;"SomeMimeType" 仅具有 TNF 字段值为0x02 并且具有与 "SomeMimeType" 匹配的类型字段（ &lt; &gt; 基于 NDEF 中指定的等效规则）的已接收 NDEF \[ 消息 \] 。

## <a name="subscriptions-for-ndefwkt"></a>"NDEF： wkt" 的订阅。


消息可使用 NFC 论坛众所周知的类型命名空间定义消息的内容。

### <a name="required-actions"></a>必需的措施

-   驱动程序必须与 "NDEF： wkt" 的订阅匹配。 &lt;SomeWellKnownType &gt; "仅具有 TNF 字段值为0x01 并且具有与" SomeWellKnownType "匹配的类型字段（ &lt; &gt; 基于在 NDEF 中指定的等效规则）的 NDEF 消息 \[ \] 。
-   驱动程序不得验证已知类型，因此，NFC 论坛可以定义将来的已知类型，而无需更新驱动程序。

## <a name="subscriptions-for-unknown-ndef-type-ndefunknown"></a>未知 NDEF 类型的订阅： "NDEF： Unknown"


这允许客户端订阅非类型化的数据负载。

### <a name="required-actions"></a>必需的措施

驱动程序必须仅将 "NDEF： Unknown" 的订阅与 NDEF 中指定的 TNF 字段值为0x05 的 NDEF 消息匹配 \[ \] 。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)
