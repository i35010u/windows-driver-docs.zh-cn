---
title: Windows 筛选平台体系结构概述
description: Windows 筛选平台体系结构概述
ms.assetid: a20efbe1-f98c-452d-a134-9f65eb6dbc04
keywords:
- Windows 筛选平台体系结构 WDK
- 体系结构 WDK Windows 筛选平台
- 筛选器引擎 WDK Windows 筛选平台
- 标注驱动程序 WDK Windows 筛选平台，平台体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e203b72114861da712eafcbd45ca66520221a6e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370579"
---
# <a name="windows-filtering-platform-architecture-overview"></a>Windows 筛选平台体系结构概述


本部分简要概述 Windows 筛选平台体系结构。 Windows 筛选平台体系结构的更深入讨论，请参阅[Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK 中的文档。

下图显示了 Windows 筛选平台的基本体系结构。

![说明 windows 筛选平台的基本体系结构的关系图](images/wfparch.png)

[筛选器引擎](filter-engine.md)是 Windows 筛选平台的核心。 筛选器引擎执行的基于 IP 的网络数据的所有筛选操作。 在 TCP/IP 堆栈中的关键点有[筛选层](filtering-layer.md)个网络数据传递给筛选器引擎进行处理。 如果筛选器筛选层的筛选条件都成立，筛选器引擎会将应用筛选器的操作。

[标注驱动程序](callout-driver.md)通过注册一个或多个提供附加的筛选功能[标注](callout.md)与筛选器引擎。 [筛选器](filter.md)引擎可以在筛选器中指定的筛选器操作的标注。 在这种情况下，筛选器引擎将网络数据传递给其他处理的指定标注。

Windows 筛选平台中包含多个内置的标注。 请参阅[内置标注标识符](https://docs.microsoft.com/windows-hardware/drivers/network/built-in-callout-identifiers)有关的两个标注的说明。

 

 





