---
title: DirectX 版本通知
description: DirectX 版本通知
ms.assetid: 62c030cf-8eb6-4a94-bd15-730b9219291c
keywords:
- 版本号 WDK DirectX 9。0
- 通知 DirectX 版本 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e7fb976e41269c7d169d728142b5c11727c9a23
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066700"
---
# <a name="notifying-about-directx-version"></a>DirectX 版本通知


## <span id="ddk_notifying_about_directx_version_gg"></span><span id="DDK_NOTIFYING_ABOUT_DIRECTX_VERSION_GG"></span>


DirectX 8.0 和更高版本的驱动程序始终会收到有关 D3DGDI2 类型 DXVERSION 请求中的应用程序所使用的 DirectX 运行时版本的通知 \_ \_ ，以便他们能够报告版本的设备功能。 此外，由于应用程序请求具有各种像素格式的图面上的操作，因此还会通知 DirectX 9.0 和更高版本的驱动程序：应用程序在 D3DGDI2 类型 GETFORMATCOUNT 和 D3DGDI2 类型 Iformatprovider.getformat 查询中支持的 DirectX 运行时版本， \_ \_ \_ \_ 使这些驱动程序可以适当地处理版本的操作。

例如，对于 DirectX 运行时版本8.0，DirectX 9.0 或更高版本的驱动程序可以使用 D3DMULTISAMPLE 类型枚举类型的元素设置多抽样图面的样本数， \_ 而不管驱动程序是否支持屏蔽多级。 但是，对于 DirectX 运行时版本9.0，DirectX 9.0 或更高版本的驱动程序不得 \_ 在 DDSCAPS3 采样掩码掩码中设置 D3DMULTISAMPLE 类型位， \_ \_ 除非该驱动程序支持将这些位作为屏蔽。 有关 D3DMULTISAMPLE 类型的详细信息 \_ ，请参阅 DIRECTX SDK 文档。

在 D3DGDI2 \_ 类型 \_ GETFORMATCOUNT 查询中，会向 DirectX 9.0 驱动程序通知[**DD \_ GETFORMATCOUNTDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatcountdata)结构的**dwReserved**成员中的运行时版本。 **DwReserved**成员设置为 DD \_ 运行时 \_ 版本，0x00000900 为 DirectX 9.0。

在 D3DGDI2 \_ 类型 \_ iformatprovider.getformat 查询中，会向 DirectX 9.0 驱动程序通知在[**DD \_ GETFORMATDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatdata)结构的**format**成员中指定的 DDPIXELFORMAT 结构的**dwSize**成员中的运行时版本。 **DwSize**成员还设置为 DD \_ 运行时 \_ 版本。

 

