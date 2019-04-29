---
title: GUID_NDIS_GEN_LINK_PARAMETERS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_LINK_PARAMETERS GUID。
ms.assetid: 83895adf-2e66-4820-8037-52eb352b82fc
keywords:
- GUID_NDIS_GEN_LINK_PARAMETERS，WDK GUID_NDIS_GEN_LINK_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfeb8d1b7df18c08653adfd092260e9a8a286bad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361074"
---
# <a name="guidndisgenlinkparameters"></a>GUID_NDIS_GEN_LINK_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_LINK_PARAMETERS 集 GUID 的微型端口适配器设置链接参数。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 转换到此 GUID [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md)要设置的微型端口适配器当前链接参数 OID。 此 OID 是必需的支持 NDIS 6.0 及更高版本的微型端口驱动程序。

WMI 输入的缓冲区指定 NDIS 应设置的数据。 在输入的缓冲区中包含[NDIS_WMI_SET_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567904)结构，后跟[NDIS_LINK_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569592)结构。

