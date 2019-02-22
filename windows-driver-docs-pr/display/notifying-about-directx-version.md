---
title: 有关 DirectX 版本通知
description: 有关 DirectX 版本通知
ms.assetid: 62c030cf-8eb6-4a94-bd15-730b9219291c
keywords:
- 版本号 WDK DirectX 9.0
- 通知 DirectX 版本 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d911214831a0f03d764a1e20692f20d14f27190
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547914"
---
# <a name="notifying-about-directx-version"></a>有关 DirectX 版本通知


## <span id="ddk_notifying_about_directx_version_gg"></span><span id="DDK_NOTIFYING_ABOUT_DIRECTX_VERSION_GG"></span>


DirectX 8.0 和更高版本的驱动程序始终通知有关 D3DGDI2 中的应用程序正在使用的 DirectX 运行时版本\_类型\_DXVERSION 中请求，以便它们可以报告设备功能的版本。 此外，应用程序请求具有不同的像素格式的曲面上的操作，因为 DirectX 9.0 和更高版本的驱动程序还得到有关通知的应用程序在 D3DGDI2 中支持的 DirectX 运行时版本\_类型\_GETFORMATCOUNT 和 D3DGDI2\_类型\_GETFORMAT 查询以便这些驱动程序可以适当地处理的版本的操作。

有关示例中，为 8.0 版本的 DirectX 运行时，DirectX 9.0 或更高版本的驱动程序可以设置使用 D3DMULTISAMPLE 元素的多个采样表面的样本数\_类型枚举类型，而不管是否驱动程序支持屏蔽多重采样。 但是，对于 9.0 版的 DirectX 运行时，DirectX 9.0 或更高版本的驱动程序必须不设置 D3DMULTISAMPLE\_DDSCAPS3 中的类型位\_MULTISAMPLE\_掩码屏蔽，除非该驱动程序支持为屏蔽的位。 详细了解 D3DMULTISAMPLE\_类型，请参阅 DirectX SDK 文档。

在 D3DGDI2\_类型\_GETFORMATCOUNT 查询中，驱动程序通知中的运行时版本的 DirectX 9.0 **dwReserved**的成员[ **DD\_GETFORMATCOUNTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551566)结构。 **DwReserved**成员设置为 DD\_运行时\_版本，即为 DirectX 9.0 0x00000900。

在 D3DGDI2\_类型\_GETFORMAT 查询中，驱动程序通知中的运行时版本的 DirectX 9.0 **dwSize** DDPIXELFORMAT 结构中指定的成员**格式**的成员[ **DD\_GETFORMATDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551569)结构。 **DwSize**成员也设置为 DD\_运行时\_版本。

 

 





