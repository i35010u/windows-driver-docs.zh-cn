---
title: 缓冲 IEEE 1394 设备的常时等量 DMA 传输
description: 缓冲 IEEE 1394 设备的常时等量 DMA 传输
ms.assetid: 5a08303b-8a4a-4c55-ba48-c4d5ea06157e
keywords:
- 同步 I/O WDK IEEE 1394 总线，缓冲 DMA 传输
- 缓冲区 WDK IEEE 1394 总线
- DMA 传输 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c11deb2df1752d7866417537c7d8ce7e1f1660c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376721"
---
# <a name="buffering-isochronous-dma-transfers-for-ieee-1394-devices"></a>缓冲 IEEE 1394 设备的常时等量 DMA 传输





开始后，同步传输是连续之前暂停。 主控制器必须准备好可以提供的缓冲区，处理事务的需求。 总线驱动程序使用的缓冲区，直到它们用完，附加到的资源句柄并暂停 DMA。 发生这种情况之前，驱动程序将附加其他缓冲区来继续该事务。 ISOCH\_缓冲区描述符有选择性地提供当总线驱动程序已完成一个缓冲区包含一个回调，该驱动程序可以使用此附加额外的缓冲区。 为了获得最佳性能，驱动程序应一次附加多个缓冲区，并仅与最后一个缓冲区，以指示缓冲区提供已用完提供回调。

下图说明了在同步传输中使用的缓冲区。

![说明在同步传输中使用的缓冲区的关系图](images/1394lin.png)

 

 




