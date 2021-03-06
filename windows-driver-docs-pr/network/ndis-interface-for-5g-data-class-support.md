---
title: 用于5G 数据类支持的 NDIS 接口
description: 用于5G 数据类支持的 NDIS 接口
keywords:
- 用于5G 数据类支持的 NDIS 接口
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a8d500315478fa1229282fdeb442b1ad86ae6bf1
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250498"
---
# <a name="ndis-interface-for-5g-data-class-support"></a>用于5G 数据类支持的 NDIS 接口

NDIS 支持 NDIS_HEADER 中的修订号。 这允许向 OID 消息添加新成员，NDIS 在 [OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)中使用可选的服务 cap 表。

以下 NDIS Oid 及其数据结构已针对5G 数据类支持进行了更新。

- [OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)
- [OID_WWAN_REGISTER_STATE](oid-wwan-register-state.md)
- [OID_WWAN_PACKET_SERVICE](oid-wwan-packet-service.md)
- [OID_WWAN_SIGNAL_STATE](oid-wwan-signal-state.md)

[MBIMEx 2.0 – 5G NSA 支持](mbimex-2.0-5g-nsa-support.md)中介绍了这些 oid 的等效 MBIM CID 消息。