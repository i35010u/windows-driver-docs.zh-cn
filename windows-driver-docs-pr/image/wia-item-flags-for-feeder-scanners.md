---
title: 送纸器扫描仪的 WIA 项标志
description: 送纸器扫描仪的 WIA 项标志
ms.assetid: b1256646-be6c-436c-86da-9dff43ef9867
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b17e3d557c3e233366c39cc2857e53f861c623
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327843"
---
# <a name="wia-item-flags-for-feeder-scanners"></a>送纸器扫描仪的 WIA 项标志





本主题列出了用于扫描程序送纸器项和扫描程序送纸器子项目 （前端和后页面项） 的必需和可选的 WIA 项标志。 WIA 项标志及其定义的完整列表，请参阅[ **WIA\_IPA\_项\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff551585)。

### <a name="required-wia-item-flags-for-feeder-scanners"></a>所需 WIA 项标志送纸器扫描程序

支持以下 WIA 项标志需要 WIA 送纸器扫描程序项：

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 项是可配置的并遵循一组预定义的配置规则基于[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性。 需要此标志，因为扫描程序的文档送纸器是可编程的。

<a href="" id="wiaitemtypetransfer-"></a>**WiaItemTypeTransfer**   
WIA 项可用来将数据传输。 需要此标志，因为扫描程序的送纸器中的项，项树中，可用于将数据传输。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
项是一个文件。 此标志所需**WiaItemTypeImage**标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
映像的产品。 此标志是仅对项还具有的有效**WiaItemTypeFile**标志设置。 扫描程序的文档送纸器报告的图像格式[ **WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)属性值。 (WIA 需要*所有*送纸器扫描程序项支持至少一种图像格式。)WIA 目前要求 WiaImgFmt\_BMP 和 WiaImgFmt\_MEMORYBMP 作为支持的图像格式。

### <a name="optional-wia-item-flags-for-feeder-scanners"></a>可选 WIA 项标志送纸器扫描程序

WIA 送纸器扫描程序项都可以选择支持以下 WIA 项标记：

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
项是文件夹。 如果自动文档送纸器支持前端和后端项目，此标志是必需的根项。 此标志允许枚举的正面和背面页作为子项目。 子项*不能*将此标志。

 

 




