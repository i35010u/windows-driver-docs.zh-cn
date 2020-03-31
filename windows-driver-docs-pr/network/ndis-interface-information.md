---
title: NDIS 接口信息
description: NDIS 接口信息
ms.assetid: 35187fda-a239-4801-b0be-53fcbee7d24e
keywords:
- 管理信息基本 WDK 网络
- Mib WDK 网络
- NDIS WDK，接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb23de4c820cc1d77763332d9696e730c67546b7
ms.sourcegitcommit: 078e2dfac6c18f65ff923d1e55bff4a23e02a824
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "80400470"
---
# <a name="ndis-interface-information"></a>NDIS 接口信息





用于查询 NDIS 管理信息库（Mib）的标准化接口使过量驱动程序和用户模式应用程序查询有关网络接口的信息变得更加容易。 MIB 客户端调用 NDIS 提供的函数以从基础 NDIS 接口提供程序请求信息。 这会导致 NDIS 发出 OID 请求来检索信息。 为了向客户端提供信息，NDIS 调用了客户端向 NDIS 注册的回调函数。

有关 NDIS 网络接口服务的详细信息，请参阅[Ndis 网络接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

NDIS 提供对管理规范（WMI）的增强支持。 有关 NDIS 6.0 对 WMI 的支持的详细信息，请参阅[对 wmi 的 Ndis 支持](ndis-support-for-wmi.md)。

## <a name="related-topics"></a>相关主题


[**NDIS\_接口\_信息**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-ndis_interface_information)

 

 






