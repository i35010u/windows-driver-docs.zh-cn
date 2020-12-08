---
title: 传感器和位置平台中的隐私和安全
description: 传感器和位置平台中的隐私和安全
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76616e17eed35a871cf52b858d8f8acdac81b595
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819087"
---
# <a name="privacy-and-security-in-the-sensor-and-location-platform"></a>传感器和位置平台中的隐私和安全

位置数据可能会违反用户的隐私，尤其是在信息标识特定人员的情况下。 街道地址或确定它的纬度和经度坐标被视为个人身份信息。 用户希望计算机软件保证这种信息的安全。 软件开发人员面临的挑战是寻找向用户提供所需功能的方法，而不违反其隐私。

## <a name="privacy-and-security-controls"></a>隐私和安全控制

Windows 中的传感器和位置平台提供以下功能，以帮助确保位置数据保持私密：

- 在 Windows 8 中，有三种类型的设置用于启用位置。 管理员可以为所有用户禁用位置，使用每个用户的设置来启用或禁用位置; 对于 UWP 应用，用户可以应用每个应用的位置设置。 默认情况下，每用户位置设置将关闭，直到用户通过 "控制面板" 提供访问数据的明确许可。 有关 Windows 8 中的位置设置的详细信息，请参阅 [位置感知](/uwp/api/Windows.Devices.Geolocation)。

- Windows 向用户提供泄露消息。 这些消息可帮助用户了解使用位置数据如何导致个人身份信息的泄露。

- 使用 Location API 的桌面应用程序可以调用 [**RequestPermissions**](/windows/win32/api/locationapi/nf-locationapi-ilocation-requestpermissions) 方法来打开系统对话框，该对话框会提示用户启用位置。

- 位置驱动程序使用传感器类扩展。 类扩展处理所有 i/o 请求，并确保只有具有用户权限的程序才能访问位置数据。

## <a name="keeping-user-data-private"></a>使用户数据保持私密

编写传感器驱动程序时，必须考虑用户隐私。 必须确保不会绕过传感器类扩展强制的隐私控制。 由于在用户授予权限之前可以检索某些属性，因此你必须确保你的驱动程序不会通过这些属性显示个人身份信息。 有关用户授予权限之前可用的属性的列表，请参阅 [**ISensorDriver：： OnGetProperties**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)。

## <a name="related-topics"></a>相关主题

[体系结构概述](../sensors/architecture-overview-for-sensor-drivers.md)  

[关于传感器类扩展](../sensors/about-the-sensor-class-extension.md)  

[位置感知](/uwp/api/Windows.Devices.Geolocation)
