---
title: 在多 pin 相机上使用驱动程序 MFTs
description: 有些相机为预览、捕获和静止相机提供不同的 pin。 这些多 pin 相机为开发人员带来了独特的挑战。 本主题介绍在多 pin 相机上开发照相机驱动程序 MFT 时要考虑的一些要点。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e87fd7b06d49c089ea4774d084ca565926fd11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815217"
---
# <a name="span-iddevappsdriver_mfts_on_multi-pin_camerasspanconsiderations-for-driver-mfts-on-multi-pin-cameras-uwp-device-apps"></a><span id="devapps.driver_mfts_on_multi-pin_cameras"></span> (UWP 设备应用的多针相机上的驱动程序 MFTs 的注意事项) 


Windows 8.1 为 Ihv 和系统 Oem 提供了以媒体基础)  (变换格式（称为照相机驱动程序 MFT）创建视频处理插件的功能。 安装之后，UWP 设备应用可以使用这些驱动程序 MFTs 来启用特殊的视频效果。 有些相机为预览、捕获和静止相机提供不同的 pin。 这些多 pin 相机为开发人员带来了独特的挑战。 本主题介绍在多 pin 相机上开发照相机驱动程序 MFT 时要考虑的一些要点。 有关创建驱动程序 MFT 的详细信息，请参阅 [创建照相机驱动程序 mft](creating-a-camera-driver-mft.md)。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


驱动程序 MFT 也称为 MFT0，指示它是在源读取器中操作的第一个 MFT。 单独的 MFT0 实例会附加到捕获源上的每个 pin。 对于某些系统 Oem，AVStream 捕获驱动程序必须支持预览 pin、捕获 pin 和静态 pin。 这意味着可能有三个 MFT0 实例。 此图显示了此体系结构，其中包含三个 IHV 插件 MFT 副本，每个流一个。

![在 mf 中捕获扩展插件模型](images/372842-cameracaptureengine.png)

MFT0 的典型方案可能会带来挑战。 MFT0 的两个热门函数是：

-   分析视频流以向照相机提供反馈以改善捕获 (例如基于主机的自动焦点和自动曝光) 

-   添加视频效果

## <a name="span-idone-pin_webcamspanspan-idone-pin_webcamspanspan-idone-pin_webcamspanone-pin-webcam"></a><span id="One-pin_webcam"></span><span id="one-pin_webcam"></span><span id="ONE-PIN_WEBCAM"></span>单针网络摄像机


从历史上看，照相机以单个捕获 pin 的形式向 Windows 公开。 此图显示了一台 pin 网络摄像机的工作方式：

![单针网络摄像机](images/372826-camera-one-pin-webcam.png)

在这种情况下，照相机控制和视频效果都按设计方式工作，这是因为在应用相机控制和视频效果之后，预览和静止图像是从捕获 pin 开始的。 结果是，已保存的文件或用户的聊天联系人会看到用户在预览中看到的相同视频效果，而且只有一个相机控制功能实例。 如果有关联的 UWP 设备应用，该应用会连接到捕获 pin 上的 MFT0，因此 MFT0 将从应用 (获取控制消息，即用户) 。

## <a name="span-idthree-pin_webcamspanspan-idthree-pin_webcamspanspan-idthree-pin_webcamspanthree-pin-webcam"></a><span id="Three-pin_webcam"></span><span id="three-pin_webcam"></span><span id="THREE-PIN_WEBCAM"></span>三针网络摄像机


根据应用程序的需要，三针相机可能具有多达三个 MFT0 实例。 此图显示了三针相机的工作方式：

![三针网络摄像机](images/372826-camera-three-pin-camera.png)

这种情况面临着几个难题。 首先，对于基于主机的自动曝光解决方案，这种解决方案需要直接控制相机传感器和 ISP 设置，三个 MFT0s 可能尝试同时控制相机。 这会中断控制系统。

其次，可能有三个视频效果实例。 除了计算三倍计算的成本之外，MFT0 的三个实例现在必须以确保每个视频帧在完全相同的状态中始终具有相同效果的方式进行通信。 否则，用户看到的内容将不是保存或共享的内容。

此外，还有两个最终的复合因素：

-   可随时创建或关闭 MFT0 的每个实例

-   UWP 设备应用仅连接到 MFT0 的一个实例

## <a name="span-idcompressed_videospanspan-idcompressed_videospanspan-idcompressed_videospancompressed-video"></a><span id="Compressed_video"></span><span id="compressed_video"></span><span id="COMPRESSED_VIDEO"></span>压缩的视频


网络摄像机或系统 OEM 可能会选择在视频显示在捕获 pin 上之前压缩视频， (也就是在网络摄像机上) 。 将压缩功能卸载到网络摄像机后，较低的计算机可以节省和共享高清视频。 此压缩视频流通常无法进行分析以支持相机控制，也不能应用视频效果。 这就带来了将 MFT0 的所有实例 (和 Microsoft Store 设备应用程序（如果存在）的难题，) 知道不会将任何效果应用到捕获流。 此图表示压缩视频：

![压缩的视频](images/372826-camera-compressed-video.png)

如果用户将视频效果应用于预览流，则它不能应用于捕获流或静止 pin。 因此，用户看到的视频效果不适用于已保存或流式处理的视频。 如果预览流已停止，Microsoft Store 设备应用程序将尝试连接到捕获流。 当用户使用流式传输压缩视频时，这不允许许多功能。

## <a name="span-idcommunication_between_mft0_instancesspanspan-idcommunication_between_mft0_instancesspanspan-idcommunication_between_mft0_instancesspancommunication-between-mft0-instances"></a><span id="Communication_between_MFT0_instances"></span><span id="communication_between_mft0_instances"></span><span id="COMMUNICATION_BETWEEN_MFT0_INSTANCES"></span>MFT0 实例间的通信


如果 MFT0 的三个实例可以相互通信，则这可能会解决大多数问题。 这些实例彼此之间的发现方式取决于 IHV。 在所有 MFT0s 都能通信后，连接到 Microsoft Store 设备应用的 MFT0 实例可让其他实例知道哪个效果正在应用及其当前状态。 此外，这三个实例可以确定哪个实例应用相机控件。 最后，预览 pin 可以确定捕获 pin 是否为流式传输编码视频。 预览 pin 随后可以禁用视频效果。

尽管 MFT0 的实例之间的通信解决了主要的用户体验问题，但视频效果的三个实例仍必须同时运行。 某些视频效果可以使用最多可用的 CPU 资源，尤其是在同时预览和捕获全屏视频时。 这些是严重问题。 出于性能方面的原因，每个 ISV 都应考虑可能执行一次的处理（如人脸检测），并与所有 MFT0 实例共享。

 

 





