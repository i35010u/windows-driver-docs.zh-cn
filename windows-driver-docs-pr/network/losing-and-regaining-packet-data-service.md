---
title: 丢失和重新获取数据包数据服务
description: 丢失和重新获取数据包数据服务
ms.assetid: 1e9d6c34-f7fc-47e9-aa52-409b9e9ff4f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be110007a9fa1cc0dd6854253bf234ec31b50aa4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218079"
---
# <a name="losing-and-regaining-packet-data-service"></a>丢失和重新获取数据包数据服务


下图显示了在不同时间间隔内微型端口驱动程序丢失信号强度和数据包服务时应遵循的过程。 粗体标签是 OID 标识符或事务流控制，而常规文本中的标签是 OID 结构中的重要标志。

![说明数据包数据服务的丢失和放弃信号的示意图](images/wwanregainingpacketdataservice.png)

若要在数据丢失后重新获得包数据服务，请使用以下过程：

1.  微型端口驱动程序将 NDIS \_ WWAN \_ 链接状态发送 \_ 到 MB 服务。

2.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

3.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

4.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

5.  微型端口驱动程序将 NDIS \_ WWAN \_ 注册状态发送 \_ 到 MB 服务。

6.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](./ndis-status-wwan-packet-service.md) 发送到 MB 服务。

7.  微型端口驱动程序将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 发送到 MB 服务。

8.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

 

