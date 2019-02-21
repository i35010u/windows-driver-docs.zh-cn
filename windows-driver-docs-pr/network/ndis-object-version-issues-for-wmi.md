---
title: WMI 的 NDIS 对象版本问题
description: WMI 的 NDIS 对象版本问题
ms.assetid: 09440de8-125b-4155-9f28-c9f6893071b2
keywords:
- 支持 NDIS 版本信息 WDK WMI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d80847483368d2f86f2b76e88b5b92ac8a42f744
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547106"
---
# <a name="ndis-object-version-issues-for-wmi"></a>WMI 的 NDIS 对象版本问题





本主题介绍会影响 Windows Management Instrumentation (WMI) 支持的 NDIS 对象版本问题。

没有 WMI 托管的对象格式 (MOF) 文件内无版本控制。 因此，如果相应的 NDIS 结构具有新的修订，多个字段具有已添加到 MOF 数据对象。

NDIS\_WMI\_Xxx\_标头结构更多成员添加为新的 NDIS 版本时具有的新修订版本。 有关列表当前的 NDIS\_WMI\_Xxx\_标头结构，请参阅[NDIS WMI 结构](https://msdn.microsoft.com/library/windows/hardware/ff567905)。

时应用程序访问 WMI 信息的查询操作，它们必须在访问任何数据之前检查返回的缓冲区中的版本。 为设置操作中，应用程序必须检查**SupportedRevision**成员在 NDIS\_WMI\_输出\_信息结构，以确定基础驱动程序已接受的版本。

许多 WMI 对象包含**MSNdis\_ObjectHeader**属性，它等效于[ **NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588)结构。 填充时**MSNdis\_ObjectHeader**属性，设置**类型**并**修订**字段中所述**NDIS\_对象\_标头**主题。 若要确保无缝的可移植到 64 位系统，请设置**大小**字段`0xFFFF`。

## <a name="related-topics"></a>相关主题


[NDIS 版本的概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






