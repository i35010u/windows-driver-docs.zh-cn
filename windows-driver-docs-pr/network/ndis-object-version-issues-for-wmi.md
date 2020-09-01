---
title: WMI 的 NDIS 对象版本问题
description: WMI 的 NDIS 对象版本问题
ms.assetid: 09440de8-125b-4155-9f28-c9f6893071b2
keywords:
- NDIS 版本信息 WDK，WMI 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21d49ead48696e0aa65e635a3f8e2fdeec63e6c8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218007"
---
# <a name="ndis-object-version-issues-for-wmi"></a>WMI 的 NDIS 对象版本问题





本主题介绍了影响 WMI) 支持 (Windows Management Instrumentation 的 NDIS 对象版本问题。

 (MOF) 文件的 WMI 托管对象格式中没有版本控制。 因此，如果相应的 NDIS 结构具有新的修订版本，则已向 MOF 数据对象添加了更多字段。

\_ \_ \_ 为新的 ndis 版本添加更多成员时，NDIS WMI Xxx 标头结构具有新的修订版本。 有关当前 NDIS \_ wmi \_ Xxx \_ 标头结构的列表，请参阅 [NDIS wmi 结构](/windows-hardware/drivers/ddi/ntddndis/index)。

当应用程序访问查询操作的 WMI 信息时，它们必须先检查返回的缓冲区中的版本，然后才能访问任何数据。 对于设置操作，应用程序必须检查 NDIS WMI 输出信息结构中的 **SupportedRevision** 成员， \_ \_ \_ 以确定基础驱动程序已接受的版本。

许多 WMI 对象包含 **MSNdis \_ ObjectHeader** 属性，该属性等效于 [**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header) 结构。 填充**MSNdis \_ ObjectHeader**属性时，请设置 " **NDIS \_ 对象 \_ 标头**" 主题中所述的**类型**和**修订**字段。 若要确保无缝地移植到64位系统，请将 " **大小** " 字段设置为 `0xFFFF` 。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

