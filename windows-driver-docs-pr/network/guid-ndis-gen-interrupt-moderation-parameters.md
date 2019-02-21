---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS GUID。
ms.assetid: f4be78b8-421b-467a-a0a6-b8256b8a4ab3
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS，WDK GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cb2583d2fba0b86f7f1d76700657055de19c9cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526550"
---
# <a name="guidndisgeninterruptmoderationparameters"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_PARAMETERS 集 GUID 的微型端口适配器的中断裁决配置设置。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 转换到此 GUID [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) OID 的当前配置设置。 所有的 NDIS 微型端口驱动程序必须支持此 OID。

WMI 输入的缓冲区包含[NDIS_WMI_SET_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567904)结构，后跟[NDIS_INTERRUPT_MODERATION_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff565793)结构。

端口参数的详细信息，请参阅[OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)。

