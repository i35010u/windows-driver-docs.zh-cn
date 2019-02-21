---
title: Stream 类别
description: Stream 类别
ms.assetid: dc2af282-4976-42d8-b07b-13b2a6dfb7d5
keywords:
- 视频捕获 WDK AVStream，流类别
- 捕获视频 WDK AVStream，流类别
- 标识 pin 主要用途
- 流类别 WDK 视频捕获，有关流类别
- Guid WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e688b53bf4e63683bb982ba584b2e0a9f8b722fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545117"
---
# <a name="stream-categories"></a>Stream 类别


KsProxy 筛选器支持多种类型的流类别。 以下各小节中的表描述了不同类型的流类别和与每种类型的类别，以及视频捕获微型驱动程序应指定每个类别的扩展标头大小值相关联的数据格式。

Stream 类视频捕获微型驱动程序提供流类别和内容信息，以响应[ **SRB\_获取\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff568173)请求。 微型驱动程序返回有关它在支持每个流类别的信息[ **HW\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff559692)结构。

在 HW\_流\_信息结构**StreamFormatsArray**成员，有一个条目用于微型驱动程序为指定的流类别提供了每个唯一的数据格式。 每个**StreamFormatsArray**条目包含流格式信息，包括映像的特征，例如颜色格式，位深度、 裁剪和缩放信息。 也包含在**StreamFormatsArray**成员是指定的流类别可用的格式的范围。

对于每个视频流存在类别对应[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)并[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)时要使用的结构描述的 HW 中的流\_流\_信息结构。 以下各小节中的表中列出了与流类别相对应的结构。

流类别 GUID 和给定视频捕获流类型的固定名称 GUID 通常是相同的。 中指定这些 Guid**类别**并**名称**HW 成员\_流\_信息结构，分别。 当给定的流类别上筛选器具有多个实例时，这些 Guid 不匹配的唯一情况。 在这种情况下，应匹配类别 Guid，但每个 pin 应分配一个唯一 pin 名称 GUID。

以下各小节包含有关每个不同的视频捕获流类别信息。 用于支持类别的结构以及描述流类别 GUID 和 pin 名称 GUID。 所需的属性集支持还列出每个类别。 为方便起见，也会列出相应的用户模式下 DirectShow 类型信息。

 

 




