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
ms.openlocfilehash: 7e51aec944825b6a289ebfa11529f3739ef66f0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328710"
---
# <a name="querying-for-an-hd-audio-ddi"></a>查询 HD 音频 DDI


若要获取对具有高清晰度音频 DDI 的对象的计数的引用，音频或调制解调器的编解码器的功能驱动程序发送[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)IOCTL HD Audio 总线驱动程序。

HD Audio 总线驱动程序在 Windows Vista 及更高版本，支持[ **HDAUDIO\_总线\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536413)并[ **HDAUDIO\_总线\_接口\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418) DDI 的版本。 它不支持[ **HDAUDIO\_总线\_接口\_BDL** ](https://msdn.microsoft.com/library/windows/hardware/ff536416)版本。

HD Audio 总线驱动程序可以安装在 Windows Server 2003 和 Windows XP 中的升级。 此总线驱动程序支持这两个 DDI 版本。

获取对 HDAUDIO 的引用的过程\_总线\_接口，HDAUDIO\_总线\_接口\_V2 和 HDAUDIO\_总线\_接口\_BDL 版本 DDI 的以下各节所述：

[获取 HDAUDIO\_总线\_接口 DDI 对象](obtaining-an-hdaudio-bus-interface-ddi-object.md)

[获取 HDAUDIO\_总线\_接口\_V2 DDI 对象](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)

[获取 HDAUDIO\_总线\_接口\_BDL DDI 对象](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)

 

 




