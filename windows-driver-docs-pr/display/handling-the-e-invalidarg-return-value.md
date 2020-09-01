---
title: 处理 E_INVALIDARG 返回值
description: 处理 E_INVALIDARG 返回值
ms.assetid: 312b2452-71b3-4fbe-93fb-f4b0e6099c0f
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，E_INVALIDARG 返回值
- E_INVALIDARG 返回值 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c57d24e737187007b570da1853b96fe16883248
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067416"
---
# <a name="handling-the-e_invalidarg-return-value"></a>处理 E \_ INVALIDARG 返回值


通常，用户模式显示驱动程序无法通过返回 E INVALIDARG 来使其所有 [功能](/windows-hardware/drivers/ddi/index) 失败 \_ 。 但是，如果用户模式显示驱动程序 \_ 由于驱动程序中的编程错误或操作系统) 中运行的恶意代码而 (调用 [Microsoft Direct3D 运行时提供的函数](/windows-hardware/drivers/ddi/index) 之一时收到 e INVALIDARG 返回值，则驱动程序必须在 \_ 运行时调用驱动程序的一个函数后，将 E INVALIDARG 返回到 Direct3D 运行时。 否则，用户模式显示驱动程序绝不应将 E \_ INVALIDARG 返回到 Direct3D 运行时。

 

