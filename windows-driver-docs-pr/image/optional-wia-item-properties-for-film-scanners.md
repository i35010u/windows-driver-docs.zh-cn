---
title: 底片扫描仪的可选 WIA 项属性
description: 底片扫描仪的可选 WIA 项属性
ms.assetid: 6c17deed-7840-4ec0-bc19-d695b3e80c38
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9497354c5cd851f532e78708bdfa6ebca9cdbce4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192615"
---
# <a name="optional-wia-item-properties-for-film-scanners"></a>底片扫描仪的可选 WIA 项属性





WIA 胶片扫描器项可以选择支持以下 WIA 属性：

[**WIA \_ IPA \_ 文件 \_ 扩展名**](./wia-ipa-filename-extension.md)

[**WIA \_ IPA \_ \_ \_ 每通道原始 \_ 位数**](./wia-ipa-raw-bits-per-channel.md)

[**WIA \_ IPS \_ 自动 \_ 反扭曲**](./wia-ips-auto-deskew.md)

[**WIA \_ IP \_ 反扭曲 \_ X**](./wia-ips-deskew-x.md)

[**WIA \_ IP \_ 抗扭反 \_ Y**](./wia-ips-deskew-y.md)

[**WIA \_ IP \_ 灯**](./wia-ips-lamp.md)

[**WIA \_ IPS \_ 灯 \_ 自动 \_ 关闭**](./wia-ips-lamp-auto-off.md)

[**WIA \_ IP \_ 预览 \_ 类型**](./wia-ips-preview-type.md)

[**WIA \_ IP \_ 轮换**](./wia-ips-rotation.md)

[**WIA \_ IPS \_ 分段**](./wia-ips-segmentation.md)

[**WIA \_ IP \_ 显示 \_ 预览 \_ 控件**](./wia-ips-show-preview-control.md)

[**WIA \_ IP \_ 支持 \_ 子 \_ 项目 \_ 创建**](./wia-ips-supports-child-item-creation.md)

[**WIA \_ IP \_ 阈值**](./wia-ips-threshold.md)

[**WIA \_ IP \_ 预热 \_ \_ 时间**](./wia-ips-warm-up-time.md)

[**WIA \_ IP \_ XSCALING**](./wia-ips-xscaling.md)

[**WIA \_ IP \_ YSCALING**](./wia-ips-yscaling.md)

**注意**   如果支持 WiaImgFmt raw 格式，则需要 " [**WIA \_ IPA \_ raw \_ BITS \_ PER \_ 通道**](./wia-ipa-raw-bits-per-channel.md)" 属性 \_ 。 [**WIA \_ IPA \_ format**](./wia-ipa-format.md)属性必须支持 WiaImgFmt \_ BMP 格式。 如果[**wia \_ IPA \_ DEPTH**](./wia-ipa-depth.md)属性设置为 1 BPP，或[**wia \_ IPA \_ DATATYPE**](./wia-ipa-datatype.md)属性设置为 wia 数据阈值，则需要[**wia \_ IPS \_ 阈值**](./wia-ips-threshold.md)属性 \_ \_ 。

 

 

