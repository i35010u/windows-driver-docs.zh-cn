---
title: 用户体验的 UEFI 固件更新
description: 本部分介绍如何在 UEFI 固件更新过程中实现基本的用户体验。
ms.assetid: 178F37B2-5CED-4AAF-8434-1C7532B36510
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea463536eec53fce1e6031448708183e3049a139
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541274"
---
# <a name="user-experience-for-uefi-firmware-updates"></a>用户体验的 UEFI 固件更新


本部分介绍如何在 UEFI 固件更新过程中实现基本的用户体验。

在更新固件的过程中，务必提供 visual 向最终用户通知正在处理更新。 通过用户使您习惯于典型其设备将启动进入 Windows 所需的时间。 如果出现固件更新扩展了此启动时则需要通知用户，应使用扩展的启动时间。 否则，用户可能会结束该设备无法启动或在启动过程中导致中断固件更新过程的用户手动重新启动系统，冻结。

若要避免这种情况下执行更新的固件必须通过显示简单的通知设备会被更新管理的用户体验。 这将重置用户的启动时间预期。 这种用户体验必须添加到现有 （和熟悉的用户） 启动屏幕。 显示的图形可能是 OEM 或主板制造商的徽标。

![标准 oem 启动屏幕](images/standardoembootscreen.png)

## <a name="user-experience"></a>用户体验


固件更新过程中显示必须向用户表明更新正在进行中。 目标为此用户体验 (UX) 是按如下所示：

-   显示必须非常简短并易于理解。
-   在系统上必须具有相同的外观和感觉，作为 Windows 操作系统版本。
-   必须传递以下信息：
    -   在此过程不干扰系统 （不从中拔出电源，等等。）。
    -   启动时可能会花费比预期长。
    -   更新过程是仍在进行中。

下图演示预期的外观和感觉的此用户体验。 显示了 OEM 图像 （在本示例虚构的 Contoso 徽标） 会在其他时间显示在系统引导时。 文本"，请稍候我们安装系统更新"指示关键系统组件更新正在进行。 用户已学会了，这意味着让设备执行操作必须执行的操作，请勿打扰则由于它可能需要一些时间。

![固件更新启动屏幕](images/firmwareupdatebootscreen.png)

## <a name="time-frame"></a>时间范围


在初始启动过程中系统将需要为用户提供标准的启动屏幕中，设备中按预期的那样。 但是一旦 Windows 引导加载程序检测到新的固件封装文件存在它将转换从正常启动屏幕为固件更新启动屏幕。 转换将包括 Windows 引导加载程序，该值指示更新在屏幕上显示本地化后的文本进行调入 UpdateCapsule() 之前正在进行。

用户体验需要的时间显示固件更新 UpdateCapsule() 调用之前已成功应用所有固件更新，然后在系统已关闭引导过程传递给 Windows 的时间。 如果在此期间需要额外的重新启动，然后必须进行的每次尝试继续显示固件更新启动屏幕，而不发生中断。 如果不可以这样做 （例如，GPU 固件已更新，或冷启动是必需的） 则必须进行的每次尝试以尽可能快地显示固件更新启动屏幕。 若要实现此要求，Windows 引导加载程序将提供固件位图的副本的本地化文本。 有关详细信息，请参阅[启动屏幕组件](boot-screen-components.md)。

## <a name="related-topics"></a>相关主题
[启动屏幕组件](boot-screen-components.md)  



