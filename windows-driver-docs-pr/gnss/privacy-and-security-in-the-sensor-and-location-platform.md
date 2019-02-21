---
title: 隐私和安全的传感器和位置平台
description: 隐私和安全的传感器和位置平台
ms.assetid: 9defb163-4de6-46cc-b817-d3e6291137be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aec410cea8c30ef7014561d3e147e6f22dd0ce7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541974"
---
# <a name="privacy-and-security-in-the-sensor-and-location-platform"></a>隐私和安全的传感器和位置平台


位置数据可以违反用户的隐私，尤其是当信息标识特定人员。 街道地址或纬度和经度坐标，以确定它，被视为个人身份信息。 用户期望计算机软件，以使此类信息安全。 软件开发人员面临的挑战是寻找机会向用户授予他们希望和需要而不违反他们的隐私的功能。

### <a name="privacy-and-security-controls"></a>隐私和安全控制

在 Windows 中的传感器和位置平台提供了以下功能，可帮助确保位置数据隐私：

-   在 Windows 8 中，用于启用位置有三种类型的设置。 管理员可以禁用所有用户，每个用户设置来启用或禁用的位置，位置的设置和用户可以将每个应用位置设置应用于 UWP 应用。 默认情况下，每个用户位置设置直至用户提供明确同意通过控制面板访问数据关闭状态。

    在 Windows 8 中的位置设置的详细信息，请参阅[位置感知](https://msdn.microsoft.com/library/windows/apps/br225603)。

-   Windows 向用户提供泄露消息。 这些消息帮助用户了解如何使用位置数据可能会导致泄露个人身份信息。

-   使用位置 API 的桌面应用程序可以调用[ **RequestPermissions** ](https://msdn.microsoft.com/library/windows/desktop/dd317635)方法打开一个系统对话框，提示用户启用位置。

-   位置驱动程序使用传感器类扩展。 类扩展处理所有 I/O 请求，并可确保仅具有用户权限的程序可以访问位置数据。

### <a name="keeping-user-data-private"></a>保留用户数据私有

当您编写传感器驱动程序时，您必须考虑用户隐私。 您必须确保不绕过传感器类扩展由强制实施的隐私控件。 由于用户已授予的权限之前，可以检索某些属性，因此必须确保您的驱动程序不会泄露个人身份信息通过这些属性。 用户已授予的权限之前，将提供的属性的列表，请参阅[ **ISensorDriver::OnGetProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545610)。

### <a name="additional-resources"></a>其他资源

查看以下资源以帮助您开发软件，保护用户隐私。

-   [开发软件产品和服务的隐私准则](https://go.microsoft.com/fwlink/p/?linkid=237149)

-   [TechNet 安全开发人员中心](https://go.microsoft.com/fwlink/p/?linkid=237150)

## <a name="related-topics"></a>相关主题
[体系结构概述](https://msdn.microsoft.com/library/windows/hardware/ff545400)  
[有关传感器类扩展](https://msdn.microsoft.com/library/windows/hardware/ff545398)  
[位置感知](https://msdn.microsoft.com/library/windows/apps/br225603)  



