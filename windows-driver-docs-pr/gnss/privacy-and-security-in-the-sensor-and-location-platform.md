---
title: 传感器和位置平台中的隐私和安全
description: 传感器和位置平台中的隐私和安全
ms.assetid: 9defb163-4de6-46cc-b817-d3e6291137be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a168a743469b2ecfd45d66f34fd2f8c777334a28
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210797"
---
# <a name="privacy-and-security-in-the-sensor-and-location-platform"></a>传感器和位置平台中的隐私和安全

位置数据可能会违反用户的隐私，尤其是在信息标识特定人员的情况下。 街道地址或确定它的纬度和经度坐标被视为个人身份信息。 用户希望计算机软件保证这种信息的安全。 软件开发人员面临的挑战是寻找向用户提供所需功能的方法，而不违反其隐私。

## <a name="privacy-and-security-controls"></a>隐私和安全控制

Windows 中的传感器和位置平台提供以下功能，以帮助确保位置数据保持私密：

- 在 Windows 8 中，有三种类型的设置用于启用位置。 管理员可以为所有用户禁用位置，使用每个用户的设置来启用或禁用位置; 对于 UWP 应用，用户可以应用每个应用的位置设置。 默认情况下，每用户位置设置将关闭，直到用户通过 "控制面板" 提供访问数据的明确许可。 有关 Windows 8 中的位置设置的详细信息，请参阅[位置感知](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation)。

- Windows 向用户提供泄露消息。 这些消息可帮助用户了解使用位置数据如何导致个人身份信息的泄露。

- 使用 Location API 的桌面应用程序可以调用[**RequestPermissions**](https://docs.microsoft.com/windows/desktop/api/locationapi/nf-locationapi-ilocation-requestpermissions)方法来打开系统对话框，该对话框会提示用户启用位置。

- 位置驱动程序使用传感器类扩展。 类扩展处理所有 i/o 请求，并确保只有具有用户权限的程序才能访问位置数据。

## <a name="keeping-user-data-private"></a>使用户数据保持私密

编写传感器驱动程序时，必须考虑用户隐私。 必须确保不会绕过传感器类扩展强制的隐私控制。 由于在用户授予权限之前可以检索某些属性，因此你必须确保你的驱动程序不会通过这些属性显示个人身份信息。 有关用户授予权限之前可用的属性的列表，请参阅[**ISensorDriver：： OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)。

## <a name="related-topics"></a>相关主题

[体系结构概述](https://docs.microsoft.com/windows-hardware/drivers/sensors/architecture-overview)  

[关于传感器类扩展](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-the-sensor-class-extension)  

[位置感知](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation)  
