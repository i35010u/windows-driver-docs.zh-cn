---
title: 使用 PCMCIA_INTERFACE_STANDARD 访问内存
description: 使用 PCMCIA_INTERFACE_STANDARD 界面访问 PCMCIA 属性内存
ms.assetid: cd73a8da-1441-4e95-a955-97235ad091ce
keywords:
- PCMCIA_INTERFACE_STANDARD
- 属性内存 WDK PCMCIA 总线，PCMCIA_INTERFACE_STANDARD 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36cfcee371cbd3af25e215ba4f112a6c904b28ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837736"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-pcmcia_interface_standard-interface"></a>使用 PCMCIA\_接口\_标准接口访问 PCMCIA 属性内存





本部分介绍了驱动程序如何使用 PCMCIA\_接口\_标准接口访问属性内存。

PCMCIA 接口标准主要用于内存卡驱动程序和文件系统。

驱动程序可以使用 Pcmcia\_修改 PCMCIA\_接口\_标准接口所支持[ **\_内存\_窗口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpcm/nc-ntddpcm-pcmcia_modify_memory_window)接口例程。 PCMCIA\_修改\_内存\_窗口为 PCMCIA 内存卡设置内存窗口的属性。 "内存" 窗口由 PCMCIA 总线驱动程序映射。 请注意，此例程不提供永久窗口，它只修改现有窗口的当前设置。 此外，在系统电源状态发生变化时，设置不会永久保存。

有关详细信息，请参阅[PCMCIA\_接口\_用于内存卡的标准接口](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/pcmcia-interface-standard-interface-for-memory-cards)。

 

 





