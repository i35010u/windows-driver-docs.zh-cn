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
ms.openlocfilehash: 1e2a26a6f0fc848fc6a5e8cf82271d0eaba7af62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382641"
---
# <a name="msi-x-initialization"></a>MSI-X 初始化





为支持 MSI X，MSI 初始化需要在其微型端口驱动程序会建立筛选资源要求的函数的预注册阶段。 此函数可以更改每个 MSI X 消息中断关联或删除消息中断资源，如果该驱动程序将注册，以便在基于行的中断[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。

在 NDIS 调用之前发生预注册阶段[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 因为使用基于行的中断，微型端口驱动程序也注册初始化中的微型端口适配器时的 MSI 中断*MiniportInitializeEx*。

本部分包括：

[MSI-X Pre-Registration](msi-x-pre-registration.md)

[MSI X 资源筛选](msi-x-resource-filtering.md)

[注册和取消 MSI 中断](registering-and-deregistering-an-msi-interrupt.md)

 

 





