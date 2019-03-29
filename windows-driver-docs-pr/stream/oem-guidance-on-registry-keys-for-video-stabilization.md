---
title: 视频防抖动注册表设置
description: VideoStabilization 注册表项中的 OEM 集 MaxPixelsPerSecond 值使 Oem 可以在设备上配置视频防抖动设置并将视频防抖动应用于视频捕获时间。
ms.assetid: F0F7A705-0F39-4A62-A110-A2E47DFB7B42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 046b6f14712bee5ad278772da5bcca650ac6832d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562948"
---
# <a name="video-stabilization-registry-settings"></a>视频防抖动注册表设置


OEM 集**MaxPixelsPerSecond**中的值**VideoStabilization**注册表项使 Oem 可以在设备上配置视频防抖动设置并将视频防抖动应用于在视频捕获的时间。 配置设备的录制分辨率，以及其硬件和软件功能将考虑在内。

## <a name="overview"></a>概述


**VideoStabilization**注册表项**MaxPixelsPerSecond**值用于在设备上，在最佳情况下指定的最大的视频防抖动功能。 所有应用程序可以读取注册表项和避免尝试不合理的视频防抖动的使用情况。

中输入的值**MaxPixelsPerSecond**超过该 MFT 不会尝试打开视频防抖动，即使应用程序启用它的限制值设置。 注册表项需要指示设备可以从该处运行视频防抖动的最大分辨率和帧速率。 如果**MaxPixelsPerSecond**未设置值，视频防抖动 MFT 将使用回退值。 最后，如果也失败，视频防抖动将使用其内部逻辑若要关闭以防止非最佳用户体验。

## <a name="video-stabilization-requirements"></a>视频防抖动要求


设备被视为能够运行时可能发生以下所有内容的视频防抖动：

-   视频防抖动处于开启状态并不是传递模式

-   录制已打开

-   预览处于活动状态

-   在预览中看到任何干扰或丢弃的帧

-   录制的视频中看到任何干扰或丢弃的帧

## <a name="set-the-video-stabilization-registry-key"></a>将视频防抖动注册表项设置


**VideoStabilization 注册表密钥格式：**

-   Oem 应设置**MaxPixelsPerSecond** QWORD 值，用于定义编号的第二个，更高版本的视频防抖动会被强制运行在直通模式下，即使它启用的应用程序每像素的截止值。

-   **MaxPixelsPerSecond**定义，如下所示：

    `MaxPixelsPerSecond = width * height * frame-rate`

    例如，对于在 30 fps，分辨率为 1080p **MaxPixelsPerSecond**将被定义为 1920年\*1080年\*30 = 62208000。

**VideoStabilization 注册表项位置：**

-   Oem 应创建并设置**VideoStabilization**视频防抖动的以下位置的注册表项：

    **HKEY\_本地\_MACHINE\\软件\\Microsoft\\Windows Media Foundation\\平台\\VideoStabilization**

    若要设置**VideoStabilization**注册表项**MaxPixelsPerSecond**值在 32 位计算机上时，请在提升的命令提示符使用以下命令：

    ```console
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Media Foundation\Platform\VideoStabilization" /v "MaxPixelsPerSecond" /t REG_QWORD /d 62208000 /f 
    ```

-   64 位计算机上 Oem 还应创建并在 Wow6432Node 路径上设置相同的密钥：

    **HKEY\_本地\_MACHINE\\软件\\Wow6432Node\\Microsoft\\Windows Media Foundation\\平台\\VideoStabilization**

    若要设置**VideoStabilization**注册表项**MaxPixelsPerSecond**值 64 位计算机上时，请在提升的命令提示符使用以下命令：

    ```console
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Windows Media Foundation\Platform\VideoStabilization" /v "MaxPixelsPerSecond" /t REG_QWORD /d 62208000 /f 
    ```

设置时， **VideoStabilization**注册表项将视频防抖动 MFT 和第一个和第三方应用对可见。

如果**MaxPixelsPerSecond**设置值，视频防抖动 MFT 决不会试图稳定帧速率或超出限制的解决方法。 相反，它将进入直通模式下，即使应用请求视频防抖动。 视频防抖动 MFT 具有一种机制来为给定设备应用中建议帧速率和分辨率。 应用程序可以选择以避免此类传递具有填充的注册表项的那些设备上的建议。

如果**MaxPixelsPerSecond**值未设置，视频防抖动 MFT 将尝试达到稳定状态，直到达到默认值，但不要太高。

默认值为每秒，即 1920年像素 x 1080 像素 x 30 fps 62208000 像素。 视频防抖动尝试达到稳定状态，但不能维护实时稳定的视频帧，内部逻辑将切换视频防抖动为直通模式 （关闭视频防抖动） 而不删除任何帧。

视频防抖动关闭上一个会话中，如果 MFT 将尝试为每个新会话，决定切换到直通模式之前在常规模式下启动视频防抖动。 这是因为它可以不依赖于以前的模式来决定未来，因为设备可能已在压力下时上一次操作。

## <a name="video-stabilization-test-requirements"></a>视频防抖动测试要求


Oem 需要验证其视频防抖动工作的设备的端到端功能。 他们需要验证在给定的最大像素 / 第二种解决方案的可接受的体验。

Oem 必须验证以下各项：

-   视频防抖动内部逻辑在 Microsoft 提供的注册表项位置处于禁用状态。 禁用内部逻辑可保证，视频防抖动不会进入直通模式下遇到的压力的情况下，它测试过程。

-   视频防抖动可以运行独立的而无需后台任务或其他功能

-   使用视频防抖动启用和禁用的内部逻辑的流畅预览呈现

-   平滑视频录制视频防抖动启用和禁用的内部逻辑

-   每秒计数来实现所需的像素稳定录制

-   没有温度过高

**请注意**零售系统不应具有注册表项来禁用此部分中所述的视频防抖动内部逻辑。 但是，零售系统应有**VideoStabilization**的注册表项**MaxPixelsPerSecond**通过此测试过程中确定的值。


**请注意** **VideoStabilization**注册表项**MaxPixelsPerSecond**值函数仅当属性[MF\_低\_延迟](https://msdn.microsoft.com/library/windows/desktop/hh162832)效果设置。 提供的视频防抖动效果添加到 MediaCapture 管道，将自动设置该属性。 但是，如果视频防抖动效果插入到自定义管道或的管道，不会设置**MF\_低\_延迟**属性，注册表项不起作用。
