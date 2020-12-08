---
title: MSI-X 初始化
description: MSI-X 初始化
keywords:
- MSI-X WDK 网络，初始化
- 消息-已发出信号中断 WDK 网络，初始化
- Msi WDK 网络，初始化
- 正在初始化 MSI-X
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b15a5b00556965e95c11e75d0f063cffb97b184
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791395"
---
# <a name="msi-x-initialization"></a>MSI-X 初始化





为了支持 MSI X，MSI 初始化需要一个预注册阶段，其中微型端口驱动程序会建立一个用于筛选资源需求的函数。 如果驱动程序将在 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数中注册基于行的中断，此函数可以更改每个 MSI X 消息的中断相关性，或删除消息中断资源。

预注册阶段发生在 NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数之前。 与基于行的中断一样，小型端口驱动程序还会在 *MiniportInitializeEx* 中初始化微型端口适配器时注册 MSI 中断。

本节包括：

[MSI-X 预先注册](msi-x-pre-registration.md)

[MSI-X 资源筛选](msi-x-resource-filtering.md)

[注册和取消注册 MSI 中断](registering-and-deregistering-an-msi-interrupt.md)

 

