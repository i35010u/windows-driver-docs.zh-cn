---
title: 通过使用 PCMCIA_INTERFACE_STANDARD 访问内存
description: 通过使用 PCMCIA_INTERFACE_STANDARD 接口访问 PCMCIA 属性内存
ms.assetid: cd73a8da-1441-4e95-a955-97235ad091ce
keywords:
- PCMCIA_INTERFACE_STANDARD
- 属性内存 WDK PCMCIA 总线，PCMCIA_INTERFACE_STANDARD 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d73cdc5d353ad04f4930ec3b70660ec6f9b4e42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391577"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-pcmciainterfacestandard-interface"></a>通过使用 PCMCIA 访问 PCMCIA 属性内存\_接口\_标准接口





本部分介绍如何将驱动程序可以使用 PCMCIA\_接口\_访问属性内存的标准接口。

标准的 PCMCIA 接口主要用于内存卡驱动程序和文件系统。

驱动程序可以使用[ **PCMCIA\_修改\_内存\_窗口**](https://msdn.microsoft.com/library/windows/hardware/ff537610)接口 PCMCIA 所支持例程\_接口\_标准接口。 PCMCIA\_修改\_内存\_窗口设置 PCMCIA 内存卡的内存窗口的特性。 通过 PCMCIA 总线驱动程序映射内存窗口。 请注意，此例程不提供永久窗口，它只修改一个现有的窗口的当前设置。 此外，设置并不是永久通过系统电源状态的更改。

有关详细信息，请参阅[PCMCIA\_界面\_标准接口，用于内存卡](https://msdn.microsoft.com/library/windows/hardware/ff537606)。

 

 





