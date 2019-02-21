---
title: 原始格式的数据传输
description: 原始格式的数据传输
ms.assetid: 8541b5ce-fd55-47b0-9687-162fb2b4e6aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2066fca36d6ab0d4306a246858186c8d8cdcc99f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555745"
---
# <a name="raw-format-data-transfer"></a>原始格式的数据传输

WIA 支持对数据传输的原始格式。 WIA 传输的原始格式的优点是它支持扫描头的完整功能。

[ **WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)属性可以设置为原始格式的 GUID 符号名称**WiaImgFmt\_RAW**。

若要添加对原始格式的数据传输的支持，扫描程序驱动程序必须提供所有标准[WIA 扫描仪属性](properties-for-wia-scanner-minidrivers.md)。 标准扫描程序属性包括图片范围、 分辨率和每个像素的通道。 您的驱动程序还必须提供的每个通道中的位数[ **WIA\_IPA\_RAW\_位\_每\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff551641)属性。

原始格式是*不*意图是一种文件格式; 它只是一部分的数据传输。 图像处理应用程序将原始数据转换为标准映像的文件格式。 [ **WIA\_IPA\_FILENAME\_扩展**](https://msdn.microsoft.com/library/windows/hardware/ff551549)属性必须设置为空字符串 (含义""，而不**NULL**，作为**NULL**可能对于某些应用程序出现问题)。

扫描行必须是双字节对齐。 扫描行可能需要的末尾处填充，以便其长度是 4 个字节的倍数。 必须打包每个扫描行中的像素。 可以压缩或未压缩图像数据。

**请注意**  对于未压缩的图像数据，数据必须采用已打包的像素格式; 平面扫描应转换为已打包的像素格式的微型驱动程序。

本部分提供有关以下主题的其他信息：

[WIA 的原始数据标头](wia-raw-data-header.md)

[对于原始格式传输属性验证](property-validation-for-raw-format-transfers.md)
