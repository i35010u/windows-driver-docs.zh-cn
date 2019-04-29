---
title: 底片扫描仪的 WIA 项标志
description: 底片扫描仪的 WIA 项标志
ms.assetid: 50aad730-6897-488d-a9de-58ce24738c17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a87701e76ad97c6d9ad81ae2f0f790ab110f2809
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363047"
---
# <a name="wia-item-flags-for-film-scanners"></a>底片扫描仪的 WIA 项标志





本主题列出了所需的 WIA 项标志用于扫描程序电影项和扫描程序电影胶片的子项目 （即，帧）。 WIA 项标志及其定义的完整列表，请参阅[ **WIA\_IPA\_项\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff551585)。

### <a name="required-wia-item-flags-for-film-scanners"></a>所需 WIA 项标志电影扫描仪

支持以下 WIA 项标志需要 WIA 电影扫描程序项：

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 项是可配置的并遵循一组预定义的配置规则基于[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性。 需要此标志，因为扫描，扫描程序的一部分电影是可编程的。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 项可用来将数据传输。 需要此标志，因为扫描程序的电影胶片项可用于将数据传输。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
项是一个文件。 此标志所需**WiaItemTypeImage**标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
映像的产品。 需要此标志，因为电影扫描程序报告的图像格式[ **WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)属性值。 （WIA 情况需要，电影胶片扫描程序的所有项都支持至少一种图像格式）。WIA 目前要求 WiaImgFmt\_BMP 和 WiaImgFmt\_MEMORYBMP 图像格式支持。

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
项是文件夹。 若要允许单个帧的枚举子项目的根电影项目需要此标志。 （帧代表单个电影正在扫描的表面上的多个所选的区域。）扫描程序电影子项目 （帧）*不能*将此标志。

 

 




