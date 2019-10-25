---
title: WMI 的 NDIS 对象版本问题
description: WMI 的 NDIS 对象版本问题
ms.assetid: 09440de8-125b-4155-9f28-c9f6893071b2
keywords:
- NDIS 版本信息 WDK，WMI 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ff635f89567863fb15c0a6fd2929aee468a56ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844364"
---
# <a name="ndis-object-version-issues-for-wmi"></a>WMI 的 NDIS 对象版本问题





本主题介绍了影响 Windows Management Instrumentation （WMI）支持的 NDIS 对象版本问题。

WMI 托管对象格式（MOF）文件中没有版本控制。 因此，如果相应的 NDIS 结构具有新的修订版本，则已向 MOF 数据对象添加了更多字段。

为新的 NDIS 版本添加更多成员时，NDIS\_WMI\_Xxx\_标头结构具有新的修订版本。 有关当前 NDIS\_WMI\_Xxx\_标头结构的列表，请参阅[NDIS WMI 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)。

当应用程序访问查询操作的 WMI 信息时，它们必须先检查返回的缓冲区中的版本，然后才能访问任何数据。 对于设置操作，应用程序必须检查 NDIS\_WMI\_输出\_信息结构中的**SupportedRevision**成员，以确定基础驱动程序已接受的版本。

许多 WMI 对象包含**MSNdis\_ObjectHeader**属性，该属性等效于[ **\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构。 在填充**MSNdis\_ObjectHeader**属性时，请设置在**NDIS\_对象\_标头**主题中所述的**类型**和**修订**字段。 若要确保能够无缝地移植到64位系统，请将 " **Size** " 字段设置为 `0xFFFF`。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






