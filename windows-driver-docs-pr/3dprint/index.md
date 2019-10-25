---
title: 3D 打印机驱动程序设计指南
description: 本部分提供了有关 Windows 10 中的 3D 打印机驱动程序的信息。
ms.assetid: 3271C160-4253-48B5-A089-E026C6BAD3AF
ms.date: 09/20/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: c8d8b56e46e62b2da4a1b30643aed5afe8948fa8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824143"
---
# <a name="3d-printer-driver-design-guide"></a>3D 打印机驱动程序设计指南

本部分提供了有关 Windows 10 中的 3D 打印机驱动程序的信息。

Windows 10 中的 3D 打印提供了以下功能：

-   3D 制造设备的驱动程序模型

-   支持用于 3D 设备的 UWP 应用和扩展

-   作业后台打印和队列支持

-   为设备功能建模的关键字

-   用于使应用向 3D 打印机提交 3D 制造作业的 API

有关 Windows 10 中的 3D 打印的最新信息，请参阅以下资源：

-   [Windows 上的 3D 打印](https://go.microsoft.com/fwlink/p/?LinkId=627554)
-   [3D 硬件合作伙伴](https://go.microsoft.com/fwlink/p/?LinkId=627548)
-   [3D Builder 资源](https://go.microsoft.com/fwlink/p/?LinkId=627556)
-   [3D Builder 用户指南](https://go.microsoft.com/fwlink/p/?LinkId=627557)
-   [第 9 频道的 3D 打印博客](https://go.microsoft.com/fwlink/p/?LinkId=624519)

下载 [Windows 3D 打印 SDK](https://go.microsoft.com/fwlink/p/?LinkId=394375)，开始开发 3D 打印机的打印驱动程序。

## <a name="in-this-section"></a>本部分内容

-   [3D 打印合作伙伴加入指南](3d-partner-onboarding-guide.md)
-   [3D 打印机的 Microsoft 标准驱动程序](microsoft-standard-driver-for-3d-printers-.md)
-   [MS3DPrint 标准 G-Code 驱动程序](ms3dprint-standard-g-code-driver.md)
-   [3D 打印机自定义 USB 接口支持](3d-printer-custom-usb-interface.md)
-   [3D 打印示例 WSD 应用](3d-printing-sample-wsd-app.md)
-   [在设备上启用 WSPrint 2.0](enabling-wsprint-on-a-device.md)
-   [3D 制造的打印架构关键字](print-schema-keywords-for-3d-manufacturing.md)
-   [3D 硬件合作伙伴](3d-printing-partners.md)

## <a name="related-sections"></a>相关章节

-   [打印 DDI 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print)
