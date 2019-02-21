---
title: 指示接收到更高级别驱动程序的网络数据
description: 指示接收到更高级别驱动程序的网络数据
ms.assetid: 27272427-86bc-4fd3-bd2f-12d94273fcd4
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 驱动程序 WDK 的中间，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac4bb97a5a664978159a5cae81afd6292eb7cb7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524923"
---
# <a name="indicating-receive-network-data-to-higher-level-drivers"></a>指示接收到更高级别驱动程序的网络数据





无连接的中间驱动程序指示接收到下一个更高版本的驱动程序的网络数据，方法是调用[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)函数。 面向连接的中间驱动程序指示接收到下一个更高版本的驱动程序的网络数据，方法是调用[ **NdisMCoIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563561)函数。

之前，该值指示接收网络数据，可能将其转换为格式的数据所需的更高级别的驱动程序的驱动程序进程和必要情况下，将相关的数据复制到 MDLs 所带来的中间驱动程序分配[**NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。

 

 





