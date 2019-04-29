---
title: 正在初始化/显示视频微型端口驱动程序通信
description: 初始化视频微型端口以便与显示驱动程序通信
ms.assetid: 73ba423c-7ebc-4a07-aed0-d2e33f11b878
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，初始化
- 初始化微型端口驱动程序
- HwVidInitialize
- 一次性初始化 WDK 微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 898cf7e25e1eda84d8ef0ff432c07609cac6f84a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350279"
---
# <a name="initializing-the-video-miniport-for-communication-with-display-driver"></a>初始化视频微型端口以便与显示驱动程序通信

为每个适配器和找到的即插即用管理器已成功配置由微型端口驱动程序微型端口驱动程序的[ *HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)相应显示驱动程序时调用函数加载。 *HwVidInitialize*可以初始化软件的状态信息，但它不应设置在适配器上的可见状态。 返回从*HwVidInitialize*上返回来自微型端口驱动程序的, 情况下，适配器应设置为相同状态[ *HwVidResetHw* ](https://msdn.microsoft.com/library/windows/hardware/ff567363)例程。 有关详细信息*HwVidResetHw*，请参阅[重置视频微型端口驱动程序中的适配器](resetting-the-adapter-in-video-miniport-drivers.md)。

如有必要，微型端口驱动程序*HwVidInitialize*函数可执行的一次性初始化操作推迟了。 在适配器上其*HwVidFindAdapter*函数。 例如，微型端口驱动程序可能会推迟加载在适配器上的微代码并具有*HwVidInitialize*函数调用[ **VideoPortGetRegistryParameters**](https://msdn.microsoft.com/library/windows/hardware/ff570316)。

当*HwVidInitialize*。 请参阅[处理视频请求 （Windows 2000 模式）](processing-video-requests--windows-2000-model-.md)有关详细信息。

通常情况下，显示器驱动程序控制最终用户看到的除偶尔的全屏 MS-DOS 应用程序运行在基于 x86 的机运行的基于 NT 的操作系统中的显示。 有关兼容的 VGA 的微型端口驱动程序支持此功能的详细信息，请参阅[兼容的 VGA 视频微型端口驱动程序 （Windows 2000 模式）](vga-compatible-video-miniport-drivers--windows-2000-model-.md)。

[ *HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)函数可调用[ **VideoPortGetRegistryParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff570316)或[ **VideoPortSetRegistryParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff570365)获取和设置在注册表中的配置信息。 例如， *HwVidInitialize*可能会在调用**VideoPortSetRegistryParameters**注册表中的下一次启动设置非易失性的配置信息。 它可能会调用**VideoPortGetRegistryParameters**若要获取特定于适配器的、 总线相对配置参数由安装程序写入到注册表。

 

 





