---
title: 生物识别驱动程序入门
description: 生物识别驱动程序入门
ms.assetid: 7f5dcac2-db0d-4ddd-9e57-886db324e38b
keywords:
- 生物识别驱动程序 WDK，有关生物识别驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b661f71a1c9c1e2568395d342975c47844f3797f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328393"
---
# <a name="getting-started-with-biometric-drivers"></a>生物识别驱动程序入门


Windows 生物识别框架 (WBF) 是 Windows 7 和更高版本的 Windows 中的泛型生物识别体系结构。

WBF 包含已知 Windows 生物识别驱动程序接口 (WBDI) 作为基于 IOCTL 的驱动程序接口，以及一个名为 Windows 生物识别服务 (WBS) 的 Windows 服务。 WBS 也称为 WinBio 服务。 WBDI 驱动程序从 WinBio 服务响应请求。 WBF 还包括 Windows 登录名的支持。

本文档介绍 WBDI。 Windows SDK 中单独说明了 WBS。

### <a name="span-idchoosingadrivermodelspanspan-idchoosingadrivermodelspanchoosing-a-driver-model"></a><span id="choosing_a_driver_model"></span><span id="CHOOSING_A_DRIVER_MODEL"></span>选择驱动程序模型

开发驱动程序能够与 Windows 生物识别驱动程序接口 (WBDI) 时必须做出的第一个选择是要使用的驱动程序模型。

Microsoft 建议 Ihv 通过使用 Windows 用户模式驱动程序框架开发生物识别设备驱动程序 (WUDF， 嘿 [UMDF](https://msdn.microsoft.com/library/windows/hardware/ff554928)) 和 WinUSB I/O 目标。

下图显示了如何基于 UMDF Windows 生物识别驱动程序接口 (WBDI) 驱动程序适用于 Windows 7 中的 Windows 生物识别框架 (WBF) 生物识别支持。 生物识别的所有操作都是都依靠客户端应用程序到 Windows 生物识别服务 (WBS)。 WBS 将请求发送到公开 WBDI 接口的生物识别设备驱动程序。

![说明生物识别内部驱动程序体系结构的关系图](images/bioarch.png)

在上图中，由供应商提供的生物识别设备驱动程序 DLL。

如果您不想要使用 UMDF 开发您的驱动程序，您还可以选择使用 KMDF 或 WDM 驱动程序，实现 WBDI，但这不是首选的驱动程序开发环境。

以下列表显示了不同的方式，您可以使用在最前面的最首选的方法和最不方便在底部，为 WBDI，开发驱动程序：

1.  与 WinUsb I/O 目标 UMDF

2.  UMDF 与 WinUsb 或自定义 KMDF I/O 目标上的自定义 KMDF 筛选器

3.  KMDF

4.  WDM （仅在绝对必要时）

本文档介绍如何使用 UMDF 编写基于 WBDI 的用户模式下 USB 生物识别驱动程序。

 

 





