---
title: 处理 E_INVALIDARG 返回值
description: 处理 E_INVALIDARG 返回值
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，E_INVALIDARG 返回值
- E_INVALIDARG 返回值 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 590b546f9a93ce1b2c7d3c6b6eb5af6d9d680756
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795007"
---
# <a name="handling-the-e_invalidarg-return-value"></a>处理 E \_ INVALIDARG 返回值


通常，用户模式显示驱动程序无法通过返回 E INVALIDARG 来使其所有 [功能](/windows-hardware/drivers/ddi/index) 失败 \_ 。 但是，如果用户模式显示驱动程序 \_ 由于驱动程序中的编程错误或操作系统) 中运行的恶意代码而 (调用 [Microsoft Direct3D 运行时提供的函数](/windows-hardware/drivers/ddi/index) 之一时收到 e INVALIDARG 返回值，则驱动程序必须在 \_ 运行时调用驱动程序的一个函数后，将 E INVALIDARG 返回到 Direct3D 运行时。 否则，用户模式显示驱动程序绝不应将 E \_ INVALIDARG 返回到 Direct3D 运行时。

 

