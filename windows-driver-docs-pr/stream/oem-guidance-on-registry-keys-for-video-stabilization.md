---
title: 视频防抖动注册表设置
description: VideoStabilization 注册表项中的 OEM set MaxPixelsPerSecond 值使 Oem 能够在设备上配置视频抖动设置，并在捕获时将视频抖动应用到视频。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a375c3aa94838f580787e1bfd471f0c3b7e5ddd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840523"
---
# <a name="video-stabilization-registry-settings"></a>视频防抖动注册表设置


**VideoStabilization** 注册表项中的 Oem set **MaxPixelsPerSecond** 值使 oem 能够在设备上配置视频抖动设置，并在捕获时将视频抖动应用到视频。 该配置会考虑设备的录制分辨率，并考虑其硬件和软件功能。

## <a name="overview"></a>概述


在最佳情况下， **VideoStabilization** 注册表项 **MaxPixelsPerSecond** 值用于指定设备上视频的最大性能。 所有应用程序都可以读取注册表项，并避免尝试合理使用视频抖动。

在 **MaxPixelsPerSecond** 值中输入的值将设置限制，超过该限制后，MFT 将不会尝试启用视频抖动，即使应用程序启用它也是如此。 注册表项需要指示设备运行视频抖动的最大分辨率和帧速率。 如果未设置 **MaxPixelsPerSecond** 值，则视频稳定化 MFT 将使用回退值。 最后，如果此操作失败，视频稳定性将使用其内部逻辑来关闭以防止获得最佳的用户体验。

## <a name="video-stabilization-requirements"></a>视频抖动要求


当发生以下所有情况时，设备被视为能够运行视频抖动：

-   视频稳定处于开启状态，并且未处于直通模式

-   录制已打开

-   预览处于活动状态

-   预览中未显示干扰或丢帧

-   录制的视频中未显示干扰帧或丢帧

## <a name="set-the-video-stabilization-registry-key"></a>设置视频不稳定注册表项


**VideoStabilization 注册表项格式：**

-   Oem 应设置 **MaxPixelsPerSecond** QWORD 值，该值定义每秒像素数的截止值，超过此值后，视频稳定将被强制在传递模式下运行（即使应用程序已启用）。

-   **MaxPixelsPerSecond** 定义如下：

    `MaxPixelsPerSecond = width * height * frame-rate`

    例如，对于 30 fps 的1080p 分辨率， **MaxPixelsPerSecond** 将定义为 1920 \* 1080 \* 30 = 62208000。

**VideoStabilization 注册表项位置：**

-   在以下位置，Oem 应创建并设置视频稳定的 **VideoStabilization** 注册表项：

    **HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ Windows 媒体基础 \\ 平台 \\ VideoStabilization**

    若要在32位计算机上设置 **VideoStabilization** 注册表项 **MaxPixelsPerSecond** 值，请在提升的命令提示符下使用以下命令：

    ```console
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Media Foundation\Platform\VideoStabilization" /v "MaxPixelsPerSecond" /t REG_QWORD /d 62208000 /f 
    ```

-   在64位计算机上，Oem 还应在 Wow6432Node 路径上创建和设置相同的密钥：

    **HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Wow6432Node \\ Microsoft \\ Windows 媒体基础 \\ 平台 \\ VideoStabilization**

    若要在64位计算机上设置 **VideoStabilization** 注册表项 **MaxPixelsPerSecond** 值，请在提升的命令提示符下使用以下命令：

    ```console
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Windows Media Foundation\Platform\VideoStabilization" /v "MaxPixelsPerSecond" /t REG_QWORD /d 62208000 /f 
    ```

设置此项后， **VideoStabilization** 注册表项将对视频稳定 MFT 和第一个和第三方应用可见。

如果设置了 **MaxPixelsPerSecond** 值，则视频稳定 MFT 将永远不会尝试稳定帧速率或超出限制的分辨率。 相反，它将进入直通模式，即使应用程序请求视频稳定性。 视频稳定 MFT 有一种机制，用于向给定设备的应用程序推荐帧速率和分辨率。 应用可以选择建议，以避免在已填充注册表项的设备上进行此类传递。

如果未设置 **MaxPixelsPerSecond** 值，则视频稳定化 MFT 将尝试使其达到默认值，但不会更高。

默认值为每秒62208000像素，即1920像素 x 1080 像素 x 30 fps。 当视频抖动尝试稳定，但无法维持视频帧的实时稳定性时，内部逻辑会将视频抖动切换为直通模式 (关闭视频稳定) 而不删除任何帧。

如果在上一个会话中视频抖动关闭，则在决定切换到直通模式之前，MFT 将尝试在每个新会话的常规模式下启动视频稳定性。 这是因为它不能依赖之前的模式来做出未来的决策，因为设备在上次操作时可能已经过压力。

## <a name="video-stabilization-test-requirements"></a>视频抖动测试要求


Oem 需要验证其设备的端到端功能是否正常工作。 它们需要以每秒给定的最大像素分辨率来验证可接受的体验。

Oem 必须验证以下各项：

-   Microsoft 提供的注册表项位置禁用了视频稳定内部逻辑。 禁用内部逻辑可保证在遇到压力情况时，视频稳定不会进入直通模式。

-   视频稳定可以单独运行，无需后台任务或其他功能

-   启用视频稳定并禁用内部逻辑时的平滑预览呈现

-   启用视频稳定并禁用内部逻辑时的平滑视频录制

-   稳定记录中实现的每秒所需像素数

-   无过热

**注意** 零售系统不应具有用于禁用本部分中所述视频稳定化内部逻辑的注册表项。 但是，零售系统应具有 **VideoStabilization** 注册表项，该注册表项具有通过此测试过程确定的 **MaxPixelsPerSecond** 值。


**注意** 仅当对此效果设置了 attribute [MF \_ 低 \_ 延迟](/windows/desktop/medfound/mf-low-latency)时， **VideoStabilization** 注册表项 **MaxPixelsPerSecond** 值功能才起作用。 将提供的视频抖动效果添加到 MediaCapture 管道后，会自动设置属性。 但是，如果将视频抖动效果插入到未设置 **MF \_ 低 \_ 延迟** 属性的自定义管道或管道，则注册表项不起作用。
