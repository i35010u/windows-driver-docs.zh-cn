---
title: 要求
description: 要求
ms.assetid: d939a319-f321-455e-a34d-220a3faf6092
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ba9938a61ce6830ff53cd94fb9659602e8752b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380648"
---
# <a name="requirements"></a>要求


存储接收器驱动程序系统满足以下要求：

-   目标的系统包括 Windows XP、 Windows Vista 和 Windows 7。

-   对于 1667 UFD 设备必须保持与旧 UFD 设备的体验相一致的最终用户体验。

-   以前版本的 Windows XP 和 Vista 不依赖于 USBStor.sys 以外任何现有的系统二进制文件的修改。

-   存储接收器驱动程序系统实现，同时保持灵活性，作为一个平台，用于硬件供应商创新，1667年身份验证类解决方案。 所有第三方扩展点供用户模式代码通过供应商。

-   应支持第三方应用程序授予非排他性访问接收器的接收器驱动程序不进行声明。

-   支持声明对接收器的独占所有权的第三方 UMDF 驱动程序。 应用程序或其他驱动程序只能访问接收器通过此驱动程序。

-   第三方身份验证接收器驱动程序允许参与 act 授权工作流。 供应商创建实现的已发布的身份验证 DDI UMDF 驱动程序。

-   向后兼容性允许旧非 1667年设备参与否则保留为 1667年设备的平台体验。

-   存储接收器驱动程序系统管理根据 Windows 组策略在主机上的设备访问。 可能会在设备或个人信息藩篱的粒度级别应用策略。

-   在主机上的动态更改 ACL 为了提供安全的解决方案来保护对多用户或快速用户切换环境中的用户数据访问一次授予对单一的授权用户的独占 ACT 的访问权限。

 

 




