---
title: 重新处理操作
description: 重新处理操作
ms.assetid: fdf1228b-ccae-4079-b968-b4dbb5665555
keywords:
- 网络 WDK，参加操作数据
- 数据 WDK 网络，参加操作
- 数据包 WDK 网络，参加操作
- 参加操作 WDK 网络
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- 分配 MDLs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c627ac99fb778ce7a3346f899804f5ce77c9b306
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362932"
---
# <a name="retreat-operations"></a>重新处理操作





参加操作可以增加使用的数据中的空间大小[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构或在所有 NET\_缓冲区中结构[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

NDIS 提供了以下撤回函数：

[**NdisRetreatNetBufferDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff564527)

[**NdisRetreatNetBufferListDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff564529)

参加操作有时可以分配与网络相关联的 MDLs\_缓冲区结构。 若要提供用于分配 MDLs 的机制，驱动程序可以提供的可选入口点[ **NetAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff568326)函数。 如果入口点是**NULL**，NDIS 使用默认方法来分配 MDLs。 在中，必须释放 MDLs [ **NetFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff568348)提供的机制，用于分配 MDL 倒数函数。

若要获取的新**DataLength**，NDIS 添加的驱动程序指定*DataOffsetDelta*与当前**DataLength** 。 如果的大小*未使用的数据空间*大于*DataOffsetDelta*，参加操作减小**DataOffset** 。 在这种情况下，新**DataOffset**是当前**DataOffset**减去*DataOffsetDelta* 。

如果*DataOffsetDelta*大于**DataOffset**，参加操作分配新的数据空间。 在这种情况下，调整 NDIS **DataOffset**相应地。

对于发送操作，NDIS 分配内存，如果没有足够*未使用的数据空间*来满足撤回请求。 如果没有内存分配是必需的只需调整 NDIS **DataOffset**并**DataLength** 。 为了提高性能，驱动程序应以容纳所有基础驱动程序的参加操作在发送之前分配足够的总数据大小。

接收返回的情况下，只需调整 NDIS **DataOffset**并**DataLength**相应地。 参加操作反转提前操作所花费的放置期间接收处理。 参加操作完成后*已用数据空间*包含标头数据过程中使用的基础驱动程序接收处理。

 

 





