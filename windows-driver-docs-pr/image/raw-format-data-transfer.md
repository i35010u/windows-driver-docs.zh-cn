---
title: 原始格式数据传输
description: 原始格式数据传输
ms.assetid: 8541b5ce-fd55-47b0-9687-162fb2b4e6aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eb10e98d9800d01d8df9ddaf4741d59e1f841a0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187599"
---
# <a name="raw-format-data-transfer"></a>原始格式数据传输

WIA 支持数据传输的原始格式。 WIA 传输的原始格式的优点是它支持扫描头的全部功能。

[**WIA \_ IPA \_ format**](./wia-ipa-format.md)属性可以设置为 raw 格式的 GUID 符号名称**WiaImgFmt \_ raw**。

若要添加对原始格式数据传输的支持，扫描器驱动程序必须提供所有标准的 [WIA 扫描器属性](properties-for-wia-scanner-minidrivers.md)。 标准扫描程序属性包括图片区、分辨率和每个像素通道数。 你的驱动程序还必须提供 [**WIA \_ IPA \_ RAW \_ bits \_ per \_ 通道**](./wia-ipa-raw-bits-per-channel.md) 属性中每个通道的位数。

原始格式 *不* 应为文件格式;它只是数据传输的一部分。 图像应用程序将原始数据转换为标准的图像处理文件格式。 [**WIA \_ IPA \_ FILENAME \_ EXTENSION**](./wia-ipa-filename-extension.md)属性必须设置为空字符串 (表示 "" 且不为**null**，因为对于某些应用程序) ， **NULL**可能是一个问题。

扫描行必须与 DWORD 对齐。 扫描行可能需要填充到末尾，以便其长度为4个字节的倍数。 必须为每个扫描行内的像素打包。 图像数据可以进行压缩或解压缩。

**注意**   对于未压缩的图像数据，数据必须为打包的像素格式;平面扫描应由小型驱动程序转换为打包像素格式。

本部分提供有关以下主题的其他信息：

[WIA 原始数据标头](wia-raw-data-header.md)

[进行原始格式传输所需的属性验证](property-validation-for-raw-format-transfers.md)