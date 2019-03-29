---
title: 内容 ID 和内容权限
description: 内容 ID 和内容权限
ms.assetid: aee123e4-bc1b-4ba8-9f8d-a9d207297c8d
keywords:
- 内容权利 WDK 音频
- 内容 Id WDK 音频
- 数字权限管理 WDK 音频，则内容 Id
- DRM WDK 音频，则内容 Id
- 数字权限管理 WDK 音频，则内容权限
- DRM WDK 音频，则内容权限
- 标识符 WDK 音频
- 混合的流 WDK 音频
- DigitalOutputDisable 标志
- CopyProtect 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c87c077220de72741cb932713ddcffa4abf4ee6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568146"
---
# <a name="content-ids-and-content-rights"></a>内容 ID 和内容权限


## <span id="content_ids_and_content_rights"></span><span id="CONTENT_IDS_AND_CONTENT_RIGHTS"></span>


内容 ID （标识符） 是 ULONG 值[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)生成在运行时来识别在馈送到特定 pin 的音频数据流中的受 DRM 保护内容。

内容的权限是通过内容提供商授予给用户的播放和复制受 DRM 保护的内容的权限的数字表示形式。 内容形式的指定权限[ **DRMRIGHTS** ](https://msdn.microsoft.com/library/windows/hardware/ff536355) DRMK 将传递给音频驱动程序的结构。

DRMRIGHTS 包含两个标志：**DigitalOutputDisable**并**CopyProtect**。 如果**DigitalOutputDisable**设置标志，该驱动程序必须禁用任何数字输出连接到外部设备 （通过 S/PDIF 连接器，例如）。 如果**CopyProtect**设置标志，该驱动程序必须禁用可能允许安全的内容保存到磁盘或任何其他形式的非易失性存储的持久性副本的功能。 例如，典型的音频硬件允许播放信号以通过捕获通道进行路由。 如果此信号是以数字形式，捕获的信号可能适合数字输入信号的副本。 如果播放混合包含具有任何流中的数据**CopyProtect**标志设置，该驱动程序必须设为静音播放捕获路径。

DRM 兼容的音频驱动程序必须支持[IDrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff536568)它 WaveCyclic 和 WavePci 微型端口驱动程序的对象公开用于呈现音频数据接收器插针上的接口。 若要获取对的引用**IDrmAudioStream**中的驱动程序，DRMK 调用对象**QueryInterface**的插针的方法。 Pin 包含类型的接口[IMiniportWaveCyclicStream](https://msdn.microsoft.com/library/windows/hardware/ff536715)或[IMiniportWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536725)。 **IDrmAudioStream**接口支持只有一个方法[ **IDrmAudioStream::SetContentId** ](https://msdn.microsoft.com/library/windows/hardware/ff536570) (除了这三个**IUnknown**方法)。 当调用 DRMK **SetContentId**，它将传入的内容 ID 和内容的权利，该驱动程序将与 pin 的数据流相关联。

而不是直接调用 Drmk.sys 中的 DRM 函数，WaveCyclic 或 WavePci 微型端口驱动程序可以访问通过 DRM 函数[IDrmPort2](https://msdn.microsoft.com/library/windows/hardware/ff536573)接口 (**IDrmPort2**派生自基类[IDrmPort](https://msdn.microsoft.com/library/windows/hardware/ff536571))。 在 Microsoft Windows XP 及更高版本，WaveCyclic 和 WavePci 端口驱动程序支持**IDrmPort2**。 微型端口驱动程序将获取对端口驱动程序的引用**IDrmPort2**通过调用 port 对象的接口**QueryInterface**方法替换 REFIID IID\_IDrmPort2。

一些音频驱动程序支持硬件混合使用，并且可以同时处理多个输入的数据流。 这种类型的驱动程序必须跟踪的单个流和复合的内容权利的所有流的两个的内容 Id。 驱动程序调用[ **IDrmPort::CreateContentMixed** ](https://msdn.microsoft.com/library/windows/hardware/ff536581)以确定混合流的复合权限并创建一个内容 ID 来标识该流。 完成该驱动程序使用的内容 ID 后，它必须调用[ **IDrmPort::DestroyContent** ](https://msdn.microsoft.com/library/windows/hardware/ff536583)若要删除该内容 id。

每次添加或删除混音器，从输入的流驱动程序必须删除旧的组合的内容 ID 并创建新的组合的新内容 ID。 然后再删除旧的内容 ID，该驱动程序必须首先成功转发到它以前转发到旧的内容 id。 所有流的新内容 ID 有关详细信息，请参阅[转发 DRM 内容 Id](forwarding-drm-content-ids.md)。

 

 




