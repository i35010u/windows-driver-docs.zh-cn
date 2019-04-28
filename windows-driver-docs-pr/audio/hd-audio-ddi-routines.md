---
title: HD 音频 DDI 例程
description: HD 音频 DDI 例程
ms.assetid: 2f360031-39bd-457e-8b64-04b37e21a7fe
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 571394fa686deb866253d5d9712f12de92a81d87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333594"
---
# <a name="hd-audio-ddi-routines"></a>HD 音频 DDI 例程


中所述[差异之间 HD 音频 DDI 版本](https://msdn.microsoft.com/library/windows/hardware/ff536258)，HD 音频 DDI 的三个版本存在。 通过定义以下三个 DDI 版本[ **HDAUDIO\_总线\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536413)， [ **HDAUDIO\_总线\_接口\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff536418)，和[ **HDAUDIO\_总线\_接口\_BDL** ](https://msdn.microsoft.com/library/windows/hardware/ff536416)结构。

三个 DDI 版本都可以访问仅在内核模式下。

每个 DDI 版本提供了对 HD Audio 总线控制器管理的硬件资源的访问。 这些资源包括编解码器、 DMA 引擎、 链路带宽、 链接位置寄存器和墙上时钟注册。 HD Audio 总线驱动程序实现 DDI 并公开与其子 DDI。 子级是使用 DDI 来管理已连接到高清晰度音频控制器的硬件编解码器的内核模式函数驱动程序的实例。

若要获得访问权限 DDI 版本，功能驱动程序必须查询 DDI 上下文对象的 HD Audio 总线驱动程序。 有关详细信息，请参阅[获取 HDAUDIO\_总线\_界面 DDI 对象](https://msdn.microsoft.com/library/windows/hardware/ff537589)，[获取 HDAUDIO\_总线\_接口\_V2 DDI 对象](https://msdn.microsoft.com/library/windows/hardware/ff537592)，并[获取 HDAUDIO\_总线\_接口\_BDL DDI 对象](https://msdn.microsoft.com/library/windows/hardware/ff537586)。

在三个 DDI 版本中的每个例程将指向上下文对象的指针作为其第一个调用参数。

HDAUDIO\_总线\_接口结构定义包含以下例程 DDI:

[**AllocateCaptureDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536177)

[**AllocateDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536179)

[**AllocateRenderDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536181)

[**ChangeBandwidthAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff536229)

[**FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)

[**FreeDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536393)

[**GetDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536397)

[**GetLinkPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536398)

[**GetResourceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536399)

[**GetWallClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536401)

[**RegisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff537803)

[**SetDmaEngineState**](https://msdn.microsoft.com/library/windows/hardware/ff537889)

[**TransferCodecVerbs**](https://msdn.microsoft.com/library/windows/hardware/ff538596)

[**UnregisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff538663)

HDAUDIO\_总线\_接口\_V2 结构也可在 Windows Vista 和更高版本的 Windows，它定义包含以下例程 DDI:

[**AllocateCaptureDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536177)

[**AllocateDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536179)

[**AllocateDmaBufferWithNotification**](https://msdn.microsoft.com/library/windows/hardware/ff536180)

[**AllocateRenderDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536181)

[**ChangeBandwidthAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff536229)

[**FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)

[**FreeDmaBufferWithNotification**](https://msdn.microsoft.com/library/windows/hardware/ff536392)

[**FreeDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536393)

[**GetDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536397)

[**GetLinkPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536398)

[**GetResourceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536399)

[**GetWallClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536401)

[**RegisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff537803)

[**RegisterNotificationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff537809)

[**SetDmaEngineState**](https://msdn.microsoft.com/library/windows/hardware/ff537889)

[**TransferCodecVerbs**](https://msdn.microsoft.com/library/windows/hardware/ff538596)

[**UnregisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff538663)

[**UnregisterNotificationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff538669)

HDAUDIO\_总线\_HD 音频 DDI 界面版本支持 Windows Vista 和更高版本的 Windows 中。 此外，可以在 Windows 2000，Windows XP 和 Windows Server 2003 安装支持此 DDI 的 HD Audio 总线驱动程序的版本。

HDAUDIO\_总线\_接口\_BDL 结构定义包含以下例程 DDI:

[**AllocateCaptureDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536177)

[**AllocateContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536178)

[**AllocateRenderDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536181)

[**ChangeBandwidthAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff536229)

[**FreeContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536390)

[**FreeDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536393)

[**GetDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536397)

[**GetLinkPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536398)

[**GetResourceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536399)

[**GetWallClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536401)

[**RegisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff537803)

[**SetDmaEngineState**](https://msdn.microsoft.com/library/windows/hardware/ff537889)

[**SetupDmaEngineWithBdl**](https://msdn.microsoft.com/library/windows/hardware/ff537894)

[**TransferCodecVerbs**](https://msdn.microsoft.com/library/windows/hardware/ff538596)

[**UnregisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff538663)

新版 HD Audio 总线驱动程序支持 HDAUDIO\_总线\_接口\_BDL 版本 HD 音频 DDI 的可以安装在 Windows 2000、 Windows XP 和 Windows Server 2003。 但是，Windows Vista 提供对此 DDI 版本不支持。

在两个 DDIs 例程大部分都是相同的名称和操作。 但是，以下两个例程，属于 HDAUDIO\_总线\_DDI 的界面版本，不包括在 HDAUDIO\_总线\_接口\_BDL 版本：

[**AllocateDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536179)

[**FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)

同样，下面的三个例程在 HDAUDIO\_总线\_界面\_DDI BDL 版本不属于 HDAUDIO\_总线\_界面版本：

[**AllocateContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536178)

[**FreeContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536390)

[**SetupDmaEngineWithBdl**](https://msdn.microsoft.com/library/windows/hardware/ff537894)

本部分介绍以下 DDI 例程：

[**AllocateCaptureDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536177)

[**AllocateContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536178)

[**AllocateDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536179)

[**AllocateRenderDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536181)

[**ChangeBandwidthAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff536229)

[**FreeContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536390)

[**FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)

[**FreeDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536393)

[**GetDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536397)

[**GetLinkPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536398)

[**GetResourceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536399)

[**GetWallClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536401)

[**RegisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff537803)

[**SetDmaEngineState**](https://msdn.microsoft.com/library/windows/hardware/ff537889)

[**SetupDmaEngineWithBdl** ](https://msdn.microsoft.com/library/windows/hardware/ff537894)适用于[ **PHDAUDIO\_BDL\_ISR**](https://msdn.microsoft.com/library/windows/hardware/mt750609)

[**TransferCodecVerbs**](https://msdn.microsoft.com/library/windows/hardware/ff538596)

[**UnregisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff538663)

前面的列表包含在一个或两个版本的 DDI 中出现的所有例程。

 

 





