---
title: 调用其他 Windows 筛选平台函数
description: 调用其他 Windows 筛选平台函数
ms.assetid: dae70b4d-2be2-4db3-86cc-2e7df7d5c034
keywords:
- Windows 筛选平台标注驱动程序 WDK、 调用其他函数
- 标注驱动程序 WDK Windows 筛选平台，调用其他函数
- 筛选器引擎 WDK Windows 筛选平台
- 内核模式标注驱动程序 WDK Windows 筛选平台
- 用户模式下标注驱动程序 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24b8ee9c6b24c69c0d8d0a43a5db24f8ac7a8f79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567208"
---
# <a name="calling-other-windows-filtering-platform-functions"></a>调用其他 Windows 筛选平台函数


许多其他可用于用户模式下管理应用程序的 Windows 筛选平台功能也都可在标注驱动程序。 这使标注驱动程序来执行管理任务，如将筛选器添加到筛选器引擎。 这些函数的用户模式和内核模式版本之间的唯一区别是返回的数据类型。 用户模式下函数返回 Win32 错误代码，而内核模式函数返回等效的 NTSTATUS 代码。

大多数 Windows 筛选平台管理函数作为参数需要筛选器引擎到打开的会话的句柄。 以下主题讨论如何标注驱动程序可以打开和关闭与筛选器引擎的会话。

[打开与筛选器引擎的会话。](opening-a-session-to-the-filter-engine.md)

[关闭与筛选器引擎的会话。](closing-a-session-to-the-filter-engine.md)

可以从标注驱动程序调用的其他 Windows 筛选平台函数的列表，请参阅[其他 Windows 筛选平台函数](https://msdn.microsoft.com/library/windows/hardware/ff569961)。 有关如何使用这些函数的详细信息，请参阅[Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK 中的文档。

 

 





