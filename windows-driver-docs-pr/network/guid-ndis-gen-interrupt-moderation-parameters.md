---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS GUID。
ms.assetid: f4be78b8-421b-467a-a0a6-b8256b8a4ab3
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS，WDK GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: a94098371cfe0e0a727660da8801c5a4e1046e6d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207565"
---
# <a name="guid_ndis_gen_interrupt_moderation_parameters"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_PARAMETERS 设置 GUID 来设置微型端口适配器的中断裁决配置。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 将此 GUID 转换为 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) OID 以设置当前配置。 所有 NDIS 微型端口驱动程序都必须支持此 OID。

WMI 输入缓冲区包含后跟[NDIS_INTERRUPT_MODERATION_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)结构的[NDIS_WMI_SET_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构。

有关端口参数的详细信息，请参阅 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)。