---
title: 初始化显示微型端口驱动程序
description: 初始化显示微型端口驱动程序
ms.assetid: 505dab48-7c00-4bf4-8433-487360f67b26
keywords:
- 微型端口驱动程序 WDK 显示，请初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c5e62adedbddd59339712fc9d819e5cd8ba97db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350275"
---
# <a name="initializing-the-display-miniport-driver"></a>初始化显示微型端口驱动程序


操作系统加载显示微型端口驱动程序后，执行以下步骤来初始化显示微型端口驱动程序：

1.  操作系统将调用显示微型端口驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556157)函数。

2.  **DriverEntry**分配[**驱动程序\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff556169)结构，并填充**版本**的成员驱动程序\_初始化\_数据与 DXGKDDI\_界面\_版本和驱动程序的其余成员\_初始化\_并指出了显示的数据微型端口驱动程序的其他入口点函数 （即，显示微型端口驱动程序实现的函数）。

3.  **DriverEntry**调用[ **DxgkInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff560824)函数以加载 Microsoft DirectX 图形内核子系统 (*Dxgkrnl.sys*)，以及提供指向显示微型端口驱动程序与 DirectX 图形内核子系统的其他入口点函数。

4.  之后**DxgkInitialize**返回时， **DriverEntry**传播的返回值**DxgkInitialize**返回到操作系统。 显示微型端口驱动程序编写人员应做任何假设的值的**DxgkInitialize**返回。

 





