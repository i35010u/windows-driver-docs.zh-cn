---
title: GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS GUID。
ms.assetid: 8648c75a-dcb3-4723-a2d0-d406d3a073d6
keywords:
- GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS，WDK GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e530dc8b9645ec1ef24e7cd62df37316e830c2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349855"
---
# <a name="guidndistcpoffloadadminsettings"></a>GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS 集 GUID 以设置 NDIS 端口的配置参数的卸载。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 转换到此 GUID [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID NDIS 端口的当前配置设置。 提供任务卸载的任何类型的支持的 NDIS 微型端口驱动程序必须支持此 OID。

WMI 输入的缓冲区包含[NDIS_WMI_SET_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567904)结构，后跟[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)结构。

端口参数的详细信息，请参阅[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)。

