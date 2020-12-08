---
title: 克隆流指针
description: 克隆流指针
keywords:
- 流指针 WDK AVStream，克隆
- 克隆流指针 WDK AVStream
- 复制流指针 WDK AVStream
- 复制流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18736421576c2f64b248511d3f514e14a190b083
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788181"
---
# <a name="cloning-stream-pointers"></a>克隆流指针





多个流指针可以引用单个帧。 若要复制流指针，请调用 [**KsStreamPointerClone**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)。

流指针的生成副本称为流指针 *克隆*。 克隆是与父级完全相同的新流指针。 最初，克隆引用相同的帧并且具有相同的锁定状态。 创建后，克隆独立于其父流指针。

可以克隆前沿、尾随边缘或当前克隆流指针。

添加克隆流指针会递增该特定帧上的引用计数。 有关引用计数的详细信息，请参阅 [流指针简介](introduction-to-stream-pointers.md) 。

使用 [**KsPinGetFirstCloneStreamPointer**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetfirstclonestreampointer) 和 [**KsStreamPointerGetNextClone**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointergetnextclone)枚举克隆流指针。

克隆将一直存在，直到通过调用 [**KsStreamPointerDelete**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)将其删除。 当微型驱动程序删除克隆时，AVStream 会递减相应帧的引用计数。

请参阅 [AVSTREAM DMA 服务](avstream-dma-services.md) ，了解如何使用流指针克隆的示例。

 

