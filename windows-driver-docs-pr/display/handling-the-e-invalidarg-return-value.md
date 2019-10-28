---
title: 处理 E_INVALIDARG 返回值
description: 处理 E_INVALIDARG 返回值
ms.assetid: 312b2452-71b3-4fbe-93fb-f4b0e6099c0f
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，E_INVALIDARG 返回值
- E_INVALIDARG 返回值 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 646c77a9eb633d7d7bdbaa05b04d19cdd39cebdc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839662"
---
# <a name="handling-the-e_invalidarg-return-value"></a>处理 E\_INVALIDARG 返回值


通常，用户模式显示驱动程序无法通过返回 E\_INVALIDARG 来使其所有[功能](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)失败。 但是，如果用户模式显示驱动程序在调用[Microsoft Direct3D 运行时提供的函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)之一时收到 E\_INVALIDARG 返回值（这是由于驱动程序中的编程错误或操作中运行的恶意代码。系统），则在运行时调用驱动程序的一个函数后，驱动程序必须将 E\_INVALIDARG 返回到 Direct3D 运行时。 否则，用户模式显示驱动程序绝不应将 E\_INVALIDARG 返回到 Direct3D 运行时。

 

 





