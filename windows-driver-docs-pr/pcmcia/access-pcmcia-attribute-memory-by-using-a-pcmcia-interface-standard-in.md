---
title: 通过使用 PCMCIA_INTERFACE_STANDARD 访问内存
description: 通过使用 PCMCIA_INTERFACE_STANDARD 接口访问 PCMCIA 属性内存
ms.assetid: cd73a8da-1441-4e95-a955-97235ad091ce
keywords:
- PCMCIA_INTERFACE_STANDARD
- 属性内存 WDK PCMCIA 总线，PCMCIA_INTERFACE_STANDARD 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d0e10d5cdbf5ad0db7c7450016ee16ebf2fcf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353534"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-pcmciainterfacestandard-interface"></a>通过使用 PCMCIA 访问 PCMCIA 属性内存\_接口\_标准接口





本部分介绍如何将驱动程序可以使用 PCMCIA\_接口\_访问属性内存的标准接口。

标准的 PCMCIA 接口主要用于内存卡驱动程序和文件系统。

驱动程序可以使用[ **PCMCIA\_修改\_内存\_窗口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpcm/nc-ntddpcm-pcmcia_modify_memory_window)接口 PCMCIA 所支持例程\_接口\_标准接口。 PCMCIA\_修改\_内存\_窗口设置 PCMCIA 内存卡的内存窗口的特性。 通过 PCMCIA 总线驱动程序映射内存窗口。 请注意，此例程不提供永久窗口，它只修改一个现有的窗口的当前设置。 此外，设置并不是永久通过系统电源状态的更改。

有关详细信息，请参阅[PCMCIA\_界面\_标准接口，用于内存卡](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/pcmcia-interface-standard-interface-for-memory-cards)。

 

 





