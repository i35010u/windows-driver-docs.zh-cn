---
title: 远程 NDIS 设备控制
description: 远程 NDIS 设备控制
ms.assetid: 52096845-57ee-4da5-95c7-ceae00e8159d
keywords:
- 远程 NDIS WDK 网络、 设备控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be646203a1e9ad77327101d5959c3ef6d1295dbd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388754"
---
# <a name="remote-ndis-device-control"></a>远程 NDIS 设备控制





主机使用远程\_NDIS\_查询\_MSG 和远程\_NDIS\_设置\_MSG 来控制远程 NDIS 设备的操作。 NDIS 对象 ID (OID) 与每个此类消息用于标识设备操作参数或统计信息计数器。 列表[远程 NDIS Oid](remote-ndis-oids.md)分解为两个组：*常规 OID*并*802.3 特定 OID*。 此外，每个组包含的子部分的统计信息 OID 查询。 常规 Oid 所需的任何网络设备。

 

 





