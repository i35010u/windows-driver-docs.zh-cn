---
title: 处理 E_INVALIDARG 返回值
description: 处理 E_INVALIDARG 返回值
ms.assetid: 312b2452-71b3-4fbe-93fb-f4b0e6099c0f
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，E_INVALIDARG 返回值
- E_INVALIDARG 返回值 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54da26c839c6d003106f8fa97c1f0aa7ee3fe992
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369844"
---
# <a name="handling-the-einvalidarg-return-value"></a>处理电子\_INVALIDARG 返回值


通常情况下，用户模式显示驱动程序不能故障的任何其[函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)通过返回 E\_INVALIDARG。 但是，如果用户模式显示驱动程序将收到电子\_INVALIDARG 时它将调用一个返回值[Microsoft Direct3D 运行时提供的函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)（由于中的驱动程序或恶意代码的编程错误运行在操作系统中），则驱动程序必须返回 E\_INVALIDARG 回 Direct3D 运行时后，运行时调用的一个驱动程序的函数。 否则，用户模式显示驱动程序应永远不会返回电子\_INVALIDARG 到 Direct3D 运行时。

 

 





