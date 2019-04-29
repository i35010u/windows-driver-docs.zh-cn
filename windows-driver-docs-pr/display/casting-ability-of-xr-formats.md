---
title: XR 格式的强制转换功能
description: XR 格式的强制转换功能
ms.assetid: 18f9ce6e-df8e-4e57-b86f-338baadcb1b2
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示 XR 格式转换功能
- 扩展的格式 WDK Windows 7 显示、 XR 格式转换功能
- XR 格式转换功能 WDK Windows 7 显示
- 强制转换功能 WDK Windows 7 显示
- 强制转换功能 WDK Windows 7 显示，XR 格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ad2d04e2631b0ac01b549114a8b57c4b9150cff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385684"
---
# <a name="casting-ability-of-xr-formats"></a>XR 格式的强制转换功能


本部分仅适用于 Windows 7 和更高版本的操作系统。

DXGI\_格式\_R10G10B10\_XR\_偏差\_A2\_UNORM 格式属于 DXGI\_格式\_R10G10B10A2\_TYPELESS系列。 因此，应用程序可以强制转换 DXGI\_格式\_R10G10B10\_XR\_偏差\_A2\_UNORM 格式通过该系列的其他成员"视图"的 API 级别概念。 此过程是应用程序呈现到的资源的预期的方法。 具体而言，运行时仅可以查看扫描的 Direct3D 和复制 (通过驱动程序的[ **BltDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff538252)函数) 的资源的格式 XR\_偏置。 因此，若要呈现到的资源，应用程序通常创建的视图格式 DXGI\_格式\_R10G10B10A2\_UNORM。

 

 





