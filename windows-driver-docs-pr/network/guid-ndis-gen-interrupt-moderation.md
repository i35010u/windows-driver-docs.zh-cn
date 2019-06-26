---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_INTERRUPT_MODERATION GUID。
ms.assetid: 355e5e4d-61b7-4cc0-8cf7-c95a773e805a
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION，WDK GUID_NDIS_GEN_INTERRUPT_MODERATION 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd2f935ec3884c7ea12642439d645cea6fb02b39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382726"
---
# <a name="guidndisgeninterruptmoderation"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION

WMI 客户端可以使用 GUID_NDIS_GEN_INTERRUPT_MODERATION 方法 GUID 来获取与指定的端口的微型端口适配器相关联的审查参数的中断。

此 GUID 需要 WMI 方法请求返回中断裁决参数。 WMI 方法标识符应 NDIS_WMI_DEFAULT_METHOD_ID，且应包含 WMI 输入的缓冲区[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

NDIS 转换到此 GUID [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)相关联的微型端口适配器的查询请求。 此 OID 是必需的支持 NDIS 6.0 及更高版本的微型端口驱动程序。

NDIS 返回 GUID 的数据缓冲区包含[NDIS_INTERRUPT_MODERATION_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)结构。

有关端口状态的详细信息，请参阅[OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)。

