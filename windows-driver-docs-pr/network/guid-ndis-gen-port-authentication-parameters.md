---
title: GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS GUID。
ms.assetid: a61e972b-0969-4ee8-ad57-cf88beda962d
keywords:
- GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS，WDK GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fdb16228d73a5be5948b8ab7ecc1a6d2dafa65b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382712"
---
# <a name="guidndisgenportauthenticationparameters"></a>GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS 集 GUID 设置 NDIS 端口的端口身份验证参数。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 转换到此 GUID [OID_GEN_PORT_AUTHENTICATION_PARAMETERS](oid-gen-port-authentication-parameters.md) OID NDIS 端口的当前身份验证配置设置。 支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

指定 WMI 输入的缓冲区[NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_set_header)跟 NDIS_PORT_AUTHENTICATION_PARAMETERS 结构的结构。

端口参数的详细信息，请参阅[OID_GEN_PORT_AUTHENTICATION_PARAMETERS](oid-gen-port-authentication-parameters.md)。

