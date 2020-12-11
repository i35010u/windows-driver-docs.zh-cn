---
title: 处理 E_INVALIDARG 返回值
description: 处理 E_INVALIDARG 返回值
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，E_INVALIDARG 返回值
- E_INVALIDARG 返回值 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 813c271c852dc48af1df10dc22c4b53a35dddcee
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091058"
---
# <a name="handling-the-e_invalidarg-return-value"></a>处理 E \_ INVALIDARG 返回值


通常，用户模式显示驱动程序无法通过返回 E INVALIDARG 来使其所有功能失败 \_ 。 但是，如果用户模式显示驱动程序 \_ 由于驱动程序中的编程错误或操作系统) 中运行的恶意代码而 (调用 [Microsoft Direct3D 运行时提供的函数](/windows-hardware/drivers/ddi/_display/#functions) 之一时收到 e INVALIDARG 返回值，则驱动程序必须在 \_ 运行时调用驱动程序的一个函数后，将 E INVALIDARG 返回到 Direct3D 运行时。 否则，用户模式显示驱动程序绝不应将 E \_ INVALIDARG 返回到 Direct3D 运行时。

 

