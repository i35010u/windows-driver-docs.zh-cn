---
title: 释放 NDIS 端口
description: 释放 NDIS 端口
ms.assetid: ae7b608d-6105-4fdc-b805-0f0101d7c218
keywords:
- 端口 WDK NDIS，释放
- NDIS 端口 WDK，释放
- 释放 NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d24b13066dc5617ddb86fa1ef2240f613f4dad4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382764"
---
# <a name="freeing-an-ndis-port"></a>释放 NDIS 端口





微型端口驱动程序必须释放所有 NDIS 端口它[分配](allocating-an-ndis-port.md)中的微型端口适配器及其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 它也可以调用释放端口随时[ **NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)，如下所示的两种情况除外。

微型端口驱动程序必须释放所有已分配的端口，在这些情况下：

-   如果您的驱动程序[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数将失败，它必须免费所有分配的端口。
-   如果微型端口适配器将停止，您的驱动程序[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数必须释放所有已分配的端口。

只需调用微型端口驱动程序不能[ **NdisMFreePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)在这些情况下：

-   如果端口是默认端口，NDIS 将其释放自动，因此微型端口驱动程序必须释放它。 如果你尝试释放[的默认端口](default-ndis-port.md)， [ **NdisMFreePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)返回 NDIS\_状态\_无效\_端口错误。
-   如果端口处于活动状态，微型端口驱动程序将需要停用它，然后再调[ **NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)。

## <a name="related-topics"></a>相关主题


[分配 NDIS 端口](allocating-an-ndis-port.md)

[停用 NDIS 端口](deactivating-an-ndis-port.md)

[默认 NDIS 端口](default-ndis-port.md)

 

 






