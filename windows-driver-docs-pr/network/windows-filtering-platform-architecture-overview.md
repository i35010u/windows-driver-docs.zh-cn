---
title: Windows 筛选平台体系结构概述
description: Windows 筛选平台体系结构概述
ms.assetid: a20efbe1-f98c-452d-a134-9f65eb6dbc04
keywords:
- Windows 筛选平台体系结构 WDK
- 体系结构 WDK Windows 筛选平台
- 筛选引擎 WDK Windows 筛选平台
- 标注驱动程序 WDK Windows 筛选平台，平台体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 670354bb487bb10cbe558be4b52ce0114cc7d70b
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734159"
---
# <a name="windows-filtering-platform-architecture-overview"></a>Windows 筛选平台体系结构概述


本部分提供 Windows 筛选平台体系结构的简要概述。 有关 Windows 筛选平台体系结构的更详尽的讨论，请参阅 Microsoft Windows SDK 中的 [Windows 筛选平台](/windows/win32/fwp/windows-filtering-platform-start-page) 文档。

下图显示了 Windows 筛选平台的基本体系结构。

![阐释 windows 筛选平台的基本体系结构的关系图](images/wfparch.png)

[筛选器引擎](filter-engine.md)是 Windows 筛选平台的核心。 筛选器引擎对基于 TCP/IP 的网络数据执行所有筛选操作。 TCP/IP 堆栈中的关键点有一些 [筛选层](filtering-layer.md) ，其中的网络数据传递给筛选器引擎进行处理。 如果筛选层筛选条件都为 true，则筛选器引擎会应用该筛选器的操作。

[标注驱动程序](callout-driver.md) 通过向筛选器引擎注册一个或多个 [标注](callout.md) 来提供附加的筛选功能。 筛选器引擎中的[筛选](filter.md)器可以指定筛选器操作的标注。 在这种情况下，筛选器引擎会将网络数据传递到指定的标注进行其他处理。

Windows 筛选平台包含多个内置的标注。 有关其中每个标注的说明，请参阅 [内置标注标识符](./built-in-callout-identifiers.md) 。

