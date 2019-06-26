---
title: 查询 HD 音频 DDI
description: 查询 HD 音频 DDI
ms.assetid: 972bce92-0ecd-486a-a9a8-fcd434ad12a5
keywords:
- HD Audio 查询
- 高清晰度音频 (HD Audio) 查询
- 查询 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12e61ddceb239d25bdc7d59c1c5f8f82dc81bd66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355281"
---
# <a name="querying-for-an-hd-audio-ddi"></a>查询 HD 音频 DDI


若要获取对具有高清晰度音频 DDI 的对象的计数的引用，音频或调制解调器的编解码器的功能驱动程序发送[ **IRP\_MN\_查询\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)IOCTL HD Audio 总线驱动程序。

HD Audio 总线驱动程序在 Windows Vista 及更高版本，支持[ **HDAUDIO\_总线\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)并[ **HDAUDIO\_总线\_接口\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2) DDI 的版本。 它不支持[ **HDAUDIO\_总线\_接口\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)版本。

HD Audio 总线驱动程序可以安装在 Windows Server 2003 和 Windows XP 中的升级。 此总线驱动程序支持这两个 DDI 版本。

获取对 HDAUDIO 的引用的过程\_总线\_接口，HDAUDIO\_总线\_接口\_V2 和 HDAUDIO\_总线\_接口\_BDL 版本 DDI 的以下各节所述：

[获取 HDAUDIO\_总线\_接口 DDI 对象](obtaining-an-hdaudio-bus-interface-ddi-object.md)

[获取 HDAUDIO\_总线\_接口\_V2 DDI 对象](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)

[获取 HDAUDIO\_总线\_接口\_BDL DDI 对象](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)

 

 




