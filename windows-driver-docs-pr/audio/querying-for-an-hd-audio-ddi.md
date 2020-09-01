---
title: 查询 HD 音频 DDI
description: 查询 HD 音频 DDI
ms.assetid: 972bce92-0ecd-486a-a9a8-fcd434ad12a5
keywords:
- HD 音频，查询
- 高清晰音频 (HD 音频) ，查询
- 查询 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eadfff50d944f0486dd6f8d0c2c487620dd323f3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211335"
---
# <a name="querying-for-an-hd-audio-ddi"></a>查询 HD 音频 DDI


若要获取对带有 HD 音频 DDI 的对象的计数引用，音频或调制解调器编解码器的函数驱动程序将 [**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md) IOCTL 发送到 hd 音频总线驱动程序。

在 Windows Vista 和更高版本中，HD 音频总线驱动程序支持 [**HDAUDIO \_ 总线 \_ 接口**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface) 和 DDI 的 [**HDAUDIO \_ 总线 \_ 接口 \_ V2**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2) 版本。 它不支持 [**HDAUDIO \_ 总线 \_ 接口 \_ BDL**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl) 版本。

在 Windows Server 2003 和 Windows XP 中，可以将 HD 音频总线驱动程序安装为升级。 此总线驱动程序支持两个 DDI 版本。

以下各节介绍了获取对 HDAUDIO \_ 总线 \_ 接口、HDAUDIO \_ 总线接口 \_ \_ V2 和 HDAUDIO \_ 总线 \_ 接口 \_ BDL 版本的引用的过程：

[获取 HDAUDIO \_ 总线 \_ 接口 DDI 对象](obtaining-an-hdaudio-bus-interface-ddi-object.md)

[获取 HDAUDIO \_ BUS \_ 接口 \_ V2 DDI 对象](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)

[获取 HDAUDIO \_ 总线 \_ 接口 \_ BDL DDI 对象](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)

 

