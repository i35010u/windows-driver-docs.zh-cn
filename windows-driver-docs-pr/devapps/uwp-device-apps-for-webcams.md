---
title: 适用于相机的 UWP 设备应用
description: 此部分介绍相机的 UWP 设备应用。
ms.assetid: 6CF13679-BCF3-443C-A864-4BBC54B8DA1C
ms.date: 09/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 24feda30bbe41eba2021a02bda768b76200ef53b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359486"
---
# <a name="uwp-device-apps-for-cameras"></a>适用于相机的 UWP 设备应用


此部分介绍相机的 UWP 设备应用。 设备应用程序可以突出显示自定义的相机设置和特殊的照相机效果通过照相机的特殊的功能。

## <a name="in-this-section"></a>本节内容


| 主题 | 描述 |
| ----- | ----------- |
| [如何自定义照相机选项](how-to-customize-camera-options.md) | 在 Windows 8.1 UWP 设备应用程序允许设备制造商自定义某些相机应用中显示更多的照相机选项浮出控件。 本主题介绍<strong>更多选项</strong>浮出控件，显示由 CameraCatureUI API，并显示如何将C#的版本[UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例将替换与默认浮出控件自定义浮出控件。 |
| [创建一个照相机驱动程序 MFT](creating-a-camera-driver-mft.md) | 在 Windows 8.1 UWP 设备应用程序允许设备制造商上与相机驱动程序 MFT （媒体基础转换） 的照相机的视频流应用自定义设置和特殊效果。 本主题介绍驱动程序 Mft 并使用[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例来演示如何创建一个。<br><br> **重要：** 本主题已弃用。 请参阅[设备 MFT 设计指南](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)更新的指南。
| [多针相机上的驱动程序 Mft 的注意事项](driver-mfts-on-multi-pin-cameras.md) | 某些摄像机的预览版、 捕获和仍可提供独立引脚。 这些多针口相机会给开发人员带来独特的挑战。 本主题介绍了要开发多针相机上的照相机驱动程序 MFT 时考虑的一些要点。 |
| [确定内部相机的位置](identifying-the-location-of-internal-cameras.md) | 本主题提供有关在 Windows 8.1 中的系统上支持内部相机的信息。 它介绍了如何识别的内置相机物理位置，以便它们能够正常运行的 UWP 应用。 它还介绍了如何设置模型 ID，以使照相机适用于 UWP 的设备应用程序。 |


## <a name="windows81-samples"></a>Windows 8.1 示例


-   [UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例提供了控制由驱动程序 MFT 实现的效果的 UWP 设备应用程序。

-   [驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例提供了用于相机的 UWP 设备应用程序的驱动程序 MFT。 驱动程序 MFT 是捕获视频时使用特定照相机使用媒体基础转换。 驱动程序 MFT 也称为是 MFT0，因为它是第一个 MFT 应用于从照相机中捕获的视频流。 捕获照片或视频从摄像机时，此 MFT 可以提供视频效果或其他处理。 可以与照相机的驱动程序包一起分发。

-   [摄像头捕获 UI](https://go.microsoft.com/fwlink/p/?linkid=228589)示例演示如何使用[Windows.Media.Capture.CameraCaptureUI](https://msdn.microsoft.com/library/windows/apps/br241030) API，后者会显示全屏显示 UI 的捕获照片或视频。 摄像头捕获 UI 提供了用于从照片切换到视频、 使时间延迟拍摄的照片，计时器和相机设置调节照相机选项控件的控件。

    可以使用此示例以调用[UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例。

-   [相机选项 UI](https://go.microsoft.com/fwlink/p/?linkid=228588)示例演示如何在 UWP 设备应用中使用相机选项。
