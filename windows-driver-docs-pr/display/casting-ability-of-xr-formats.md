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
ms.openlocfilehash: 63084c43d37948b79b798ba8f6609cfc4408d83c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067464"
---
# <a name="casting-ability-of-xr-formats"></a>XR 格式的强制转换功能


本部分仅适用于 Windows 7 及更高版本的操作系统。

DXGI \_ format \_ R10G10B10 \_ XR \_ 偏向 \_ A2 \_ UNORM FORMAT 是 dxgi 格式 R10G10B10A2 无格式系列的成员 \_ \_ \_ 。 因此，应用程序可以 \_ \_ \_ \_ \_ 通过 "视图" 的 API 级别概念将 DXGI 格式 R10G10B10 XR 偏向 A2 \_ UNORM 格式转换为该系列的任何其他成员。 此过程是应用程序呈现到资源的预期方式。 具体而言，Direct3D 运行时只能通过驱动程序的 [**BltDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) 函数) XR 偏向的资源来扫描和复制 (\_ 。 因此，应用程序通常会创建一个格式为 DXGI \_ format \_ R10G10B10A2 UNORM 的视图 \_ 。

 

