---
title: 初始化视频微型端口/显示器驱动程序通信
description: 初始化视频微型端口以便与显示驱动程序通信
ms.assetid: 73ba423c-7ebc-4a07-aed0-d2e33f11b878
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，初始化
- 初始化视频微型端口驱动程序
- HwVidInitialize
- 一次性初始化 WDK 视频微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 90e4cd58ebd5016b17b406b70f1a52b7438cd316
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840370"
---
# <a name="initializing-the-video-miniport-for-communication-with-display-driver"></a>初始化视频微型端口以便与显示驱动程序通信

对于 PnP 管理器找到的每个适配器并通过微型端口驱动程序成功配置，加载相应的显示驱动程序时，将调用微型端口驱动程序的[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)函数。 *HwVidInitialize*可以初始化软件状态信息，但它不应在适配器上设置可见状态。 从*HwVidInitialize*返回时，适配器应设置为与从微型端口驱动程序的[*HwVidResetHw*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_reset_hw)例程返回相同的状态。 有关*HwVidResetHw*的详细信息，请参阅[重置视频微型端口驱动程序中的适配器](resetting-the-adapter-in-video-miniport-drivers.md)。

如果需要，微型端口驱动程序的*HwVidInitialize*函数可以在适配器上执行由其*HwVidFindAdapter*函数延迟的一次性初始化操作。 例如，微型端口驱动程序可能会延迟在适配器上加载微码，并使*HwVidInitialize*函数调用[**VideoPortGetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetregistryparameters)。

当*HwVidInitialize*。 有关详细信息，请参阅[处理视频请求（Windows 2000 模型）](processing-video-requests--windows-2000-model-.md) 。

通常，显示驱动程序会控制最终用户看到的显示，但在运行基于 NT 的操作系统的基于 x86 的计算机中运行全屏 MS-DOS 应用程序时偶尔除外。 若要详细了解如何在 VGA 兼容的微型端口驱动程序中支持此功能，请参阅[与 Vga 兼容的视频微型端口驱动程序（Windows 2000 模型）](vga-compatible-video-miniport-drivers--windows-2000-model-.md)。

[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)函数可调用[**VideoPortGetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetregistryparameters)或[**VideoPortSetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsetregistryparameters) ，以获取和设置注册表中的配置信息。 例如， *HwVidInitialize*可能会调用**VideoPortSetRegistryParameters** ，为下一次启动设置注册表中的非易失性配置信息。 它可以调用**VideoPortGetRegistryParameters**来获取由安装程序写入到注册表中的特定于适配器的总线相关配置参数。

 

 





