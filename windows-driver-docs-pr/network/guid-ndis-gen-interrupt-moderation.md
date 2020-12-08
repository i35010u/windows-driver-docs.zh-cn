---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_INTERRUPT_MODERATION GUID。
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION，WDK GUID_NDIS_GEN_INTERRUPT_MODERATION 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f19d0b18f67d5a8cebb7b652e4c57f3842afc5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825485"
---
# <a name="guid_ndis_gen_interrupt_moderation"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION

WMI 客户端可以使用 GUID_NDIS_GEN_INTERRUPT_MODERATION 方法 GUID 来获取与微型端口适配器的指定端口关联的中断裁决参数。

此 GUID 需要 WMI 方法请求才能返回中断裁决参数。 应 NDIS_WMI_DEFAULT_METHOD_ID WMI 方法标识符，WMI 输入缓冲区应包含 [NDIS_WMI_METHOD_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 的结构。

NDIS 将此 GUID 转换为关联微型端口适配器的 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) 查询请求。 此 OID 对于支持 NDIS 6.0 和更高版本的微型端口驱动程序是必需的。

NDIS 随 GUID 返回的数据缓冲区包含 [NDIS_INTERRUPT_MODERATION_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters) 结构。

有关端口状态的详细信息，请参阅 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)。
