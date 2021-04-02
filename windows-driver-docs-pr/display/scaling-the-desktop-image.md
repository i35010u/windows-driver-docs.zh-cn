---
title: 缩放桌面映像
description: 描述桌面图像缩放的工作原理
keywords:
- 连接显示 WDK Windows 7 显示、CCD 概念、缩放桌面映像
- 连接显示 WDK Windows Server 2008 R2 显示、CCD 的概念、缩放桌面映像
- 配置显示 WDK Windows 7 显示、CCD 概念、缩放桌面映像
- 配置显示 WDK Windows Server 2008 R2 显示、CCD 概念、缩放桌面映像
- CCD 概念 WDK Windows 7 显示，缩放桌面映像
- CCD 概念 WDK Windows Server 2008 R2 显示，缩放桌面映像
- 缩放桌面图像 WDK Windows 7 显示
- 缩放桌面映像 WDK Windows Server 2008 R2 显示器
ms.date: 03/31/2021
ms.localizationpriority: medium
ms.openlocfilehash: 589171877edd973ceba8c4e05c33bc9c443d7181
ms.sourcegitcommit: 83a11e69f7b175011d032a179e4cfa6d5ede9ac2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2021
ms.locfileid: "106113628"
---
# <a name="scaling-the-desktop-image"></a>缩放桌面映像

本主题仅适用于 windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

## <a name="how-scaling-works"></a>缩放的工作原理

调用方可以使用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 连接和配置显示 (CCD) 函数将桌面映像缩放到监视器：

* 如果桌面和监视器使用相同的分辨率，则不需要 **SetDisplayConfig** 将桌面映像缩放到监视器。 此 **SetDisplayConfig** 操作称为 " *标识缩放*"。
* 如果桌面和监视器分辨率不同， **SetDisplayConfig** 将应用以下一种缩放类型。 监视器分辨率由 [**DISPLAYCONFIG_TARGET_MODE**](/windows/win32/api/wingdi/ns-wingdi-displayconfig_target_mode) 结构定义。

  * **居中缩放**

    居中缩放是一种模式，在该模式下桌面显示在监视器上，根本不进行任何缩放。 当 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 应用居中缩放时，黑色带区可能在桌面的上方和下方可见。 下图显示了中心缩放。

    ![阐释中心缩放的图](images/ccd-center-scale.png)

  * **延伸缩放**

    拉伸缩放是一种模式，在该模式下，桌面在监视器上水平和垂直拉伸，以确保使用整个显示。 当 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 应用延伸缩放时，桌面上方和下方不会显示黑色带区。 但是，桌面可能会失真。 下图显示了延伸缩放。

    ![演示拉伸缩放的图](images/ccd-stretch-scale.png)

  * **纵横比-保留延伸**

    纵横比-保留延伸缩放是一种模式，在该模式下，桌面会在保持纵横比的同时水平和垂直拉伸。 当 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 应用纵横比保留延伸缩放时，黑色带区可能会显示在桌面的 *上方和下方* 或 *左侧或右侧* 。 但是，黑色带区不能同时 *显示在桌面的**上方和下方*。 由于用户需要使用这种类型的缩放，因此 **SetDisplayConfig** 会将此类型的缩放作为默认值应用。 下图显示了纵横比，其中保留了延伸缩放。

    ![图说明了纵横比-保留延伸比例](images/ccd-arpstretch-scale.png)

缩放取决于用于路径的源和目标模式。 此外，调用方可以调用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 而无需指定目标模式信息 (即，将 *modeInfoArray* 参数设置为可选，并且可以将其设置为 **NULL**) 。 这意味着调用方通常无法预测 **SetDisplayConfig** 是否必须执行任何缩放。 此外，不存在 API 来获取图形适配器支持的缩放类型的完整列表。 [**EnumDisplaySettings**](/windows/win32/api/winuser/nf-winuser-enumdisplaysettingsa) Win32 函数返回在调用方请求 Windows 7 缩放类型时 *lpDevMode* 参数指向的 **DEVMODE** 结构的 **dmDisplayFixedOutput** 成员中 DMDFO_DEFAULT。

调用方传递给 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 的缩放是缩放意向，而不是显式请求来执行缩放操作。 如果需要缩放 (例如，源和目标解析) 不同， **SetDisplayConfig** 将使用调用方提供的缩放。 如果不支持所提供的缩放， **SetDisplayConfig** 将使用图形适配器的默认缩放。 当调用方传递给 **SetDisplayConfig** 的源和目标解析相同时， **SetDisplayConfig** 始终设置标识缩放。

## <a name="scaling-requests"></a>缩放请求数

下表显示了不同的 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 缩放请求，并标识了在以下子节中找到的表中使用的缩写命名法。  有关 DISPLAYCONFIG_SCALING_ *XXX* 值的定义，请参阅 [DISPLAYCONFIG_SCALING](/windows/win32/api/wingdi/ne-wingdi-displayconfig_scaling) 。

| 缩放请求 | 下表中使用的缩写命名法 |
| --------------- | ------- |
| DISPLAYCONFIG_SCALING_IDENTITY | DC_IDENTITY  |
| DISPLAYCONFIG_SCALING_CENTERED | DC_CENTERED  |
| DISPLAYCONFIG_SCALING_STRETCHED |DC_STRETCHED  |
| DISPLAYCONFIG_SCALING_ASPECTRATIOCENTEREDMAX | DC_ASPECTRATIOCENTEREDMAX  |
| DISPLAYCONFIG_SCALING_CUSTOM | DC_CUSTOM  |
| DISPLAYCONFIG_SCALING_PREFERRED | DC_PREFERRED  |
| 适配器默认缩放值。 目前，tablet 系统上的默认值为 "拉伸"。 在支持 [Windows 显示驱动程序模型](windows-vista-display-driver-model-design-guide.md)  (WDDM) 的非平板系统上，默认值是由驱动程序定义的。 在具有支持 WDDM 的图形适配器的非平板系统上， [新的功能为 Windows 7](../what-s-new-in-driver-development.md)，默认值为 DC_ASPECTRATIOCENTEREDMAX。 | AdapterDefault  |
| 当前连接的监视器的数据库的缩放值 | DatabaseValue |

### <a name="setdisplayconfig-scaling-requests"></a>SetDisplayConfig 缩放请求

下表显示了保存在数据库中的值和实际设置的值，其中：

* "设置 (相同的) " 和 "存储 (相同) " 是在生成的源模式和目标模式具有相同的分辨率时设置和存储值
* "设置 (不同的) " 和 "应用商店 (不同) " 是在生成的源模式和目标模式具有不同的分辨率时设置和存储值

| 传递给 SetDisplayConfig 的缩放标志 | 设置 (相同)  | 将 (存储)  | 设置 (不同的)  | 设置 (不同的)  |
| - | - | - | - | - |
| 当前不在 Db 中的配置 DC_IDENTITY | DC_IDENTITY | AdapterDefault | AdapterDefault | AdapterDefault |
| 在 Db 中 DC_IDENTITY 当前配置 | DC_IDENTITY | DatabaseValue | DatabaseValue |DatabaseValue |
| DC_CENTERED | DC_IDENTITY | DC_CENTERED | DC_CENTERED | DC_CENTERED |
| DC_STRETCHED | DC_IDENTITY | DC_STRETCHED | DC_STRETCHED | DC_STRETCHED |
| 具有 Windows 7 功能驱动程序的 WDDM 上的 DC_ASPECTRATIOCENTEREDMAX |DC_IDENTITY | DC_ASPRATIOMAX | DC_ASPRATIOMAX | DC_ASPRATIOMAX |
| WDDM 驱动程序上的 DC_ASPECTRATIOCENTEREDMAX | DC_IDENTITY | AdapterDefault | AdapterDefault | AdapterDefault |
| 在具有 Windows 7 功能驱动程序的 WDDM 上 DC_CUSTOM 在路径上支持自定义缩放 | DC_CUSTOM | DC_CUSTOM | DC_CUSTOM | DC_CUSTOM |
| 在具有 Windows 7 功能驱动程序的 WDDM 上 DC_CUSTOM，该驱动程序不支持路径上的自定义缩放 | DC_IDENTITY | AdapterDefault | AdapterDefault | AdapterDefault |
| WDDM 驱动程序上的 DC_CUSTOM | DC_IDENTITY | AdapterDefault | AdapterDefault | AdapterDefault |
| 当前不在 Db 中的配置 DC_PREFERRED | DC_IDENTITY | AdapterDefault | AdapterDefault | AdapterDefault |
| 在 Db 中 DC_PREFERRED 当前配置 | DC_IDENTITY | DatabaseValue | DatabaseValue |DatabaseValue |

### <a name="legacy-changedisplaysettingsex-scaling-requests"></a>旧式 ChangeDisplaySettingsEx 缩放请求

下表显示了调用方可传递给旧  [**ChangeDisplaySettingsEx**](/windows/win32/api/winuser/nf-winuser-changedisplaysettingsexa) API 的缩放如何映射到缩放集，其中：

* "设置 (相同的) " 和 "存储 (相同) " 是在生成的源模式和目标模式具有相同的分辨率时设置和存储值
* "设置 (不同的) " 和 "应用商店 (不同) " 是在生成的源模式和目标模式具有不同的分辨率时设置和存储值

| 传递给 ChangeDisplaySettingsEx 的缩放标志 | 设置 (相同)  | 将 (存储)  | 设置 (不同的)  | 设置 (不同的)  |
| - | - | - | - | - |
| DMDFO_DEFAULT 当前配置不在 CCD 数据库中 | DC_IDENTITY | AdapterDefault | AdapterDefault | AdapterDefault |
| 在 CCD 数据库中用当前配置 DMDFO_DEFAULT | DC_IDENTITY | DatabaseValue | DatabaseValue |DatabaseValue |
| DMDFO_STRETCH| DC_IDENTITY | DC_STRETCHED | DC_STRETCHED | DC_STRETCHED |
| DMDFO_CENTER | DC_IDENTITY | DC_CENTERED | DC_CENTERED | DC_CENTERED |
| DM_DISPLAYFIXEDOUTPUT 未设置，当前配置不在 CCD 数据库中 | DC_IDENTITY | AdapterDefault | AdapterDefault | AdapterDefault |
| DM_DISPLAYFIXEDOUTPUT 未设置，CCD 数据库中的当前配置 | DC_IDENTITY | DatabaseValue | DatabaseValue |DatabaseValue |

### <a name="legacy-enumdisplaysettings-scaling-translation"></a>旧式 EnumDisplaySettings 缩放翻译

下表显示了如何从 [**EnumDisplaySettings**](/windows/win32/api/winuser/nf-winuser-enumdisplaysettingsa)转换和返回显示配置缩放。

| 当前活动缩放 | 从旧的 EnumDisplaySettings (ENUM_CURRENT_SETTINGS 返回的 GDI 缩放值)  |
| - | - |
| DC_IDENTITY  | DMDFO_DEFAULT |
| DC_CENTERED  | DMDFO_CENTER |
| DC_STRETCHED  | DMDFO_STRETCH |
| DC_ASPRATIOMAX  | DMDFO_DEFAULT |
| DC_CUSTOM  | DMDFO_DEFAULT |
| DC_PREFERRED  | DMDFO_DEFAULT |

## <a name="directx-games-and-scaling"></a>DirectX 游戏和缩放

Microsoft DirectX 9L 及更早版本要求应用程序始终调用 [**ChangeDisplaySettingsEx**](/windows/win32/api/winuser/nf-winuser-changedisplaysettingsexa)函数，而不 DM_DISPLAYFIXEDOUTPUT 在 *lpDevMode* 参数指向的 DEVMODE 结构的 **dmFields** 成员中设置。 DirectX 10 和更高版本的运行时允许应用程序选择这些应用程序传递给 **ChangeDisplaySettingsEx** 的缩放。 下表显示了将缩放值映射到传递给 **ChangeDisplaySettingsEx** 的缩放标志。

| DXGI 翻转链缩放值 | 传递给 ChangeDisplaySettingsEx 的缩放标志 |
| - | - |
| DXGI_MODE_SCALING_UNSPECIFIED  | DMDFO_DEFAULT、DMDFO_CENTER 或 DMDFO_STRETCH。 应用程序使用的缩放取决于多个因素，包括当前桌面缩放和驱动程序公开的模式列表。 |
| DXGI_MODE_SCALING_CENTERED  | DMDFO_CENTER |
| DXGI_MODE_SCALING_STRETCHED  | DMDFO_STRETCH |

通过将此信息与前面的缩放表结合使用，可以确定 DirectX 应用程序所需的缩放。
