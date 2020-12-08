---
title: 自定义的 OID 和状态指示
description: 自定义的 OID 和状态指示
keywords:
- 状态指示 WDK 网络，WMI
- WMI WDK 网络，状态指示
- Windows Management Instrumentation WDK 网络，状态指示
- 自定义 Oid WDK 网络
- 自定义状态指示 WDK 网络
- WMI WDK 网络，OID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf60504778d70d91525a87f7011810b679044897
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838573"
---
# <a name="customized-oids-and-status-indications"></a>自定义的 OID 和状态指示





你可以创建 NDIS 映射到你创建的自定义 GUID 的自定义 OID。 NDIS 向微型端口驱动程序的 WMI 注册自定义 GUID，以便 WMI 客户端可以查询或设置关联的信息。

为了提供自定义状态指示，NDIS 微型端口驱动程序必须使用 NDIS \_ 状态 \_ 媒体特定的 \_ \_ 指示 \_ ，如状态指示。 WMI 客户端必须使用 WMI 事件随附的数据来标识自定义事件。 NDIS 不会注册自定义 Guid 以获取状态指示。

若要获取微型端口适配器的自定义 Oid 和关联的 WMI Guid，在微型端口驱动程序完成初始化后，NDIS 将向微型端口驱动程序发出 OID 请求。 NDIS 发出 [OID 生成 \_ 支持 \_ 的 \_ 列表](./oid-gen-supported-list.md) 查询，以获取微型端口驱动程序支持的 oid 列表。 小型端口驱动程序在其响应中包含自定义 Oid 和标准 Oid。 为了获取与自定义 Oid 关联的 Guid，NDIS 向无连接微型端口驱动程序或支持面向连接的微型端口驱动程序的[oid \_ gen \_ 共同 \_ 支持的 \_ guid](./oid-gen-co-supported-guids.md)查询发出[oid 生成 \_ \_ 支持 \_ ](./oid-gen-supported-guids.md)的 guid 查询。

对 OID 生成 \_ 支持的 \_ \_ guid 或 oid gen 支持 guid 的查询将 \_ \_ \_ \_ [ndis \_ GUID](filling-in-an-ndis-guid-structure.md) 结构的数组返回到 ndis。 每个 NDIS \_ guid 结构将自定义 GUID 映射到自定义 OID。

若要支持自定义 Oid 和状态指示，必须填写 NDIS \_ GUID 结构。 还必须创建 (MOF) 文件的托管对象格式，该文件描述了 GUID 并使用微型端口驱动程序生成此文件。

本节包括：

[填充 NDIS \_ GUID 结构](filling-in-an-ndis-guid-structure.md)

[包含 MOF 文件](including-a-mof-file.md)

 

