---
title: 网络驱动程序中的数据包结构
description: 网络驱动程序中的数据包结构
ms.assetid: 01989a73-3f68-431a-ab77-b61f03265c22
keywords:
- 数据包 WDK 网络
- 网络驱动程序 WDK，数据包
- 网络数据 WDK
- 数据 WDK 网络
- 网络数据包结构 WDK
- 网络数据缓冲区 WDK
- 数据缓冲区 WDK 网络
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bc20f1fb93f2991fe2ef7f39af883f98e18939a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843706"
---
# <a name="packet-structures-in-network-drivers"></a>网络驱动程序中的数据包结构





在 NDIS 6.0 和更高版本中，较高层驱动程序会分配[**net\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)和[**NET\_缓冲区列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构来保存网络数据包信息，并将这些结构发送到下一个较低的 NDIS 驱动程序，以便可以将数据发送到网络。 较低级别的驱动程序将分配 NET\_BUFFER 和 NET\_BUFFER\_列表结构来保留接收的数据，并将这些结构传递到相关的更高层驱动程序。 有时，较高层的驱动程序会分配结构，并将其传递到较低的层驱动程序，请求使用较低层的驱动程序将接收的数据复制到提供的缓冲区中。 NDIS 提供了用于分配和操作子结构的函数，这些函数构成 NET\_BUFFER 和 NET\_BUFFER\_列表结构。

有关 NDIS 驱动程序中网络数据缓冲区结构的详细信息，请参阅[NET\_BUFFER](net-buffer-architecture.md)structure。

 

 





