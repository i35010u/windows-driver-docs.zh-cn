---
title: Windows 内核模式 DMA 库
description: Windows 内核模式 DMA 库
ms.assetid: db6cc33a-474b-44a2-bd55-769ff31abae7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 280e06ea682e54e42982fbade9e3b502b7fae22d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835724"
---
# <a name="windows-kernel-mode-dma-library"></a>Windows 内核模式 DMA 库


若要提高性能，设备可能需要以绕过中央处理单元（CPU）的方式直接访问内存。 这种技术称为直接内存访问（DMA）。 Windows 为设备驱动程序开发人员提供 DMA 库。

有关驱动程序 DMA 的详细信息，请参阅[dma](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

有关 DMA 例程的列表，请参阅[直接内存访问（DMA）库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

请注意，DMA 是一种用于在设备和内存之间直接进行通信的技术，与[设备内存访问](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)不同，后者是一组提供的用于读取和写入 i/o 端口和 CPU 注册的宏。

 

 




