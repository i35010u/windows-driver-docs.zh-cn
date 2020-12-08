---
title: MB 标识变形解决方案详细信息
description: 描述 MB 标识变形设备的配置要求和兼容 Id
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36b471e9f5451f9deaa03bdfcb1a245cd1c24b4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815951"
---
# <a name="mb-identity-morphing-solution-details"></a>MB 标识变换解决方案详细信息


## <a name="configuration-requirements"></a>配置要求


需要维护跨 Windows 8 转换的函数顺序。 例如，如果 MBIM 是 Windows 8 配置中的第三个函数，则它也应该是 NCM-2.0-配置中的第三个函数。

Windows 7-配置

Windows 7 配置应为变形设备中的第一个配置。 此配置应将大容量存储函数作为函数之一。 Windows 8 不会选择此配置。 在 windows 7 和更早版本的 Windows 中，Windows 7 配置是选择的默认配置。 此配置用于公开 USB 大容量存储功能，其中 Ihv 放置其驱动程序包，使用户能够安装 IHV 的驱动程序。

Windows 8-配置

Windows 7 配置会将 MBIM 函数公开为加载 MBCD 的函数之一。 在 Windows 8 中，此配置的值在返回到 USBCCGP 的 subCompatibleID 值中使用。 USBCCGP 在加载时选择此配置。 Windows 8 配置应为配置2、3或4。 不支持将其他配置作为 Windows-8-配置。 此配置还会将大容量存储函数公开为允许用户安装 IHV 的驱动程序包的第一个功能。

IHV-NCM-2.0-配置

IHV-NCM-2.0-配置公开了特定于 IHV 的功能，以及 MBIM 和大容量存储功能。 Windows 未设置或使用此配置。 在用户安装后，IHV 软件可以平滑此配置。 请注意，此配置中的函数顺序应与在 Windows-8-配置中的顺序相同。 尽管可以向 Windows 8 配置中添加额外的函数，但应以相同的顺序保留现有函数。

IHV-NCM-1.0-配置

IHV-NCM-1.0-配置公开了特定于 IHV 的功能，以及 NCM 1.0 和大容量存储功能。 Windows 8 未设置或使用此配置。 此配置仅在用户安装了 IHV 软件之后用于 Windows 7 和更早版本的 Windows 中。 IHV 软件将变形设备从 Windows 7 配置推移到此配置。

## <a name="compatible-ids"></a>兼容 Id


兼容 Id 是8个字符或更小的字符串，用于指示驱动程序加载到 Windows 的首选项。 设备可以通过使用 Microsoft OS 描述符来定义兼容的 Id。 兼容的和 subcompatible 的 Id 适用于各个函数。 每个配置可以具有一组单独的兼容 Id，这些 Id 映射到该配置内的函数集。 尽管兼容 Id 和 subcompatible Id 适用于单个函数，但在未选择任何配置时，变形设备可以具有单个兼容 ID。 此兼容和 subcompatible ID 在逻辑上适用于整个变形设备。

**正在加载 USBCCGP**

在 Windows 8 中，需要使用 USBCCGP 驱动程序在变形设备上自动选择 Windows 8 配置。

若要加载 USBCCGP 驱动程序，在变形设备上未选择任何配置时，变形设备需要报告以下兼容和 subcompatible Id：

-   如果变形设备使用 IADs 将接口分组到函数中，则应将兼容 ID 报告为 "ALTRCFG"，并将 subcompatible ID 报告为 Windows 8 配置的编号。
-   如果变形设备使用 WCM Ufd 将接口分组到函数中，则应将兼容 ID 报告为 "WMCALTR"，并将 subcompatible ID 报告为 Windows 8 配置的编号。

例如，如果 Windows 8 配置为配置3，则在这两种情况下，subcompatible ID 将为 "3"。

**变形兼容 Id**

在 USB 设备枚举过程中，如果未在变形设备上选择 "配置"，USBHUB 将在变形设备中查询兼容 ID。 变形设备应返回用于加载 USBCCGP 的兼容 ID 和 subcompatible ID，如 [MB 标识变形解决方案概述](mb-identity-morphing-solution-overview.md)中所述。

USBHUB 加载 USBCCGP 后，USBCCGP 选择前面报告的 subcompatible ID 指示的配置。 然后，USBCCGP 第二次查询兼容 ID 和 subcompatible ID。 此时，变形设备应返回当前所选配置的兼容 Id 和 subcompatible Id。 因此，在 USBCCGP 加载并选择特定配置后，变形设备需要对报告的兼容和 subcompatible Id 进行变形。 变形设备不能报告在选择配置之后用于加载 USBCCGP 的兼容 Id 和 subcompatible Id。

![usbhub 在枚举过程中从设备查询 microsoft os 描述符。](images/mbim13.png)

USBHUB 在枚举过程中从设备查询 Microsoft OS 描述符。

![设备返回处于未配置状态的 compatid。 ](images/mbim14.png)

设备返回处于未配置状态的 CompatId。 此 CompatId 用于加载 USBCCGP。

![usbccgp 选择在 subcompatible id 中报告的配置。](images/mbim15.png)

USBCCGP 选择在 subcompatible ID 中报告的配置。

![设备会根据新配置推移其 microsoft os 描述符。 microsoft os 描述符的 usbccgp 查询。](images/mbim16.png)

设备会根据新配置推移其 Microsoft OS 描述符。 Microsoft OS 描述符的 USBCCGP 查询。

![设备不返回任何 compatid。 基于类/子类/协议，usbccgp 加载 usbstor 和 mbcd。](images/mbim17.png)

设备不返回任何 CompatID。 基于类/子类/协议，USBCCGP 加载 USBSTOR 和 MBCD。

 

 





