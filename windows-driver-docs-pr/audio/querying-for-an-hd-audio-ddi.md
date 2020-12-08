---
title: 查询 HD 音频 DDI
description: 查询 HD 音频 DDI
keywords:
- HD 音频，查询
- 高清晰音频 (HD 音频) ，查询
- 查询 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 904ab72bcfcd32a4bce9269f1ea87aa93887681b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800769"
---
# <a name="querying-for-an-hd-audio-ddi"></a>查询 HD 音频 DDI


若要获取对带有 HD 音频 DDI 的对象的计数引用，音频或调制解调器编解码器的函数驱动程序将 [**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md) IOCTL 发送到 hd 音频总线驱动程序。

在 Windows Vista 和更高版本中，HD 音频总线驱动程序支持 [**HDAUDIO \_ 总线 \_ 接口**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface) 和 DDI 的 [**HDAUDIO \_ 总线 \_ 接口 \_ V2**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2) 版本。 它不支持 [**HDAUDIO \_ 总线 \_ 接口 \_ BDL**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl) 版本。

在 Windows Server 2003 和 Windows XP 中，可以将 HD 音频总线驱动程序安装为升级。 此总线驱动程序支持两个 DDI 版本。

以下各节介绍了获取对 HDAUDIO \_ 总线 \_ 接口、HDAUDIO \_ 总线接口 \_ \_ V2 和 HDAUDIO \_ 总线 \_ 接口 \_ BDL 版本的引用的过程：

[获取 HDAUDIO \_ 总线 \_ 接口 DDI 对象](obtaining-an-hdaudio-bus-interface-ddi-object.md)

[获取 HDAUDIO \_ BUS \_ 接口 \_ V2 DDI 对象](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)

[获取 HDAUDIO \_ 总线 \_ 接口 \_ BDL DDI 对象](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)

 

