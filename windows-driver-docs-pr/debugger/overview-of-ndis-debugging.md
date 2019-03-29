---
title: NDIS 调试概述
description: NDIS 调试概述
ms.assetid: d15e8a0c-e553-4e0d-84ed-5fdc2026a2d3
keywords:
- NDIS 调试概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ace66602dde1efba95cf1841158a74087deae4ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562080"
---
# <a name="overview-of-ndis-debugging"></a>NDIS 调试概述


用于调试的网络驱动程序的两个主要工具是调试跟踪和网络驱动程序接口规范 (NDIS) 扩展。 调试跟踪的详细信息，请参阅[启用 NDIS 调试跟踪](enabling-ndis-debug-tracing.md)。 调试扩展 NDIS 的详细信息，请参阅[NDIS 扩展](ndis-extensions--ndiskd-dll-.md)，提供了扩展模块 Ndiskd.dll 中找到的扩展命令的完整列表。 扩展模块将出现在 winxp 目录。

另一种工具进行调试的网络驱动程序是常规调试扩展，可用于获取调试信息的集合。 例如，输入[ **！ 堆栈 2 ndis ！**](-stacks.md) 显示以开头的堆栈中的所有线程**ndis ！**。 此信息也可用于调试挂起并停止运行。

此外，还有一个特定于 NDIS 的 bug 检查代码，bug 检查 0x7C (BUGCODE\_NDIS\_驱动程序)。 其参数的完整列表，请参阅[ **Bug 检查 0x7C**](bug-check-0x7c--bugcode-ndis-driver.md)。

用于测试的 NDIS 驱动程序的另一个有用工具是 NDIS 验证程序。 有关详细信息，请查阅 Windows Driver Kit (WDK) 文档中的 NDIS 验证程序主题。

 

 





