---
title: 克隆流指针
description: 克隆流指针
ms.assetid: bbe01f48-db86-41c9-b7b8-b48a4a295d21
keywords:
- 流指针 WDK AVStream 克隆
- 克隆流指针 WDK AVStream
- 复制流指针 WDK AVStream
- 复制流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e730f4f3330504002c9bdca4f3d79b829eefdb75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386656"
---
# <a name="cloning-stream-pointers"></a>克隆流指针





多个流指针可以引用单个帧。 若要重复的流指针，调用[ **KsStreamPointerClone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)。

流指针的生成副本被称为流指针*克隆*。 克隆是等同于父级的新流指针。 最初，克隆引用同一帧，并具有相同的锁定状态。 创建后，克隆是独立于其父流指针。

可以克隆前沿、 尾随边缘或当前克隆流指针。

添加克隆流指针递增该特定帧的引用计数。 请参阅[简介 Stream 指针](introduction-to-stream-pointers.md)详细了解引用计数。

通过使用枚举克隆流指针[ **KsPinGetFirstCloneStreamPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetfirstclonestreampointer)并[ **KsStreamPointerGetNextClone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointergetnextclone)。

克隆存在，直到通过调用删除[ **KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)。 当微型驱动程序删除克隆时，AVStream 递减引用计数的相应帧。

请参阅[AVStream DMA 服务](avstream-dma-services.md)以举例说明如何使用流指针克隆。

 

 




