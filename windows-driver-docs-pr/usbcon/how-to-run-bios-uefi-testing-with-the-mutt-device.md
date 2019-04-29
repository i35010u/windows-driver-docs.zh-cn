---
Description: BIOS/UEFI 测试验证 USB 启动，并且切换到操作系统的控制器。
title: 对 MUTT 设备进行 BIOS/UEFI 测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 624a3ab4d1873b409dad699d68b2ea4232e1408e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366068"
---
# <a name="biosuefi-testing-with-the-mutt-devices"></a>对 MUTT 设备进行 BIOS/UEFI 测试


BIOS/UEFI 测试验证 USB 启动，并且切换到操作系统的控制器。

## <a name="usb-boot-configurations"></a>USB 启动配置


在 USB 2.0 (EHCI) 和与每个主要的 USB 媒体类型 （USB 2.0 智能机器人应用程序、 USB 3.0 智能机器人应用程序和 USB 3.0 UASP 和 USB DVD） 的 USB 3.0 (xHCI) 控制器上执行这些测试。

每个方案的预期的结果是以下事件之一：

-   当用户输入正确的按键顺序时，附加的键盘，则允许用户进入配置模式 (BIOS / UEFI 配置)。
-   从 USB 设备的按键顺序未按下时启动。

这些情况假定 BIOS /UEFI 已配置为从 USB 启动。 每个附加的 USB 存储设备已识别的 Windows 文件系统格式。

-   USB 启动方案 1 – USB 3.0 集线器

    ![usb 3.0 集线器](images/fig16-usb-bootbehind30hub.png)

-   USB 启动方案 2 – USB 2.0 集线器

    ![usb 2.0 集线器](images/fig17-usb-bootbehind20hub.png)

-   USB 启动方案 3 – 根端口

    ![启动根端口](images/fig18-usb-bootrootport.png)

## <a name="non-usb-boot-configurations"></a>非 USB 启动配置


在此方案中，假定任一 USB 可启动媒体中没有附加到系统或从 USB BIOS/UEFI 配置为不启动。 进入配置模式下使用连接的 USB 键盘 / 鼠标是此处未列出的预期的方案。

![usb 控制器切换](images/fig19-usb-controllerhandoff.png)

此方案中的预期的结果将是 SuperMUTT 包和 MUTT 包的功能和操作后在操作系统启动和运行标准 MUTT 测试。 验证测试设备后，系统应执行每个受支持的系统电源状态 （S3、 S4，等），并验证每个系统恢复后 MUTT 测试设备保持正常运行。 每个恢复事件之后运行 MUTT 测试。

## <a name="related-topics"></a>相关主题
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



