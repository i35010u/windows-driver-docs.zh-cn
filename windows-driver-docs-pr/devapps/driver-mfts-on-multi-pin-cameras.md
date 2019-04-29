---
title: 使用多针口相机上的驱动程序 Mft
description: 某些摄像机的预览版、 捕获和仍可提供独立引脚。 这些多针口相机会给开发人员带来独特的挑战。 本主题介绍了要开发多针相机上的照相机驱动程序 MFT 时考虑的一些要点。
ms.assetid: E946C676-D1CE-4759-A255-3E16EDCE599F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f811d3e914f270cea15d534a84d4df8673cdefaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387992"
---
# <a name="span-iddevappsdrivermftsonmulti-pincamerasspanconsiderations-for-driver-mfts-on-multi-pin-cameras-uwp-device-apps"></a><span id="devapps.driver_mfts_on_multi-pin_cameras"></span>多针相机 （UWP 设备应用程序） 上的驱动程序 Mft 的注意事项


Windows 8.1 提供 Ihv 和系统 Oem 在窗体的媒体基础转换 (MFT)，称为照相机驱动程序 MFT 中创建视频处理插件的功能。 安装后，通过 UWP 设备应用程序使用这些驱动程序 Mft，可以启用特殊视频效果。 某些摄像机的预览版、 捕获和仍可提供独立引脚。 这些多针口相机会给开发人员带来独特的挑战。 本主题介绍了要开发多针相机上的照相机驱动程序 MFT 时考虑的一些要点。 有关创建驱动程序 MFT 的详细信息，请参阅[创建照相机驱动程序 MFT](creating-a-camera-driver-mft.md)。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


驱动程序 MFT 也称为 MFT0 以指示它是第一个 MFT 在源读取器操作。 MFT0 的单独实例附加到每个插针上捕获源。 对于某些系统 Oem，AVStream 捕获驱动程序必须支持预览针、 捕获 pin 和静止的 pin。 这意味着可能是 MFT0 的三个实例。 此图显示了此体系结构，与 IHV 插件 MFT，一个用于每个流的三个副本。

![捕获扩展插件模型中 mf](images/372842-cameracaptureengine.png)

MFT0 的典型方案可能非常困难。 两个常用 MFT0 函数是：

-   分析视频流以提供改进 （如基于主机的自动聚焦和自动公开） 捕获的照相机的反馈

-   添加视频效果

## <a name="span-idone-pinwebcamspanspan-idone-pinwebcamspanspan-idone-pinwebcamspanone-pin-webcam"></a><span id="One-pin_webcam"></span><span id="one-pin_webcam"></span><span id="ONE-PIN_WEBCAM"></span>单针网络摄像机


从历史上看，照相机已公开到 Windows 为单个捕获 pin。 此图显示单针网络摄像机的工作的方式：

![单针网络摄像机](images/372826-camera-one-pin-webcam.png)

在这种情况下，按设计因为预览和静止图像是 tee 将从捕获插针相机控件和视频效果应用后，将工作这两个相机控件和视频效果。 结果是已保存的文件或用户的聊天好友，将看到相同的视频效果，则用户将看到在其预览版中，以及有摄像机控制功能的一个实例。 如果没有关联的 UWP 设备应用，应用已连接到的捕获插针，MFT0 因此 MFT0 获取控制消息从应用程序 （用户）。

## <a name="span-idthree-pinwebcamspanspan-idthree-pinwebcamspanspan-idthree-pinwebcamspanthree-pin-webcam"></a><span id="Three-pin_webcam"></span><span id="three-pin_webcam"></span><span id="THREE-PIN_WEBCAM"></span>三针网络摄像机


三针相机可能多达三个 MFT0，具体取决于应用程序需要的实例。 此图显示三针相机的工作的方式：

![三针网络摄像机](images/372826-camera-three-pin-camera.png)

这种情况下具有不少挑战。 首先，在基于主机的自动公开解决方案中，这需要相机传感器和 ISP 设置的直接控制，三个 MFT0s 可能尝试在同一时间控制照相机。 这将中断控制系统。

其次，有可能的视频效果的三个实例。 超出产生三次计算的成本，MFT0 的三个实例必须现在会确保每个视频帧始终具有相同的效果完全相同的状态的方式进行通信。 否则用户看到的内容不会保存或共享的内容。

此外，有两个最终的复合因素：

-   可能会创建或关闭在任何时候 MFT0 的每个实例

-   UWP 设备应用程序仅连接到 MFT0 的一个实例

## <a name="span-idcompressedvideospanspan-idcompressedvideospanspan-idcompressedvideospancompressed-video"></a><span id="Compressed_video"></span><span id="compressed_video"></span><span id="COMPRESSED_VIDEO"></span>压缩的视频


网络摄像机或系统 OEM 可以选择显示的捕获插针压缩视频 (即，对网络摄像头本身)。 将对网络摄像机压缩后，较低功率的电脑来保存和共享高清视频。 此压缩的视频流通常不能进行分析以支持照相机控件，也可以应用视频效果。 这就使 MFT0 （和 Microsoft Store 设备应用，如果有） 的所有实例的质询注意没有效果，将应用于捕获流。 此关系图表示压缩的视频：

![压缩的视频](images/372826-camera-compressed-video.png)

如果用户适用于预览流视频效果，它不能应用于捕获流或仍 pin。 因此，用户将看到不应用于已保存或流式处理视频的视频效果。 如果预览流将暂停，Microsoft Store 应用设备应用程序然后尝试连接到捕获流。 当用户流式处理压缩的视频时，这不允许的许多功能。

## <a name="span-idcommunicationbetweenmft0instancesspanspan-idcommunicationbetweenmft0instancesspanspan-idcommunicationbetweenmft0instancesspancommunication-between-mft0-instances"></a><span id="Communication_between_MFT0_instances"></span><span id="communication_between_mft0_instances"></span><span id="COMMUNICATION_BETWEEN_MFT0_INSTANCES"></span>MFT0 实例之间的通信


如果 MFT0 的三个实例可以相互通信，这可能会解决大多数问题。 这些实例方式发现彼此负责 IHV。 一旦所有 MFT0s 可以进行都通信，MFT0 实例连接到 Microsoft Store 的设备应用程序就可以知道哪一种效果要应用其他实例和其当前状态。 此外，三个实例可以确定哪些实例会应用照相机控件。 最后，预览针可以确定捕获 pin 流式处理编码的视频。 预览针然后可以禁用视频效果。

尽管 MFT0 实例之间的通信可以解决主要的用户体验问题，但仍必须同时运行视频效果的三个实例。 某些视频效果可以使用最多可用 CPU 资源，尤其是当正在全屏视频预览并捕获一次。 这些是严重的问题。 出于性能原因，每个 ISV 应考虑什么处理可能会执行一次，例如人脸检测，并与 MFT0 的所有实例共享。

 

 





