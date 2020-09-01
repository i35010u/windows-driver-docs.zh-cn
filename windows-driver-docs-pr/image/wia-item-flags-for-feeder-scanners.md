---
title: 送纸器扫描仪的 WIA 项标志
description: 送纸器扫描仪的 WIA 项标志
ms.assetid: b1256646-be6c-436c-86da-9dff43ef9867
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7c8719f7551798c79f54d726e65678a7dcf2192
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189095"
---
# <a name="wia-item-flags-for-feeder-scanners"></a>送纸器扫描仪的 WIA 项标志





本主题列出了扫描仪进纸器项的必需和可选的 WIA 项标志 (前面和背面页面项) 。 有关 WIA 项标志及其定义的完整列表，请参阅 [**wia \_ IPA \_ item \_ 标志**](./wia-ipa-item-flags.md)。

### <a name="required-wia-item-flags-for-feeder-scanners"></a>对于馈送器扫描仪，必需的 WIA 项标志

需要 WIA 进纸器扫描器项目来支持以下 WIA 项目标志：

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 项是可配置的，并遵循一组基于 [**WIA \_ IPA \_ item \_ CATEGORY**](./wia-ipa-item-category.md) 属性的预定义配置规则。 此标志是必需的，因为扫描仪的文档送纸器是可编程的。

<a href="" id="wiaitemtypetransfer-"></a>**WiaItemTypeTransfer**   
WIA 项可用于传输数据。 此标志是必需的，因为扫描器的进纸器项可用于传输数据。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
该项是一个文件。 **WiaItemTypeImage**标志需要此标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
该项是一个图像。 此标志仅对还设置了 **WiaItemTypeFile** 标志的项有效。 扫描仪的文档送纸器报告 [**WIA \_ IPA \_ 格式**](./wia-ipa-format.md) 属性值的图像格式。  (WIA 要求 *所有* 进纸器扫描器项至少支持一种图像格式。 ) WIA 目前需要将 WiaImgFmt \_ BMP 和 WiaImgFmt \_ MEMORYBMP 视为支持的图像格式。

### <a name="optional-wia-item-flags-for-feeder-scanners"></a>用于馈送器扫描器的可选 WIA 项标志

WIA 进纸器扫描器项可以选择支持以下 WIA 项标志：

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
该项是一个文件夹。 如果自动文档送纸器支持前和后项，则根项需要此标志。 此标志允许将页面的正面和背面枚举为子项。 子项目 *不能* 具有此标志。

 

