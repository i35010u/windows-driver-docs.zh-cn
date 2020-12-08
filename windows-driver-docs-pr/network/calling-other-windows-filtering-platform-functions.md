---
title: 调用其他 Windows 筛选平台函数
description: 调用其他 Windows 筛选平台函数
keywords:
- Windows 筛选平台标注驱动程序 WDK，调用其他功能
- 标注驱动程序 WDK Windows 筛选平台，调用其他函数
- 筛选引擎 WDK Windows 筛选平台
- 内核模式标注驱动程序 WDK Windows 筛选平台
- 用户模式标注驱动程序 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f1bc792028bf723237afbdbf1bdee6fee36e18a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805241"
---
# <a name="calling-other-windows-filtering-platform-functions"></a>调用其他 Windows 筛选平台函数


其他可用于用户模式管理应用程序的 Windows 筛选平台功能也可用于标注驱动程序。 这使标注驱动程序能够执行管理任务，例如向筛选器引擎添加筛选器。 这些函数的用户模式和内核模式版本之间唯一的区别是返回的数据类型。 用户模式函数返回 Win32 错误代码，而内核模式函数返回等效的 NTSTATUS 代码。

大多数 Windows 筛选平台管理函数需要将会话的句柄作为参数从筛选器引擎中打开。 以下主题讨论标注驱动程序如何打开和关闭与筛选器引擎的会话。

[与筛选器引擎建立会话](opening-a-session-to-the-filter-engine.md)

[关闭与筛选器引擎建立的会话](closing-a-session-to-the-filter-engine.md)

有关可从标注驱动程序调用的其他 Windows 筛选平台功能的列表，请参阅 [其他 Windows 筛选平台函数](calling-other-windows-filtering-platform-functions.md)。 有关如何使用这些函数的详细信息，请参阅 Microsoft Windows SDK 中的 [Windows 筛选平台](/windows/win32/fwp/windows-filtering-platform-start-page) 文档。

 

