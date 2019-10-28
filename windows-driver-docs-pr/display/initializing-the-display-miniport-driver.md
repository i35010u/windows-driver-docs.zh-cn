---
title: 初始化显示微型端口驱动程序
description: 初始化显示微型端口驱动程序
ms.assetid: 505dab48-7c00-4bf4-8433-487360f67b26
keywords:
- 微型端口驱动程序 WDK 显示，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82e7ca1f2402614a0d7107d4d9855221e9cd1045
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840374"
---
# <a name="initializing-the-display-miniport-driver"></a>初始化显示微型端口驱动程序


操作系统加载了显示微型端口驱动程序后，将执行以下步骤来初始化显示微型端口驱动程序：

1.  操作系统调用显示微型端口驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)函数。

2.  **DriverEntry** [ **\_数据结构分配驱动程序\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)\_\_，并使用 DXGKDDI\_接口\_版本和驱动程序的剩余成员\_初始化\_数据，其中包含指向显示微型端口驱动程序的其他入口点函数（即显示微型端口驱动程序实现的函数）的指针。

3.  **DriverEntry**调用[**DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)函数以加载 Microsoft directx 图形内核子系统（*Dxgkrnl*），并向 DirectX 图形内核子系统提供指向显示微型端口驱动程序的其他项的指针point 函数。

4.  **DxgkInitialize**返回后， **DriverEntry**将**DxgkInitialize**的返回值传播回操作系统。 显示微型端口驱动程序编写器不应对**DxgkInitialize**返回的值作出任何假设。

 





