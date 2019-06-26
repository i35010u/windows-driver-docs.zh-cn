---
title: 底片扫描仪的 WIA 项标志
description: 底片扫描仪的 WIA 项标志
ms.assetid: 50aad730-6897-488d-a9de-58ce24738c17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f963b16c2d98554fd5304408fc1de2ac93f73252
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383072"
---
# <a name="wia-item-flags-for-film-scanners"></a>底片扫描仪的 WIA 项标志





本主题列出了所需的 WIA 项标志用于扫描程序电影项和扫描程序电影胶片的子项目 （即，帧）。 WIA 项标志及其定义的完整列表，请参阅[ **WIA\_IPA\_项\_标志**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)。

### <a name="required-wia-item-flags-for-film-scanners"></a>所需 WIA 项标志电影扫描仪

支持以下 WIA 项标志需要 WIA 电影扫描程序项：

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 项是可配置的并遵循一组预定义的配置规则基于[ **WIA\_IPA\_项\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)属性。 需要此标志，因为扫描，扫描程序的一部分电影是可编程的。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 项可用来将数据传输。 需要此标志，因为扫描程序的电影胶片项可用于将数据传输。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
项是一个文件。 此标志所需**WiaItemTypeImage**标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
映像的产品。 需要此标志，因为电影扫描程序报告的图像格式[ **WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)属性值。 （WIA 情况需要，电影胶片扫描程序的所有项都支持至少一种图像格式）。WIA 目前要求 WiaImgFmt\_BMP 和 WiaImgFmt\_MEMORYBMP 图像格式支持。

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
项是文件夹。 若要允许单个帧的枚举子项目的根电影项目需要此标志。 （帧代表单个电影正在扫描的表面上的多个所选的区域。）扫描程序电影子项目 （帧）*不能*将此标志。

 

 




