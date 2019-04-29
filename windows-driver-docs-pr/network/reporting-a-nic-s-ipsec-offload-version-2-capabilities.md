---
title: 报告 NIC 的 IPsec 卸载版本 2 功能
description: 报告 NIC 的 IPsec 卸载版本 2 功能
ms.assetid: 0ce5c42d-5c0c-4dfa-8a9f-a80c8924201d
keywords:
- IPsecOV2 WDK TCP/IP 传输功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 024c6181c96cd3a775b8e72c3b987303aee4fa3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380879"
---
# <a name="reporting-a-nics-ipsec-offload-version-2-capabilities"></a>报告 NIC 的 IPsec 卸载版本 2 功能

\[IPsec 任务卸载功能已弃用，不应使用。\]




若要指定 IPsec 卸载版本 2 (IPsecOV2) 功能、 NDIS 6.1 和更高版本的微型端口驱动程序指定当前或默认配置中的 nic [ **NDIS\_IPSEC\_卸载\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff565808)结构。 微型端口驱动程序必须包括中的默认 IPsecOV2 配置[ **NDIS\_微型端口\_适配器\_卸载\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)结构。 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数从[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数并传递中信息在 NDIS\_微型端口\_适配器\_卸载\_属性。

微型端口驱动程序必须报告 IPsecOV2 功能中的更改，如果有，请在[ **NDIS\_状态\_任务\_卸载\_当前\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff567424)状态指示。

**请注意**  NDIS NDIS 6.1 和更高版本的驱动程序提供直接的 OID 请求接口。 [直接 OID 请求路径](https://msdn.microsoft.com/library/windows/hardware/ff564736)支持查询或频繁设置的 OID 请求。

 

中的查询响应[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)，NDIS 包括 NDIS\_IPSEC\_卸载\_V2结构中[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599) NDIS 返回中的结构**InformationBuffer**隶属[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。 NDIS 使用微型端口驱动程序提供的信息。

 

 





