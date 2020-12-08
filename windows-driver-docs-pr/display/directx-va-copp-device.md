---
title: DirectX VA COPP 设备
description: DirectX VA COPP 设备
keywords:
- COPP 设备 WDK DirectX VA
- 复制保护 WDK COPP，COPP 设备
- 视频复制保护 WDK COPP，COPP 设备
- COPP WDK DirectX VA，COPP 设备
- 受保护的视频 WDK COPP，COPP 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7be464be30e52a669308c5758db0874a83708398
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809326"
---
# <a name="directx-va-copp-device"></a>DirectX VA COPP 设备


## <span id="ddk_directx_va_copp_device_gg"></span><span id="DDK_DIRECTX_VA_COPP_DEVICE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

应该实现显示驱动程序，以便为每个视频会话创建 DirectX VA COPP 设备。 COPP 设备表示用于接收 COPP 命令和状态请求的终结点。 COPP 设备还存储其关联的物理连接器的保护设置。 物理连接器可以支持多种内容保护类型。 例如，除了用于模拟 (CGMS 的内容生成管理系统) 外，S-视频连接器还可以支持 (ACP) 的模拟内容保护。 有关详细信息，请参阅 [定义 COPP 设备类](defining-the-copp-device-class.md)。

需要 COPP 设备的多个实例，以使不同的进程可以通过 COPP 配置图形适配器输出的设置。 因此，你应该实现 COPP 设备类，以便在系统上的多个视频会话处于活动状态时，每个 COPP 设备都能正常工作。

**注意**   视频会话由可能与一个或多个视频 substreams 组合的视频流组成。 视频会话与特定图形适配器的输出连接器相关联。 多个视频会话可以在系统上和单个进程内处于活动状态。

 

 

 





