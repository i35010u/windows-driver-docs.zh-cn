---
title: GUID_NDIS_GEN_LINK_PARAMETERS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_LINK_PARAMETERS GUID。
ms.assetid: 83895adf-2e66-4820-8037-52eb352b82fc
keywords:
- GUID_NDIS_GEN_LINK_PARAMETERS，WDK GUID_NDIS_GEN_LINK_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b1b23c86fd8f61c775632e8301d885d7fbf569c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382720"
---
# <a name="guidndisgenlinkparameters"></a>GUID_NDIS_GEN_LINK_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_LINK_PARAMETERS 集 GUID 的微型端口适配器设置链接参数。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 转换到此 GUID [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md)要设置的微型端口适配器当前链接参数 OID。 此 OID 是必需的支持 NDIS 6.0 及更高版本的微型端口驱动程序。

WMI 输入的缓冲区指定 NDIS 应设置的数据。 在输入的缓冲区中包含[NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构，后跟[NDIS_LINK_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-parameters)结构。

