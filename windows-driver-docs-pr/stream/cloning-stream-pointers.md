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
ms.openlocfilehash: 6dee974f8d927e30c24ec2f7a283b02f9c2bf528
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372781"
---
# <a name="cloning-stream-pointers"></a>克隆流指针





多个流指针可以引用单个帧。 若要重复的流指针，调用[ **KsStreamPointerClone**](https://msdn.microsoft.com/library/windows/hardware/ff567129)。

流指针的生成副本被称为流指针*克隆*。 克隆是等同于父级的新流指针。 最初，克隆引用同一帧，并具有相同的锁定状态。 创建后，克隆是独立于其父流指针。

可以克隆前沿、 尾随边缘或当前克隆流指针。

添加克隆流指针递增该特定帧的引用计数。 请参阅[简介 Stream 指针](introduction-to-stream-pointers.md)详细了解引用计数。

通过使用枚举克隆流指针[ **KsPinGetFirstCloneStreamPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff563512)并[ **KsStreamPointerGetNextClone**](https://msdn.microsoft.com/library/windows/hardware/ff567133)。

克隆存在，直到通过调用删除[ **KsStreamPointerDelete**](https://msdn.microsoft.com/library/windows/hardware/ff567130)。 当微型驱动程序删除克隆时，AVStream 递减引用计数的相应帧。

请参阅[AVStream DMA 服务](avstream-dma-services.md)以举例说明如何使用流指针克隆。

 

 




