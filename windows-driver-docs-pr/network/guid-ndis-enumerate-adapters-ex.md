---
title: GUID_NDIS_ENUMERATE_ADAPTERS_EX
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID。
ms.assetid: 46c4c127-a9f6-4555-82d1-3c537fbb7914
keywords:
- GUID_NDIS_ENUMERATE_ADAPTERS_EX，WDK GUID_NDIS_ENUMERATE_ADAPTERS_EX 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2b2de5dc51bfe03cb14ecc173e83dee3f8556f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555006"
---
# <a name="guidndisenumerateadaptersex"></a>GUID_NDIS_ENUMERATE_ADAPTERS_EX

WMI 客户端可以使用 GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID 若要获取的所有计算机上的微型端口适配器枚举。 NDIS 6.0 及更高版本支持此 WMI GUID。 NDIS 跟踪所有已加载的微型端口适配器，因为 NDIS 不会查询此信息的微型端口驱动程序。

WMI 客户端可以使用此 GUID 的设备名称和关联的值中查找**NetLuid**的成员[NDIS_WMI_ENUM_ADAPTER](https://msdn.microsoft.com/library/windows/hardware/ff567899)结构。 WMI 客户端可以使用**NetLuid**适配器在 GUID 的后续请求中的值。

NDIS 返回 GUID 的数据缓冲区包含 NDIS_WMI_ENUM_ADAPTER 结构的数组。

