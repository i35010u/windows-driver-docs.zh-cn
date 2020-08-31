---
title: 初始化显示微型端口驱动程序
description: 初始化显示微型端口驱动程序
ms.assetid: 505dab48-7c00-4bf4-8433-487360f67b26
keywords:
- 微型端口驱动程序 WDK 显示，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1748e23311034f2b3a72cd9c54663740e50f6840
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064062"
---
# <a name="initializing-the-display-miniport-driver"></a>初始化显示微型端口驱动程序


操作系统加载了显示微型端口驱动程序后，将执行以下步骤来初始化显示微型端口驱动程序：

1.  操作系统调用显示微型端口驱动程序的 [**DriverEntry**](./driverentry-of-display-miniport-driver.md) 函数。

2.  **DriverEntry**分配[**驱动程序 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)结构，并**Version** \_ \_ 使用 DXGKDDI \_ 接口 \_ 版本和驱动程序初始化 (数据的其余成员（即显示微型端口驱动 \_ \_ 程序实现的函数) ）填充驱动程序初始化数据的版本成员。

3.  **DriverEntry** 调用 [**DxgkInitialize**](/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize) 函数 *Dxgkrnl.sys*) 中加载 Microsoft DirectX 图形内核 (子系统，并向 DirectX 图形内核子系统提供指向显示微型端口驱动程序的其他入口点函数的指针。

4.  **DxgkInitialize**返回后， **DriverEntry**将**DxgkInitialize**的返回值传播回操作系统。 显示微型端口驱动程序编写器不应对 **DxgkInitialize** 返回的值作出任何假设。

