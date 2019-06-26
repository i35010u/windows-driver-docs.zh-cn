---
title: 平板扫描仪的 WIA 项标志
description: 平板扫描仪的 WIA 项标志
ms.assetid: bd070e41-47e9-4165-a250-e759b8a214aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f49fe26372de5ddd84ba499dbf50233ebbbc3672
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383062"
---
# <a name="wia-item-flags-for-flatbed-scanners"></a>平板扫描仪的 WIA 项标志





本主题列出了为根项和平板扫描仪项树的子项目的必需和可选的 WIA 项标志。 WIA 项标志及其定义的完整列表，请参阅[ **WIA\_IPA\_项\_标志**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)。

### <a name="required-wia-item-flags-for-flatbed-scanners"></a>所需 WIA 项标志平板扫描仪

支持以下 WIA 项标志需要 WIA 平板扫描仪项：

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 项是可配置的并遵循一组预定义的配置规则基于[ **WIA\_IPA\_项\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)属性。 需要此标志，因为扫描程序的平板部分是可编程。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 项可用来将数据传输。 需要此标志，因为平板扫描仪项可用于将数据传输。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
项是一个文件。 此标志所需**WiaItemTypeImage**标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
映像的产品。 此标志是仅对项还具有的有效**WiaItemTypeFile**标志设置。 需要此标志，因为平板扫描仪报告的图像格式[ **WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)属性值。 支持至少一种图像格式所需 WIA 平板扫描仪的所有项。 WIA 目前要求 WiaImgFmt\_BMP 和 WiaImgFmt\_MEMORYBMP 作为支持的图像格式。

### <a name="optional-wia-item-flags-for-flatbed-scanners"></a>可选 WIA 项标志平板扫描仪

WIA 平板扫描仪项都可以选择支持以下 WIA 项标记：

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
项是文件夹。 如果平板扫描仪项包含子项目，请添加此标志。 （这些项可能包括单个平板辊上的多个所选的区域）。应仅在基项上使用此标志。 子项*不能*将此标志。

 

 




