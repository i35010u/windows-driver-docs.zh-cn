---
title: 自定义的 Oid 和状态指示
description: 自定义的 Oid 和状态指示
ms.assetid: 675aff2c-8e4a-4a02-8d08-0f59b8fcd4a2
keywords:
- 状态指示 WDK 网络 WMI
- WMI WDK 网络、 状态指示
- Windows Management Instrumentation WDK 网络、 状态指示
- 自定义 Oid WDK 网络
- 自定义状态指示 WDK 网络
- WMI WDK 网络、 OID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d1ea0cf282703841c61492398126fd73b1b7c63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524660"
---
# <a name="customized-oids-and-status-indications"></a>自定义的 Oid 和状态指示





您可以创建一个自定义的 OID NDIS 映射到您创建一个自定义 GUID。 NDIS 注册自定义 GUID 与 WMI 的微型端口驱动程序，以便 WMI 客户端可以查询或设置关联的信息。

若要提供的自定义状态指示，NDIS 微型端口驱动程序必须使用 NDIS\_状态\_媒体\_特定\_指示\_EX 状态指示。 WMI 客户端必须使用随标识的自定义事件的 WMI 事件的数据。 NDIS 不会注册状态指示自定义 Guid。

若要获取的微型端口适配器自定义 Oid 和关联的 WMI Guid，NDIS OID 对发出请求的微型端口驱动程序微型端口驱动程序已完成初始化后。 NDIS 问题[OID\_代\_支持\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569642)查询，以获取微型端口驱动程序支持的 Oid 的列表。 微型端口驱动程序在其响应中包括自定义 Oid 和标准的 Oid。 若要获取与自定义 Oid，NDIS 问题关联的 Guid [OID\_代\_支持\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff569641)无连接的微型端口驱动程序的查询或[OID\_代\_共同\_支持\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff569566)面向连接的微型端口驱动程序的查询。

将查询与 OID\_GEN\_支持\_GUID 或 OID\_常规\_CO\_支持\_GUID 返回的数组[NDIS\_GUID](filling-in-an-ndis-guid-structure.md) NDIS 的结构。 每个 NDIS\_GUID 结构映射到自定义 OID 的自定义 GUID。

若要支持自定义 Oid 和状态指示，必须填写 NDIS\_GUID 结构。 您还必须创建描述 GUID 的托管的对象格式 (MOF) 文件并生成此文件，其微型端口驱动程序。

本部分包括：

[填写 NDIS\_GUID 结构](filling-in-an-ndis-guid-structure.md)

[包括的 MOF 文件](including-a-mof-file.md)

 

 





