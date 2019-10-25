---
title: 丢失和重新获取数据包数据服务
description: 丢失和重新获取数据包数据服务
ms.assetid: 1e9d6c34-f7fc-47e9-aa52-409b9e9ff4f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91c883bed182a18c5150e34c363038c87ed62e47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844140"
---
# <a name="losing-and-regaining-packet-data-service"></a>丢失和重新获取数据包数据服务


下图显示了在不同时间间隔内微型端口驱动程序丢失信号强度和数据包服务时应遵循的过程。 粗体标签是 OID 标识符或事务流控制，而常规文本中的标签是 OID 结构中的重要标志。

![说明数据包数据服务的丢失和放弃信号的示意图](images/wwanregainingpacketdataservice.png)

若要在数据丢失后重新获得包数据服务，请使用以下过程：

1.  微型端口驱动程序将 NDIS\_WWAN\_链接\_状态发送到 MB 服务。

2.  微型端口驱动程序将[**NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)发送到 MB 服务。

3.  微型端口驱动程序将[**NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)发送到 MB 服务。

4.  微型端口驱动程序将[**NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)发送到 MB 服务。

5.  微型端口驱动程序将 NDIS\_WWAN\_注册\_状态发送到 MB 服务。

6.  微型端口驱动程序将[ **\_WWAN\_数据包\_服务的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)发送到 MB 服务。

7.  微型端口驱动程序将[**NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)发送到 MB 服务。

8.  微型端口驱动程序将[**NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)发送到 MB 服务。

 

 





