---
title: GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS GUID。
keywords:
- GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS，WDK GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6258a2f93f5428745297f2dbf0c63d4a69a64b3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840903"
---
# <a name="guid_ndis_gen_port_authentication_parameters"></a>GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS 集 GUID 为 NDIS 端口设置端口身份验证参数。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 将此 GUID 转换为 [OID_GEN_PORT_AUTHENTICATION_PARAMETERS](oid-gen-port-authentication-parameters.md) OID，以设置 NDIS 端口的当前身份验证配置。 支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

WMI 输入缓冲区指定后跟 NDIS_PORT_AUTHENTICATION_PARAMETERS 结构的 [NDIS_WMI_SET_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header) 结构。

有关端口参数的详细信息，请参阅 [OID_GEN_PORT_AUTHENTICATION_PARAMETERS](oid-gen-port-authentication-parameters.md)。
