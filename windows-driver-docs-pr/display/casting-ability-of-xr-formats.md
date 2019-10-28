---
title: XR 格式的强制转换功能
description: XR 格式的强制转换功能
ms.assetid: 18f9ce6e-df8e-4e57-b86f-338baadcb1b2
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，XR 格式强制转换功能
- 扩展格式 WDK Windows 7 显示，XR 格式强制转换功能
- XR 格式转换能力 WDK Windows 7 显示
- 转换能力 WDK Windows 7 显示
- 转换能力 WDK Windows 7 显示，XR 格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcc99c2cb7b89bf6984424141122839f0171e4a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839057"
---
# <a name="casting-ability-of-xr-formats"></a>XR 格式的强制转换功能


本部分仅适用于 Windows 7 及更高版本的操作系统。

DXGI\_格式\_R10G10B10\_XR\_偏移\_A2\_UNORM 格式是 DXGI\_格式的成员\_R10G10B10A2\_无格式系列。 因此，应用程序可以通过 API 级别的 "视图" 概念将 DXGI\_格式转换为该系列的任何其他成员，以\_R10G10B10\_XR\_\_偏向。 此过程是应用程序呈现到资源的预期方式。 具体而言，Direct3D 运行时只能扫描并复制（通过驱动程序的[**BltDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数） XR\_偏向格式的资源。 因此，应用程序通常会创建格式为 DXGI\_格式\_R10G10B10A2\_UNORM 的格式。

 

 





