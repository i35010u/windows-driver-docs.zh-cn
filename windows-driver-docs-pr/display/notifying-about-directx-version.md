---
title: DirectX 版本通知
description: DirectX 版本通知
ms.assetid: 62c030cf-8eb6-4a94-bd15-730b9219291c
keywords:
- 版本号 WDK DirectX 9。0
- 通知 DirectX 版本 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a77e920b79746aec760ea8ed0e157b742034d8c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840527"
---
# <a name="notifying-about-directx-version"></a>DirectX 版本通知


## <span id="ddk_notifying_about_directx_version_gg"></span><span id="DDK_NOTIFYING_ABOUT_DIRECTX_VERSION_GG"></span>


DirectX 8.0 和更高版本的驱动程序始终会收到有关\_D3DGDI2 中的应用程序使用的 DirectX 运行时版本\_DXVERSION 请求的通知，以便他们能够报告版本的设备功能。 此外，由于应用程序请求具有各种像素格式的图面上的操作，因此还会通知 DirectX 9.0 和更高版本的驱动程序，了解应用程序在\_D3DGDI2 中支持的 DirectX 运行时版本\_GETFORMATCOUNTD3DGDI2\_键入\_IFORMATPROVIDER.GETFORMAT 查询，以便这些驱动程序可以适当地处理版本的操作。

例如，对于 DirectX 运行时版本8.0，DirectX 9.0 或更高版本的驱动程序可以使用 D3DMULTISAMPLE\_类型枚举类型的元素来设置多抽样面的样本数，无论驱动程序是否支持屏蔽取样. 但对于 DirectX 运行时版本9.0，DirectX 9.0 或更高版本的驱动程序不得在 DDSCAPS3\_多级采样\_掩码掩码中设置 D3DMULTISAMPLE\_类型位，除非该驱动程序支持将这些位作为屏蔽。 有关 D3DMULTISAMPLE\_类型的详细信息，请参阅 DirectX SDK 文档。

在 D3DGDI2 中\_键入\_GETFORMATCOUNT 查询，将在[**DD\_GETFORMATCOUNTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatcountdata)结构的**dwReserved**成员中通知 DirectX 9.0 驱动程序的运行时版本。 **DwReserved**成员设置为 DD\_运行时\_版本，这是0X00000900 的 DirectX 9.0。

在 D3DGDI2 中\_键入\_IFORMATPROVIDER.GETFORMAT 查询，将在[**DD\_GETFORMATDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatdata)结构的**format**成员中指定的 DDPIXELFORMAT 结构的**dwSize**成员中通知 DirectX 9.0 驱动程序的运行时版本。 **DwSize**成员还设置为 DD\_运行时\_版本。

 

 





