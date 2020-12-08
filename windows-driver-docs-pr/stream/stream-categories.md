---
title: 流类别
description: 流类别
keywords:
- 视频捕获 WDK AVStream，流类别
- 捕获视频 WDK AVStream，流类别
- 标识 pin 主要用途
- 流类别 WDK 视频捕获，关于流类别
- Guid WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49ee71ca5f40661ea68d26e7b1823c23d85b86af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809857"
---
# <a name="stream-categories"></a>流类别


KsProxy 筛选器支持多种类型的流类别。 以下子节中的表描述了不同类型的流类别以及与每种类别关联的数据格式，以及视频捕获微型驱动程序应为每个类别指定的扩展标头大小值。

Stream 类视频捕获微型驱动程序提供流类别和内容信息，以响应 [**SRB \_ 获取 \_ 流 \_ 信息**](./srb-get-stream-info.md) 请求。 微型驱动程序返回有关在 [**HW \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information) 结构中支持的每个流类别的信息。

在 HW \_ 流 \_ 信息结构中，是一个 **StreamFormatsArray** 成员，其中包含微型驱动程序为指定的流类别提供的每个唯一数据格式的条目。 每个 **StreamFormatsArray** 条目都包含流格式信息，其中包括图像特征，如颜色格式、位深度、裁剪和缩放信息。 还包括在 **StreamFormatsArray** 成员中，是指定流类别可用的格式范围。

对于每个视频流类别，在 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) HW [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) \_ 流信息结构中描述流时，将使用相应的 KSDATAFORMAT 和 KSDATARANGE 结构 \_ 。 以下子节的表中列出了与流类别对应的结构。

给定视频捕获流类型的流类别 GUID 和 pin 名称 GUID 通常是相同的。 这些 Guid 分别在 HW 流 **Category** 信息结构的类别和 **名称** 成员中指定 \_ \_ 。 当给定的流类别在一个筛选器上具有多个实例时，这些 Guid 不匹配的唯一情况是。 在这种情况下，类别 Guid 应匹配，但应为每个 pin 分配一个唯一的 pin 名称 GUID。

以下小节包含每个不同视频捕获流类别的相关信息。 描述了流类别 GUID 和 pin 名称 GUID，以及应该用于支持类别的结构。 对于每个类别，还列出了必需的属性集支持。 为了方便起见，还列出了相应的用户模式 DirectShow 类型信息。

 

