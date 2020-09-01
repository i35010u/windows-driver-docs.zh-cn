---
title: Direct3D 功能级别的硬件支持
description: 显示设备硬件必须支持 Microsoft Direct3D 功能级别，如以下 Direct3D 主题 Direct3D feature levels10Level9 ID3D11Device Methods10Level9 ID3D11DeviceContext MethodsHardware Support for Direct3D 10Level9 FormatsIn （添加）中所述，用户模式驱动程序必须在 Direct3D 功能级别中公开某些功能9_1、9_2 和9_3，才能将 Direct3D 功能正确地公开给应用程序。 这些驱动程序主题列出了驱动程序必须公开所需的 Direct3D 9 capabilitiesRequired DXGI 格式的特定功能和显示格式。
ms.assetid: 32FF5A1F-FBD0-4273-BA21-85CC0E759DC0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 049544c4c7b20ed5e47fe3d3c883359d19bf954e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065604"
---
# <a name="hardware-support-for-direct3d-feature-levels"></a>Direct3D 功能级别的硬件支持


显示设备硬件必须支持 Microsoft Direct3D 功能级别，如以下 Direct3D 主题中所述：

-   [Direct3D 功能级别](/windows/desktop/direct3d11/overviews-direct3d-11-devices-downlevel-intro)

-   [10Level9 ID3D11Device 方法](/windows/desktop/direct3d11/d3d11-graphics-reference-10level9-device)

-   [10Level9 ID3D11DeviceContext 方法](/windows/desktop/direct3d11/d3d11-graphics-reference-10level9-context)

-   [Hardware Support for Direct3D 10Level9 Formats](/previous-versions/ff471324(v=vs.85))（Direct3D 10Level9 格式的硬件支持）

此外，用户模式驱动程序必须公开 Direct3D 功能级别 9 \_ 1、9 \_ 2 和 9 3 中的某些功能，才能 \_ 将 direct3d 功能正确地公开给应用程序。 这些驱动程序主题列出了驱动程序必须公开的特定功能和显示格式：
-   [必需的 Direct3D 9 功能](required-direct3d-9-capabilities.md)

-   [必需的 DXGI 格式](required-dxgi-formats.md)

 

