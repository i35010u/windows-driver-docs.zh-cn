---
title: 驱动程序技术概述
description: 本部分包含有关每项受支持的 Windows 驱动程序技术的信息。
ms.assetid: 1ef3e216-1322-42c3-b070-94cddfb2133c
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 73e98f4239743786319c1736b3b3169492e303d8
ms.sourcegitcommit: 76147255532f5fedacf591679e2604216e89365d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72021057"
---
# <a name="overview-of-driver-technologies"></a>驱动程序技术概述

有关开发驱动程序的常规信息，请参阅 [Windows 驱动程序入门](gettingstarted/index.md)和[编写第一个驱动程序](gettingstarted/writing-your-first-driver.md)。

大部分驱动程序技术信息对于所有 Windows 10 版本都是相同的。 如果你必须对特定版本的 Windows（例如 Windows 10 移动版）予以特殊考虑，我们已明确在每个技术领域中将这些考虑事项标注出来。

## <a name="universal-windows-drivers"></a>通用 Windows 驱动程序

可以创建在所有版本的 Windows 10 上均能运行的通用 Windows 驱动程序（该驱动程序使用一部分可供 Windows 驱动程序使用的接口）。 如果可能，请使用通用 Windows 驱动程序在多个设备上启用驱动程序部署。 有关如何生成、安装、部署和调试适用于 Windows 10 的通用 Windows 驱动程序的详细信息，请参阅[通用 Windows 驱动程序入门](develop/getting-started-with-universal-drivers.md)和[将驱动程序部署到测试计算机](develop/deploying-a-driver-to-a-test-computer.md)。

## <a name="device-drivers-and-windows-10-for-desktop-computers"></a>适用于台式计算机的设备驱动程序和 Windows 10

有关用来开发台式机驱动程序的工具的信息，请参阅[驱动程序开发工具](devtest/index.md)和[用于验证驱动程序的工具](devtest/tools-for-verifying-drivers.md)。 有关将驱动程序部署到台式机上的 Windows 10 的信息，请参阅[设备和驱动程序安装](install/index.md)。 有关排查驱动程序安装问题的信息，请参阅[驱动程序部署、测试和调试配置故障排除](develop/troubleshooting-configuration-of-driver-deployment--testing-and-debugging.md)。

## <a name="driver-technologies"></a>驱动程序技术

- [3D 打印设备](3dprint/index.md)
- [ACPI](acpi/index.md)
- [音频](audio/index.md)
- [电池驱动程序](battery/index.md)
- [生物识别驱动程序](biometric/index.md)
- [蓝牙驱动程序](bluetooth/index.md)
- [显示驱动程序](display/index.md)
- [文件系统驱动程序](ifs/index.md)
- [GNSS 驱动程序](gnss/index.md)
- [GPIO 驱动程序](gpio/index.md)
- [硬件通知](gpiobtn/index.md)
- [HID 驱动程序](hid/index.md)
- [IEEE 驱动程序](ieee/index.md)
- [图像处理设备驱动程序](image/index.md)
- [内核模式驱动程序技术](kernel/index.md)
- [移动宽带](mobilebroadband/index.md)
- [多功能设备驱动程序](multifunction/index.md)
- [NetAdapterCx](netcx/index.md)
- [网络驱动程序](network/index.md)
- [NFC 设备驱动程序](nfc/index.md)
- [并行端口驱动程序](parports/index.md)
- [合作伙伴应用程序开发](partnerapps/index.md)
- [PCI 驱动程序](pci/index.md)
- [PCMCIA 驱动程序](pcmcia/index.md)
- [服务点设备驱动程序](pos/index.md)
- [电源管理技术](powermeter/index.md)
- [打印设备驱动程序](print/index.md)
- [SD 卡总线驱动程序](sd/index.md)
- [传感器驱动程序](sensors/index.md)
- [串行端口驱动程序](serports/index.md)
- [智能卡设备驱动程序](smartcard/index.md)
- [简单外设总线 (SPB) 驱动程序](spb/index.md)
- [存储设备驱动程序](storage/index.md)
- [流媒体设备驱动程序](stream/index.md)
- [测试授权和执行框架 (TAEF)](taef/index.md)
- [通用串行总线 (USB)](usbcon/index.md)
- [Windows 设备测试框架 (WDTF)](wdtf/index.md)
- [Windows 硬件错误体系结构 (WHEA)](whea/index.md)
- [Windows 便携设备驱动程序](portable/index.md)

## <a name="related-sections"></a>相关章节

- [Windows 驱动程序入门](gettingstarted/index.md)
- [驱动程序开发工具](devtest/index.md)
- [Windows 硬件合作伙伴中心](dashboard/index.md)
