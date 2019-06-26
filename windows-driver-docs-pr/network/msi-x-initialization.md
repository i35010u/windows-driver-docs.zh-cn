---
title: MSI-X 初始化
description: MSI-X 初始化
ms.assetid: 64e79ea1-eb6b-4c94-8bad-dd892b712b28
keywords:
- MSI X WDK 连接网络、 初始化
- 消息信号中断 WDK 连接网络、 初始化
- Msi WDK 连接网络、 初始化
- 初始化 MSI X
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0bb4175b9d93655fe85c590a3a5b6c8407d3382
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357786"
---
# <a name="msi-x-initialization"></a>MSI-X 初始化





为支持 MSI X，MSI 初始化需要在其微型端口驱动程序会建立筛选资源要求的函数的预注册阶段。 此函数可以更改每个 MSI X 消息中断关联或删除消息中断资源，如果该驱动程序将注册，以便在基于行的中断[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。

在 NDIS 调用之前发生预注册阶段[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 因为使用基于行的中断，微型端口驱动程序也注册初始化中的微型端口适配器时的 MSI 中断*MiniportInitializeEx*。

本部分包括：

[MSI-X Pre-Registration](msi-x-pre-registration.md)

[MSI X 资源筛选](msi-x-resource-filtering.md)

[注册和取消 MSI 中断](registering-and-deregistering-an-msi-interrupt.md)

 

 





