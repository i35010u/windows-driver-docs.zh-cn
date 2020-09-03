---
title: 已检验版本和调试器
description: 已检验版本和调试器
ms.assetid: 851d9b5b-cd1c-4b1e-b3ec-d13645795705
keywords:
- 检查生成 WDK、调试器
- 调试器 WDK 检查生成
- 主机计算机 WDK 检查生成
- 目标计算机 WDK 检查生成
- 空调制解调器电缆 WDK
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6ded8fbe935d242befc02190cf93611fa83ef181
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384483"
---
# <a name="the-checked-build-and-the-debugger"></a>已检验版本和调试器

用于在 Windows 操作系统上调试内核模式驱动程序的典型设置包括两台通过网络、USB 或串行连接方式连接的计算机。 有关设置内核模式调试的信息，请参阅 [Windows 调试](../debugger/index.md)。

*主计算机*是运行调试器的系统。 它应该是稳定的系统，并且应始终运行操作系统的免费版本。

*目标计算机*是在其上运行测试的驱动程序的系统。 它可以运行免费生成或检查的生成。 若要进行更准确的调试，请首选已检查的生成。

主计算机上运行的调试器通过所建立的调试连接来控制目标计算机。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。