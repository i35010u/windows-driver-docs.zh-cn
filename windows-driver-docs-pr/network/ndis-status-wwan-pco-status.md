---
title: NDIS_STATUS_WWAN_PCO_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PCO_STATUS 通知来告知 MB 服务关于完成的上一个 OID_WWAN_PCO 查询请求。
ms.assetid: E0F70FAE-B7C6-4BE4-B89A-88084463EEA5
keywords:
- NDIS_STATUS_WWAN_PCO_STATUS、 PCO 状态通知、 移动宽带 PCO 状态通知、 MB PCO 状态通知
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c73750e765e8d2837b60de05edd4aa760a073e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341418"
---
# <a name="ndisstatuswwanpcostatus"></a>NDIS_STATUS_WWAN_PCO_STATUS

**NDIS_STATUS_WWAN_PCO_STATUS**调制解调器微型端口驱动程序发送通知来告知调制解调器中当前的协议配置选项 (PCO) 状态的操作系统。 调制解调器微型端口驱动程序将在以下三种方案中发送此通知：

1.  当新 PCO 值到达的激活连接。
2.  如果调制解调器的随时可用的 PCO 值激活或情况下主机桥接连接时。
3.  以响应[OID_WWAN_PCO](oid-wwan-pco.md)从主机的查询请求。

到达新 PCO 值，此通知会导致未经请求并且在网络中的最新 PCO 值发送。 通知将显示与的 NDIS 端口号相对应的已激活的连接 PDN 到。

当激活或从主机桥接连接时，调制解调器应检查其是否具有缓存或不 PCO 值。 如果是这样，它将通知发送到主机，对应于 PDN 主机激活或桥接的 NDIS 端口号。

此通知将用于通知宿主， **OID_WWAN_PCO**查询请求完成后，使用在通知中包含的 PCO 值。 主机需要调制解调器上的端口号与对应 PDN 传递 PCO 值的完整结构。

如果调制解调器支持 PCO 功能，但当主机发送时，从网络接收的任何 PCO 值**OID_WWAN_PCO**查询请求应返回调制解调器**NDIS_STATUS_WWAN_PCO_STATUS**通知包含一个空[WWAN_PCO_VALUE](https://msdn.microsoft.com/library/windows/hardware/45A499CE-2C9A-4070-BEF8-880E7673FA8E)有效负载。 

使用此通知[NDIS_WWAN_PCO_STATUS](https://msdn.microsoft.com/library/windows/hardware/C71187C5-74B6-450A-8461-BB9FDF60DB8D)结构。

> [!NOTE]
> 目前，在 Windows 10 版本 1709年及更高版本，某些调制解调器才能够提供特定 PCO 元素的运算符。 如果调制解调器接收 PCO 数据结构，但不存在适用的运算符特定 PCO 元素，以避免不必要的设备唤醒调制解调器应不播发到 OS 的 PCO 通知。 

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>请参阅

[OID_WWAN_PCO](oid-wwan-pco.md)

[NDIS_WWAN_PCO_STATUS](https://msdn.microsoft.com/library/windows/hardware/C71187C5-74B6-450A-8461-BB9FDF60DB8D)

[WWAN_PCO_VALUE](https://msdn.microsoft.com/library/windows/hardware/45A499CE-2C9A-4070-BEF8-880E7673FA8E)

[MB 协议配置选项 (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)
