---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS GUID。
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS，WDK GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56093f0ec6171e09e9229a8e06f01c313e6f6206
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803719"
---
# <a name="guid_ndis_gen_interrupt_moderation_parameters"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_PARAMETERS 设置 GUID 来设置微型端口适配器的中断裁决配置。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 将此 GUID 转换为 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) OID 以设置当前配置。 所有 NDIS 微型端口驱动程序都必须支持此 OID。

WMI 输入缓冲区包含后跟[NDIS_INTERRUPT_MODERATION_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)结构的[NDIS_WMI_SET_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构。

有关端口参数的详细信息，请参阅 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)。
