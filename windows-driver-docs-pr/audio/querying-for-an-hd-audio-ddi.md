---
title: 查询 HD 音频 DDI
description: 查询 HD 音频 DDI
ms.assetid: 972bce92-0ecd-486a-a9a8-fcd434ad12a5
keywords:
- HD 音频，查询
- 高清晰音频（HD 音频），查询
- 查询 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92f093863cd5b0478a8071acbfe5a16dcc1b35d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832444"
---
# <a name="querying-for-an-hd-audio-ddi"></a>查询 HD 音频 DDI


若要获取对带有 HD 音频 DDI 的对象的计数引用，音频或调制解调器编解码器的函数驱动程序会将[**IRP\_MN\_QUERY\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)IOCTL 发送到 HD 音频总线驱动程序。

在 Windows Vista 和更高版本中，HD 音频总线驱动程序支持[**HDAUDIO\_总线\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)，以及 DDI 的[**HDAUDIO\_总线\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)版本。 它不支持[**HDAUDIO\_总线\_接口\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)版本。

在 Windows Server 2003 和 Windows XP 中，可以将 HD 音频总线驱动程序安装为升级。 此总线驱动程序支持两个 DDI 版本。

用于获取对 HDAUDIO\_总线\_接口、HDAUDIO\_总线\_接口\_V2 和 HDAUDIO\_总线\_接口的引用的过程，请参阅以下各节：

[获取 HDAUDIO\_总线\_接口 DDI 对象](obtaining-an-hdaudio-bus-interface-ddi-object.md)

[获取 HDAUDIO\_总线\_接口\_V2 DDI 对象](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)

[获取 HDAUDIO\_总线\_接口\_BDL DDI 对象](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)

 

 




