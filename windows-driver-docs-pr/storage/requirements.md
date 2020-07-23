---
title: 接收器驱动程序系统要求
description: 描述存储接收器驱动程序系统满足的要求
ms.assetid: d939a319-f321-455e-a34d-220a3faf6092
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea45873dbf545ea664e4065c8043ea73f2f36ef3
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949737"
---
# <a name="silo-driver-system-requirements"></a>接收器驱动程序系统要求

存储接收器驱动程序系统满足以下要求：

- 目标系统包括 Windows XP、Windows Vista 和 Windows 7。

- 1667 UFD 设备的最终用户体验必须与旧 UFD 设备的体验保持一致。

- 以前版本的 Windows XP 和 Vista 不依赖于除 USBStor.sys 之外的任何现有系统二进制文件的修改。

- 存储接收器驱动程序系统启用1667身份验证类解决方案，同时保持对硬件供应商创新的平台。 所有第三方扩展点通过用户模式代码提供给供应商。

- 如果第三方应用程序被授予了对思洛存储器驱动程序未规定的非独占访问权，则应该支持。

- 支持声明接收器的独占所有权的第三方 UMDF 驱动程序。 应用程序或其他驱动程序只能通过此驱动程序访问接收器。

- 第三方身份验证接收器驱动程序允许参与操作的授权工作流。 供应商创建一个 UMDF 驱动程序来实现发布的身份验证 DDI。

- 向后兼容性允许传统的非1667设备参与其他为1667设备预留的平台体验。

- 存储接收器驱动程序系统根据 Windows 组策略管理主机上的设备访问。 策略可以应用于设备或每个接收器级别的粒度级别。

- 主机上动态变化的 ACL 向单个授权用户授予独占操作访问权限，以便提供安全的解决方案来保护对多用户或快速用户交换机环境中的用户数据的访问。
