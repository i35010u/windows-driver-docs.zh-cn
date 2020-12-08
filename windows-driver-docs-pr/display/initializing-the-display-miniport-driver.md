---
title: 初始化显示微型端口驱动程序
description: 初始化显示微型端口驱动程序
keywords:
- 微型端口驱动程序 WDK 显示，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce616ae805b1363540baef6b00ac0330dbf049d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827253"
---
# <a name="initializing-the-display-miniport-driver"></a>初始化显示微型端口驱动程序


操作系统加载了显示微型端口驱动程序后，将执行以下步骤来初始化显示微型端口驱动程序：

1.  操作系统调用显示微型端口驱动程序的 [**DriverEntry**](./driverentry-of-display-miniport-driver.md) 函数。

2.  **DriverEntry** 分配 [**驱动程序 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)结构，并 **Version** \_ \_ 使用 DXGKDDI \_ 接口 \_ 版本和驱动程序初始化 (数据的其余成员（即显示微型端口驱动 \_ \_ 程序实现的函数) ）填充驱动程序初始化数据的版本成员。

3.  **DriverEntry** 调用 [**DxgkInitialize**](/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize) 函数 *Dxgkrnl.sys*) 中加载 Microsoft DirectX 图形内核 (子系统，并向 DirectX 图形内核子系统提供指向显示微型端口驱动程序的其他入口点函数的指针。

4.  **DxgkInitialize** 返回后， **DriverEntry** 将 **DxgkInitialize** 的返回值传播回操作系统。 显示微型端口驱动程序编写器不应对 **DxgkInitialize** 返回的值作出任何假设。

