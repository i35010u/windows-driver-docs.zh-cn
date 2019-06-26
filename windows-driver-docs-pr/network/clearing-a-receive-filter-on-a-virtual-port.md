---
title: 清除虚拟端口上的接收筛选器
description: 清除虚拟端口上的接收筛选器
ms.assetid: 8431322B-2BF0-4F82-AAAE-0E0396BBC857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a755b2c83118b43cb7e6388c9c1a098f0f7bca8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382771"
---
# <a name="clearing-a-receive-filter-on-a-virtual-port"></a>清除虚拟端口上的接收筛选器


若要清除的 NIC 交换机上的虚拟端口 (VPort) 从接收筛选器，基础驱动程序发出的对象标识符 (OID) 组请求[OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter). **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构。

过量的驱动程序问题之前[OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)请求，它必须初始化[ **NDIS\_接收\_筛选器\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构，并按以下方式设置成员：

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_id。

-   **FilterId**成员必须设置为从早期获取驱动程序的筛选器标识符值[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)方法 OID 请求。 详细了解如何设置接收筛选器，请参阅[上虚拟端口设置接收的筛选器](setting-a-receive-filter-on-a-virtual-port.md)。

基础驱动程序必须清除所有之前释放 VPort 设置 VPort 的筛选器。 基础驱动程序还必须清除所有筛选器，然后关闭其绑定到设置默认 VPort 或从网络适配器分离。

 

 





