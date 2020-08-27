---
description: BIOS/UEFI 测试可验证控制器到操作系统的 USB 启动和切换。
title: 对 MUTT 设备进行 BIOS/UEFI 测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 363fdb780ff08bb2aadbd54fae24604403ae2959
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968982"
---
# <a name="biosuefi-testing-with-the-mutt-devices"></a>对 MUTT 设备进行 BIOS/UEFI 测试


BIOS/UEFI 测试可验证控制器到操作系统的 USB 启动和切换。

## <a name="usb-boot-configurations"></a>USB 启动配置


在 USB 2.0 (EHCI) 和 USB 3.0 (xHCI) 控制器上执行这些测试，其中每个主 USB 媒体类型 (USB 2.0 机器人、USB 3.0 机器人、USB 3.0 UASP 和 USB DVD) 。

每个方案的预期结果是以下事件之一：

-   当用户输入正确的密钥序列时，连接的键盘允许用户进入配置模式 (BIOS/UEFI 配置) 。
-   未按下键序列时从 USB 设备启动。

这些方案假设 BIOS/UEFI 配置为从 USB 启动。 每个连接的 USB 存储设备都已使用 Windows 可识别的文件系统进行格式化。

-   USB 启动方案1– USB 3.0 集线器

    ![usb 3.0 集线器](images/fig16-usb-bootbehind30hub.png)

-   USB 启动方案2– USB 2.0 集线器

    ![usb 2.0 集线器](images/fig17-usb-bootbehind20hub.png)

-   USB 启动方案3–根端口

    ![启动根端口](images/fig18-usb-bootrootport.png)

## <a name="non-usb-boot-configurations"></a>非 USB 启动配置


在这种情况下，假定不存在附加到系统的 USB 可启动媒体，或者 BIOS/UEFI 配置为不从 USB 启动。 使用连接的 USB 键盘/鼠标进入配置模式是预期方案，此处未列出。

![usb 控制器切换](images/fig19-usb-controllerhandoff.png)

此方案的预期结果是，在启动到操作系统并运行标准 MUTT 测试后，SuperMUTT Pack 和 MUTT Pack 都可以正常工作，并可正常运行。 验证测试设备后，系统应在每个系统恢复后 (S3、S4) 执行每个受支持的系统电源状态，并验证 MUTT 测试设备是否仍然正常工作。 每次恢复事件后运行 MUTT 测试。

## <a name="related-topics"></a>相关主题
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



