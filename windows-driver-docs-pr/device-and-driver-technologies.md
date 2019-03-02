---
title: 设备和驱动程序技术
description: 本部分包含有关每项受支持的 Windows 驱动程序技术的信息。
ms.assetid: 1ef3e216-1322-42c3-b070-94cddfb2133c
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8be95023093318da17e9f84a643d181696b879c8
ms.sourcegitcommit: 132f0c2d827982b808053ecd3b4d137a2883cca1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "56518560"
---
# <a name="device-and-driver-technologies"></a>设备和驱动程序技术

本部分包含有关每项受支持的 Windows 驱动程序技术的信息。 大部分驱动程序技术信息对于所有 Windows 10 版本都是相同的。 当必须对特定版本的 Windows（例如 Windows 10 移动版）进行特殊考虑时，我们明确在每个技术领域中将这些事项标注出来。 有关开发驱动程序的常规信息，请参阅[编写你的第一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-your-first-driver)。

## <a name="universal-windows-drivers"></a>通用 Windows 驱动程序

你可以创建可在所有版本的 Windows 10 上运行的通用 Windows 驱动程序（一个使用可供 Windows 驱动程序使用的部分接口的驱动程序）。 如果可能，请使用通用 Windows 驱动程序在多个设备上启用驱动程序部署。 有关如何生成、安装、部署和调试适用于 Windows 10 的通用 Windows 驱动程序的详细信息，请参阅[通用 Windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)和[将驱动程序部署到测试计算机](https://docs.microsoft.com/windows-hardware/drivers/develop/deploying-a-driver-to-a-test-computer)。

## <a name="device-drivers-and-windows10-for-desktop-computers"></a>适用于台式计算机的设备驱动程序和 Windows 10

有关用来开发台式机驱动程序的工具的信息，请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/
)和[用于验证驱动程序的工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-verifying-drivers)。 有关为台式机上的 Windows 10 部署驱动程序的信息，请参阅[分发驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/develop/distributing-a-driver-package-win8)。 有关对驱动程序配置进行疑难解答的信息，请参阅[对驱动程序配置进行疑难解答](https://docs.microsoft.com/windows-hardware/drivers/develop/troubleshooting-configuration-of-driver-deployment--testing-and-debugging)。

## <a name="device-drivers-and-windows10-mobile"></a>设备驱动程序和 Windows 10 移动版

Windows 10 移动版针对移动设备的独特需求进行了优化。 可以使用程序包将驱动程序添加到移动设备上的 OS，不需要将驱动程序复制到桌面或使用“设备管理器”安装它。 有关使用程序包的详细信息，请参阅[创建移动程序包](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))。 此外，移动设备上的驱动程序需要使用特定的过程进行签名，以维护 OS 的完整性，如[移动代码签名](https://docs.microsoft.com/previous-versions/windows/hardware/code-signing/dn756634(v=vs.85))中所述。 有关将设备驱动程序添加到手机等移动设备的演练，请参阅[将驱动程序添加到测试映像](https://docs.microsoft.com/previous-versions//mt131832(v=vs.85))。

## <a name="in-this-section"></a>本部分内容

- [3D 打印设备](3dprint/index.md)
- [高级配置和电源接口 (ACPI)](acpi/index.md)
- [音频设备](audio/index.md)
- [电池设备](battery/index.md)
- [生物识别设备](biometric/index.md)
- [蓝牙设备](bluetooth/index.md)
- [显示设备（适配器和监视器）](display/index.md)
- [GNSS 设备（位置）](gnss/index.md)
- [硬件通知](gpiobtn/index.md)
- [人工输入设备 (HID)](hid/index.md)
- [图像处理设备（扫描仪）](image/index.md)
- [可安装的文件系统驱动程序](ifs/index.md)
- [内核模式驱动程序技术](kernel/index.md)
- [移动宽带](mobilebroadband/index.md)
- [多功能设备驱动程序](multifunction/index.md)
- [NetAdapterCx 驱动程序](netcx/index.md)
- [网络驱动程序](network/index.md)
- [NFC 设备驱动程序](nfc/index.md)
- [并行端口驱动程序](parports/index.md)
- [合作伙伴应用程序开发](partnerapps/index.md)
- [PCI 驱动程序](pci/index.md)
- [PCMCIA 驱动程序](pcmcia/index.md)
- [服务点 (POS) 驱动程序](pos/index.md)
- [电源管理技术](powermeter/index.md)
- [打印设备](print/index.md)
- [SD 卡总线驱动程序](sd/index.md)
- [传感器驱动程序](sensors/index.md)
- [串行端口驱动程序](serports/index.md)
- [智能卡读卡器设备驱动程序](smartcard/index.md)
- [简单外设总线 (SPB) 驱动程序](spb/index.md)
- [存储设备驱动程序](storage/index.md)
- [流媒体设备驱动程序](stream/index.md)
- [测试授权和执行框架 (TAEF)](taef/index.md)
- [通用串行总线 (USB)](usbcon/index.md)
- [Windows 设备测试框架 (WDTF)](wdtf/index.md)
- [Windows 硬件错误体系结构 (WHEA)](whea/index.md)
