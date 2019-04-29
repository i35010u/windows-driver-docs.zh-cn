---
title: DirectX VA COPP 设备
description: DirectX VA COPP 设备
ms.assetid: f9268b38-3317-4c4f-b9c1-e0ad3c88f92e
keywords:
- COPP 设备 WDK DirectX VA
- 复制保护 WDK COPP，COPP 设备
- 视频复制保护 WDK COPP，COPP 设备
- COPP WDK DirectX VA，COPP 设备
- 受保护视频 WDK COPP，COPP 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c70743891b3a1c48dc327e6a9f5186ab093edf54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380417"
---
# <a name="directx-va-copp-device"></a>DirectX VA COPP 设备


## <span id="ddk_directx_va_copp_device_gg"></span><span id="DDK_DIRECTX_VA_COPP_DEVICE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

应实现显示器驱动程序，以便为每个视频会话创建 DirectX VA COPP 设备。 COPP 设备表示终结点以接收 COPP 命令和状态请求。 COPP 设备还将存储其关联的物理连接器的保护设置。 物理连接器可以支持多个内容保护类型。 例如，S-视频连接器可以支持模拟内容保护 (ACP) 内容生成管理系统除了模拟 (CGMS A) 保护。 有关详细信息，请参阅[定义 COPP 设备类](defining-the-copp-device-class.md)。

COPP 设备的多个实例是输出的必需的以便不同的进程可以配置的设置通过 COPP 图形适配器。 因此，应实现 COPP 设备类，以便每个 COPP 设备执行相应的操作时多个视频会话处于活动状态在系统上。

**请注意**  视频课程包含的一个或多个视频的子流可能需要合并的视频流。 视频会话绑定到特定的图形适配器的输出连接器。 多个视频会话可处于活动状态，及在单个进程中的系统上。

 

 

 





