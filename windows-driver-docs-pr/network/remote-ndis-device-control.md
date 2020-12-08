---
title: 远程 NDIS 设备控制
description: 远程 NDIS 设备控制
keywords:
- 远程 NDIS WDK 网络，设备控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d761e9645ee8bcfe1fb48ffedd898d3da035f65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799338"
---
# <a name="remote-ndis-device-control"></a>远程 NDIS 设备控制





主机使用远程 \_ ndis \_ 查询 \_ 消息和远程 \_ ndis \_ SET \_ msg 来控制远程 ndis 设备的操作。  (OID) 的 NDIS 对象 ID 与每个此类消息一起用于标识设备操作参数或统计信息计数器。 [远程 NDIS oid](remote-ndis-oids.md)的列表分为两组：*常规 oid* 和 *802.3 特定 oid*。 此外，每个组都包含一个 "统计信息 OID" 查询子节。 所有网络设备都需要常规 Oid。

 

 





