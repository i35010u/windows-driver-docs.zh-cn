---
title: 扫描仪存储的 WIA 项标志
description: 扫描仪存储的 WIA 项标志
ms.assetid: 493b7c4f-d36a-4447-92a3-34b42ef58397
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 075692e00073bdde61b002a8b8591d52445eb7fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352723"
---
# <a name="wia-item-flags-for-scanner-storage"></a>扫描仪存储的 WIA 项标志


本主题列出了根项目和存储扫描程序项树的子项目的必需和可选的 WIA 项标志。 WIA 项标志及其定义的完整列表，请参阅[ **WIA\_IPA\_项\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff551585)。

### <a name="required-wia-item-flags-for-scanners-storage"></a>所需扫描仪存储标志 WIA 项

WIA 存储扫描程序文件夹项 (WIA\_类别\_文件夹) 需支持以下 WIA 项标志：

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
项是文件夹。 仅对文件夹项需要此标志。

<a href="" id="wiaitemtypestorage"></a>**WiaItemTypeStorage**  
WIA 项是可能包含存储项目的文件夹。 仅对文件夹项需要此标志。

采用 WIA 存储扫描程序文件的项 (WIA\_类别\_已完成\_文件) 所需支持以下 WIA 项标志：

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
项包含可用于传输数据。 此标志还规定**WiaItemTypeImage**标志。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 项可用来将数据传输。 需要此标志，因为平板扫描仪项可用于将数据传输。

### <a name="optional-wia-item-flags-for-scanners-storage"></a>可选 WIA 项标志扫描仪存储

WIA 存储扫描程序文件夹项 (WIA\_类别\_文件夹) 可以选择性地支持以下 WIA 项标志：

<a href="" id="wiaitemtypedeleted"></a>**WiaItemTypeDeleted**  
可以删除某项时，可能会选择性地使用此标志。

采用 WIA 存储扫描程序文件的项 (WIA\_类别\_已完成\_文件) 可以选择性地支持以下 WIA 项标志：

<a href="" id="wiaitemtypeaudio"></a>**WiaItemTypeAudio**  
项是一个音频文件。 如果该文件包含音频数据，仅对项也具有有效，则需要此标志**WiaItemTypeFile**标志设置。

<a href="" id="wiaitemtypedeleted"></a>**WiaItemTypeDeleted**  
可以删除某项时，可能会选择性地使用此标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
映像的产品。 如果该文件仍包含图像数据，仅对于还具有项无效，则需要此标志**WiaItemTypeFile**标志设置。

 

 




