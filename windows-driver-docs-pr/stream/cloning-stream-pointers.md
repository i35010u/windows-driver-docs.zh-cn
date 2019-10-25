---
title: 克隆流指针
description: 克隆流指针
ms.assetid: bbe01f48-db86-41c9-b7b8-b48a4a295d21
keywords:
- 流指针 WDK AVStream，克隆
- 克隆流指针 WDK AVStream
- 复制流指针 WDK AVStream
- 复制流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fd84284c4695b563d7903106e0ae8b4326b0501
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844734"
---
# <a name="cloning-stream-pointers"></a>克隆流指针





多个流指针可以引用单个帧。 若要复制流指针，请调用[**KsStreamPointerClone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)。

流指针的生成副本称为流指针*克隆*。 克隆是与父级完全相同的新流指针。 最初，克隆引用相同的帧并且具有相同的锁定状态。 创建后，克隆独立于其父流指针。

可以克隆前沿、尾随边缘或当前克隆流指针。

添加克隆流指针会递增该特定帧上的引用计数。 有关引用计数的详细信息，请参阅[流指针简介](introduction-to-stream-pointers.md)。

使用[**KsPinGetFirstCloneStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetfirstclonestreampointer)和[**KsStreamPointerGetNextClone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointergetnextclone)枚举克隆流指针。

克隆将一直存在，直到通过调用[**KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)将其删除。 当微型驱动程序删除克隆时，AVStream 会递减相应帧的引用计数。

请参阅[AVSTREAM DMA 服务](avstream-dma-services.md)，了解如何使用流指针克隆的示例。

 

 




