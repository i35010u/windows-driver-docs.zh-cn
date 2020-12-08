---
title: 适用于相机的 UWP 设备应用
description: 此部分介绍相机的 UWP 设备应用。
ms.date: 09/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 63433ff7abc3dede4389aea009a43adce47ac3e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802647"
---
# <a name="uwp-device-apps-for-cameras"></a>适用于相机的 UWP 设备应用


此部分介绍相机的 UWP 设备应用。 设备应用可以通过自定义相机设置和特殊相机效果突出显示相机的特殊功能。

## <a name="in-this-section"></a>在本节中


| 主题 | 描述 |
| ----- | ----------- |
| [如何自定义相机选项](how-to-customize-camera-options.md) | 在 Windows 8.1 中，UWP 设备应用允许设备制造商自定义在某些照相机应用中显示更多相机选项的弹出窗口。 本主题介绍了 CameraCatureUI API 显示的 " <strong>更多选项</strong> " 弹出窗口，并演示了 c # 版本的 [UWP 设备应用程序](/samples/browse/) 示例如何使用自定义浮出控件替换默认浮出控件。 |
| [创建相机驱动程序 MFT](creating-a-camera-driver-mft.md) | 在 Windows 8.1 中，UWP 设备应用允许设备制造商通过相机驱动程序 MFT 将自定义设置和特殊效果应用于照相机的视频流， (media foundation 转换) 。 本主题介绍了驱动程序 MFTs，并使用了 [驱动程序 MFT](/samples/browse/) 示例演示如何创建一个。<br><br> **重要提示：** 本主题已弃用。 请参阅 [设备 MFT 设计指南](../stream/dmft-design.md) 了解更新的指南。
| [多针相机上的驱动程序 MFT 的注意事项](driver-mfts-on-multi-pin-cameras.md) | 有些相机为预览、捕获和静止相机提供不同的 pin。 这些多 pin 相机为开发人员带来了独特的挑战。 本主题介绍在多 pin 相机上开发照相机驱动程序 MFT 时要考虑的一些要点。 |
| [识别内部相机的位置](identifying-the-location-of-internal-cameras.md) | 本主题提供有关在 Windows 8.1 中的系统上支持内部相机的信息。 它介绍如何识别内置相机的物理位置，使其能够正常使用 UWP 应用。 它还介绍了如何设置模型 ID，以便相机与 UWP 设备应用程序一起工作。 |


## <a name="windows-81-samples"></a>Windows 8.1 示例


-   [适用于照相机的 uwp 设备应用](/samples/browse/)示例提供了一个 UWP 设备应用，该应用控制驱动程序 MFT 实现的效果。

-   [驱动程序 mft](/samples/browse/)示例提供用于照相机的 UWP 设备应用程序的驱动程序 mft。 驱动程序 MFT 是在捕获视频时用于特定相机的媒体基础转换。 驱动程序 MFT 也称为 MFT0，因为它是应用于从照相机捕获的视频流的第一个 MFT。 从相机捕获照片或视频时，此 MFT 可提供视频效果或其他处理。 它可以与照相机的驱动程序包一起分发。

-   [相机捕获 UI](/samples/browse/)示例演示如何使用[CameraCaptureUI](/uwp/api/Windows.Media.Capture.CameraCaptureUI) API，该 API 显示用于捕获照片或视频的全屏幕 UI。 相机捕获 UI 提供了用于从照片切换到视频的控件、用于拍摄延迟照片的计时器以及用于调整照相机设置的相机选项控制。

    您可以使用此示例调用 [UWP 设备应用程序的相机](/samples/browse/) 示例。

-   [相机选项 UI](/samples/browse/)示例演示如何在 UWP 设备应用中使用相机选项。
