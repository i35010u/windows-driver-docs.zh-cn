---
title: 生物识别驱动程序入门
description: 生物识别驱动程序入门
ms.assetid: 7f5dcac2-db0d-4ddd-9e57-886db324e38b
keywords:
- 生物识别驱动程序 WDK，关于生物识别驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f20584f3a329436fa618850bdc9a4edbb5ad37d
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095893"
---
# <a name="getting-started-with-biometric-drivers"></a>生物识别驱动程序入门


在 Windows 7 和更高版本的 Windows 中，Windows Biometric Framework (WBF) 是通用的生物识别体系结构。

WBF 包含一种基于 IOCTL 的驱动程序接口（称为 Windows 生物识别驱动程序接口） (WBDI) ，以及一个名为 Windows 生物识别服务 (WBS) 的 Windows 服务。 WBS 也称为 WinBio 服务。 WBDI 驱动程序响应来自 WinBio 服务的请求。 WBF 还包括 Windows 登录支持。

本文档介绍了 WBDI。 WBS 在 Windows SDK 中单独记录。

### <a name="span-idchoosing_a_driver_modelspanspan-idchoosing_a_driver_modelspanchoosing-a-driver-model"></a><span id="choosing_a_driver_model"></span><span id="CHOOSING_A_DRIVER_MODEL"></span>选择驱动程序模型

开发驱动程序以使用 Windows 生物识别驱动程序界面时，必须做出第一种选择 (WBDI) 是要使用的驱动程序模型。

Microsoft 建议 Ihv 使用 Windows 用户模式驱动程序框架 (WUDF （也称为 [UMDF](/previous-versions/ff554928(v=vs.85))) 和 WinUSB i/o 目标）来开发生物识别设备驱动程序。

下图显示了如何 (WBDI) 驱动程序的基于 UMDF 的 Windows 生物识别驱动程序接口适用于 Windows 7 中 Windows Biometric Framework (WBF) 生物识别支持。 所有生物识别操作都由使用 Windows 生物识别服务的客户端应用程序驱动 (WBS) 。 WBS 向公开 WBDI 接口的生物识别设备驱动程序发送请求。

![说明生物识别内部驱动程序体系结构的关系图](images/bioarch.png)

在上图中，供应商提供生物识别设备驱动程序 DLL。

如果不想使用 UMDF 来开发驱动程序，也可以选择使用 KMDF 或 WDM 驱动程序实现 WBDI，但这不是首选的驱动程序开发环境。

以下列表显示了为 WBDI 开发驱动程序的不同方式，最喜欢的方法是顶部，最小优先级最低：

1.  具有 WinUsb i/o 目标的 UMDF

2.  在 WinUsb 或自定义 KMDF i/o 目标上使用自定义 KMDF 筛选器的 UMDF

3.  KMDF

4.  仅当绝对必要时才 (WDM) 

本文档介绍了如何使用 UMDF 来编写基于 WBDI 的用户模式 USB 生物驱动程序。

 

