---
title: 使用 PCMCIA_INTERFACE_STANDARD 访问内存
description: 使用 PCMCIA_INTERFACE_STANDARD 界面访问 PCMCIA 属性内存
keywords:
- PCMCIA_INTERFACE_STANDARD
- 属性内存 WDK PCMCIA 总线，PCMCIA_INTERFACE_STANDARD 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d8296d778ffa2c7d27616024c7156f1cec6c8b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812523"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-pcmcia_interface_standard-interface"></a>使用 PCMCIA \_ 接口标准界面访问 Pcmcia 属性内存 \_





本部分介绍了驱动程序如何使用 PCMCIA \_ 接口 \_ 标准接口访问属性内存。

PCMCIA 接口标准主要用于内存卡驱动程序和文件系统。

驱动程序可以使用 PCMCIA 接口标准接口支持的 " [**pcmcia \_ 修改 \_ 内存" \_ 窗口**](/windows-hardware/drivers/ddi/ntddpcm/nc-ntddpcm-pcmcia_modify_memory_window) 接口例程 \_ \_ 。 "PCMCIA \_ 修改 \_ 内存 \_ " 窗口设置 pcmcia 内存卡的 "内存" 窗口的属性。 "内存" 窗口由 PCMCIA 总线驱动程序映射。 请注意，此例程不提供永久窗口，它只修改现有窗口的当前设置。 此外，在系统电源状态发生变化时，设置不会永久保存。

有关详细信息，请 [参阅 \_ \_ 内存卡的 PCMCIA 接口标准接口](./pcmcia-interface-standard-interface-for-memory-cards.md)。

 

