---
title: USB 视频类 (UVC) 驱动程序实现清单
description: 提供如何为设备实现 USB 视频类（UVC）驱动程序的分步信息。
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 39b2485631a33df4f414dc48e6d354ea36d500b5
ms.sourcegitcommit: baf3075858705d4c78d4ea4b0869bf6291bcb823
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2020
ms.locfileid: "85112139"
---
# <a name="usb-video-class-uvc-driver-implementation-checklist"></a>USB 视频类 (UVC) 驱动程序实现清单

## <a name="step-1-get-started-with-usb-video-class-uvc-using-documentation-from-usborg-and-microsoft"></a>步骤1：使用来自 USB.org 和 Microsoft 的文档开始使用 USB 视频类（UVC）

使用以下链接了解 UVC：

- 在 USB.org 访问[USB 类](https://www.usb.org/documents?search=&type%5B0%5D=55&items_per_page=50)文档（非 UVC）

- 从 USB.org 下载[USB Video 类 1.5](https://www.usb.org/document-library/video-class-v15-document-set)文档

- 查看[USB 视频类驱动程序概述](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver-overview)主题

## <a name="step-2-implement-the-platform-supplied-device-mft"></a>步骤2：实现平台提供的设备 MFT

- 平台提供的设备 MFT 用于 RGB USB 摄像机。 它提供通用功能，例如，针对3A 优先级的人脸检测投资回报率（如果照相机固件支持 UVC 1.5 标准中指定的 ROI 控制）。

- 若要启用此功能，需要确保相机支持投资回报率。 如果需要禁用此功能，则必须通过注册表项（例如，INF 文件条目）来执行此操作。

## <a name="step-3-implement-the-custom-device-mft-and-mft0-for-your-device"></a>步骤3：为设备实现自定义设备 MFT 和 MFT0

- 设备 MFT 是 UVC 的用户模式组件。 你可以插入此组件，以便向 UVC 添加扩展插件和优异点。

- 查看[设备 MFT 设计指南](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)。

- 查看[设备 MFT 示例代码](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/driver-device-transform-sample/)。

- 查看[创建 UWP 设备应用的照相机驱动程序 MFT](https://docs.microsoft.com/windows-hardware/drivers/devapps/creating-a-camera-driver-mft)主题中有关 MFT0 的相关信息。

> [!NOTE]
> 设备 MFT 模型取代了 MFT0 模型。 虽然 Windows 仍支持 MFT0 模型，但我们鼓励您改用设备 MFT，因为它简化了设计，并支持更多功能和可扩展性。

## <a name="step-4-implement-microsoft-specified-uvc-extensions"></a>步骤4：实现 Microsoft 指定的 UVC 扩展

- [USB 视频类 1.5 规范的 Microsoft 扩展](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)

- [UVC 中的红外流支持](https://docs.microsoft.com/windows-hardware/drivers/stream/infrared-stream-support-in-uvc)

- 方法2静止图像捕获：

  - USB.org 文档：

    - 查看*UVC 1.5 类*的第17页上开始的*方法 2*部分，specification.pdf你在上面的步骤1中下载了。

  - 特定于 Microsoft 的文档：

    - 请参阅[Microsoft extension TO USB Video Class 1.5 规范](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)中的2.2.1 和2.2.2 部分。

## <a name="step-5-test-your-uvc-implementation-to-ensure-it-passes-hlk-tests-and-meets-required-functionality-and-performance"></a>步骤5：测试 UVC 实现，以确保它能够通过了 HLK 测试并满足所需的功能和性能

- 运行[WINDOWS HLK 测试](https://docs.microsoft.com/windows-hardware/drivers/)

- 运行特定于相机的[设备。流式处理 HLK 测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-streaming)

- 确保摄像机满足任何要求，并为相机还必须符合的其他产品（例如 Skype、Windows Hello 等）传递 HLK 测试。
