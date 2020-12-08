---
title: UEFI 固件更新的用户体验
description: 本部分介绍如何在 UEFI 固件更新过程中实现基本的用户体验。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7b72e10151220fb0f58b2aa6ea13aeb2c71654c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809737"
---
# <a name="user-experience-for-uefi-firmware-updates"></a>UEFI 固件更新的用户体验


本部分介绍如何在 UEFI 固件更新过程中实现基本的用户体验。

在固件更新过程中，请务必向最终用户提供对正在处理更新的视觉通知。 随着时间的推移，用户将会熟悉其设备启动到 Windows 所用的典型时间。 如果发生扩展此启动时间的固件更新，则需要通知用户需要扩展的启动时间。 否则，用户可能会在启动过程中断定设备无法启动或冻结，从而导致用户手动重新启动系统，从而中断固件更新过程。

若要避免这种情况，执行更新的固件必须通过显示设备正在更新的简单通知来管理用户体验。 这会重置用户的启动时间预期。 必须将此用户体验添加到已存在的 (，并熟悉用户) 启动屏幕。 显示的图形可能是 OEM 或主板制造商的徽标。

![标准 oem 启动屏幕](images/standardoembootscreen.png)

## <a name="user-experience"></a>用户体验


在固件更新过程中，显示必须显示正在进行更新的用户。 此用户体验 (UX) 的目标如下：

-   显示必须非常简短且易于理解。
-   必须与系统上的 Windows 操作系统版本具有相同的外观和感觉。
-   必须传达以下消息：
    -   在此过程中请勿扰乱系统 (请勿拔下电源 ) 。
    -   启动时间可能需要比预期更长的时间。
    -   更新过程仍在进行中。

下图演示了此 UX 的预期外观和感觉。 在此示例中，将显示一个 OEM 图像 (虚拟 Contoso 徽标) ，因为在系统启动时，会显示该徽标。 文本 "请等待我们安装系统更新" 指示关键的系统组件更新正在进行。 用户已了解，这意味着让设备执行它必须执行的操作，而不会干扰，因为这可能需要一段时间。

![固件更新启动屏幕](images/firmwareupdatebootscreen.png)

## <a name="time-frame"></a>期限


在初始启动过程中，系统将需要将用户显示为设备所需的标准启动屏幕。 但是，一旦 Windows 启动程序检测到新的固件胶囊文件存在，它将从正常启动屏幕转换到固件更新启动屏幕。 该转换将包括在屏幕上显示本地化文本的 Windows 引导程序，指示在调用 UpdateCapsule ( # A1 之前正在进行更新。

固件更新 UX 需要在 UpdateCapsule ( # A1 中显示，直到已成功应用所有固件更新，并且系统已将启动过程移交给 Windows。 如果在这段时间内需要重新启动，则必须进行每次尝试，以继续显示固件更新启动屏幕而不中断。 如果无法执行此操作 (例如，更新了 GPU 固件，或者需要冷重启) 则必须尽快显示固件更新启动屏幕，然后再进行一次尝试。 为了满足此要求，Windows 引导加载将为固件提供本地化文本的位图副本。 有关详细信息，请参阅 [启动屏幕组件](boot-screen-components.md)。

## <a name="related-topics"></a>相关主题
[启动屏幕组件](boot-screen-components.md)  



