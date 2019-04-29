---
title: USB 视频类 (UVC) 驱动程序实现清单
description: 提供有关实现你的设备的 USB 视频类 (UVC) 驱动程序分步信息。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9ae4a63cf21c92ba4dad28a357fdcf35bbea51d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367463"
---
# <a name="usb-video-class-uvc-driver-implementation-checklist"></a>USB 视频类 (UVC) 驱动程序实现清单

## <a name="step-1-get-started-with-usb-video-class-uvc-using-documentation-from-usborg-and-microsoft"></a>第 1 步：开始使用 USB 视频类 (UVC) 使用 USB.org 和 Microsoft 文档

使用下面的链接，了解 UVC:

- 访问[USB 类](http://www.usb.org/developers/docs/devclass_docs/)USB.org 文档 （非 UVC 特定于）

- 下载[USB 视频类 1.5](https://go.microsoft.com/fwlink/p/?linkid=2085170) USB.org 文档

- 审阅[USB 视频类驱动程序概述](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver-overview)主题

## <a name="step-2-implement-the-platform-supplied-device-mft"></a>步骤 2：实现平台提供设备 MFT

- 平台提供设备 MFT 是用于 RGB USB 摄像机。 它提供常见功能，例如，人脸检测的基于投资回报率的 3A 优先顺序 （如果照相机固件支持 UVC 1.5 标准中指定的投资回报率控件）。

- 若要启用此功能，需要确保照相机支持投资回报率。 如果你需要禁用此功能，必须通过注册表项 （例如，INF 文件条目） 来执行。

## <a name="step-3-implement-the-custom-device-mft-and-mft0-for-your-device"></a>步骤 3:为你的设备实现的自定义设备 MFT 和 MFT0

- 设备 MFT 是 UVC 的用户模式组件。 你可以将此组件向 UVC 添加扩展和竞争优势。

- 审阅[设备 MFT 设计指南](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)。

- 审阅[设备 MFT 示例代码](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/sampledevicemft)位于 GitHub 上。

- 查看情况的相关信息中 MFT0[创建的 UWP 设备应用程序的照相机驱动程序 MFT](https://docs.microsoft.com/windows-hardware/drivers/devapps/creating-a-camera-driver-mft)主题。

**请注意**设备 MFT 模型取代 MFT0 模型。 尽管 Windows 仍支持 MFT0 模型，我们建议您改为使用设备 MFT，因为它简化了设计，并支持更多的功能和可伸缩性。

## <a name="step-4-implement-microsoft-specified-uvc-extensions"></a>步骤 4：实现 Microsoft 指定 UVC 扩展

- [USB 视频类 1.5 规范的 Microsoft 扩展](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)

- [UVC 中的红外流支持](https://docs.microsoft.com/windows-hardware/drivers/stream/infrared-stream-support-in-uvc)

- 方法 2 静止图像捕获：

    - USB.org 文档：

        - 查看有关的部分*方法 2*上的第 17 页开头*UVC 1.5 类 specification.pdf*你在上面的步骤 1 中下载。

    - 特定于 Microsoft 的文档：

        - 查看部分 2.2.1 和在 2.2.2 [USB 视频类 1.5 规范的 Microsoft 扩展](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)。

## <a name="step-5-test-your-uvc-implementation-to-ensure-it-passes-hlk-tests-and-meets-required-functionality-and-performance"></a>步骤 5：测试 UVC 实现，以确保它通过 HLK 测试并满足所需的功能和性能

- 运行[Windows HLK 测试](https://msdn.microsoft.com/library/windows/hardware/dn930814)

- 运行特定于照相机的[Device.Streaming HLK 测试](https://msdn.microsoft.com/library/windows/hardware/dn941930)

- 请确保照相机满足任何要求，并通过照相机也必须符合 （例如，Skype、 Windows Hello，等） 其他产品的 HLK 测试。
