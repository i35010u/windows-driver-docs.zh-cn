---
title: 扫描仪存储的 WIA 项标志
description: 扫描仪存储的 WIA 项标志
ms.assetid: 493b7c4f-d36a-4447-92a3-34b42ef58397
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 306f0f8544e480af983527465037cdd218af467f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191681"
---
# <a name="wia-item-flags-for-scanner-storage"></a>扫描仪存储的 WIA 项标志


本主题列出了存储扫描器项树的根项和子项的必需和可选的 WIA 项标志。 有关 WIA 项标志及其定义的完整列表，请参阅 [**wia \_ IPA \_ item \_ 标志**](./wia-ipa-item-flags.md)。

### <a name="required-wia-item-flags-for-scanners-storage"></a>扫描仪存储所需的 WIA 项标志

\_需要 wia CATEGORY) 文件夹 (wia 类别 \_ 文件夹项才能支持以下 wia 项标志：

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
该项是一个文件夹。 只有文件夹项需要此标志。

<a href="" id="wiaitemtypestorage"></a>**WiaItemTypeStorage**  
WIA 项是可以包含存储项的文件夹。 只有文件夹项需要此标志。

Wia 类别 (wia \_ 类别完成的文件项 \_ \_ 需要支持以下 wia 项目标志) ：

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
项包含可用于传输的数据。 **WiaItemTypeImage**标志还需要此标志。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 项可用于传输数据。 此标志是必需的，因为平板扫描仪项可用于传输数据。

### <a name="optional-wia-item-flags-for-scanners-storage"></a>扫描仪存储的可选 WIA 项标志

Wia \_ 分类文件夹 (wia 分类 \_ 文件夹项) 可以选择支持以下 WIA 项标志：

<a href="" id="wiaitemtypedeleted"></a>**WiaItemTypeDeleted**  
可以选择在删除项时使用此标志。

Wia 存储扫描器文件项 (WIA \_ 类别 \_ 完成 \_ 文件) 可以选择支持以下 WIA 项标志：

<a href="" id="wiaitemtypeaudio"></a>**WiaItemTypeAudio**  
该项是一个音频文件。 如果文件包含音频数据并且仅对同时设置了 **WiaItemTypeFile** 标志的项有效，则需要此标志。

<a href="" id="wiaitemtypedeleted"></a>**WiaItemTypeDeleted**  
可以选择在删除项时使用此标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
该项是一个图像。 如果文件包含静态图像数据并且仅对还设置了 **WiaItemTypeFile** 标志的项有效，则需要此标志。

 

