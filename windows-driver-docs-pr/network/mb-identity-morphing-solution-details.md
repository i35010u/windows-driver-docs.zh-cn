---
title: MB 标识变形解决方案详细信息
description: 介绍配置要求和兼容 Id MB 标识变形的设备
ms.assetid: E4E17B4F-665B-425C-B90B-F60561B71CAB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f76696e4e057e298ccb8a9eddf763fcb287df92b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343419"
---
# <a name="mb-identity-morphing-solution-details"></a>MB 标识变换解决方案详细信息


## <a name="configuration-requirements"></a>配置需求


在 Windows 8 中的转换函数的顺序需要维护。 例如，如果 MBIM 是 Windows 8 配置中的第三个函数，它应为 IHV-NCM-2.0-配置中的第三个函数。

Windows-7-Configuration

Windows 7 配置应变形设备中的第一个配置。 此配置应具有大容量存储函数的函数之一。 Windows 8 将不选择此配置。 在 Windows 7 和 Windows 的早期版本中，Windows 7 配置是所选的默认配置。 此配置用于公开 USB 大容量存储函数 Ihv 放置其驱动程序包，从而允许用户安装 IHV 的驱动程序的位置。

Windows-8-Configuration

Windows 7 配置为在其加载 MBCD 的函数之一公开 MBIM 函数。 在 Windows 8 中，返回到 USBCCGP subCompatibleID 值中使用此配置的值。 USBCCGP 在加载时选择此配置。 Windows 8 配置应为 2、 3 或 4 任一配置。 为 Windows 8 配置不支持任何其他配置。 此配置还公开了大容量存储函数作为第一个函数，以允许用户安装 IHV 的驱动程序包。

IHV-NCM-2.0-Configuration

IHV-NCM-2.0-配置公开特定于 IHV 的函数以及 MBIM 和大容量存储函数。 未设置或通过 Windows 使用此配置。 由用户执行安装后要 IHV 软件，可以影响到此配置。 请注意，在此配置中的函数的顺序应与 Windows 8 配置相同。 尽管可对 Windows 8 配置添加额外的函数，但现有的函数应将保留在相同的顺序。

IHV-NCM-1.0-Configuration

IHV-NCM-1.0-配置公开特定于 IHV 的函数以及 NCM 1.0 和大容量存储函数。 此配置不是设置或使用的 Windows 8。 IHV 软件已安装用户后，将仅在 Windows 7 和 Windows 的早期版本中使用此配置。 IHV 软件采用变形过程将设备从 Windows 7 配置为此配置。

## <a name="compatible-ids"></a>兼容 Id


兼容 Id 是 8 个字符或更小设备用于指示驱动程序加载到 Windows 的首选项的字符串。 设备可以通过使用 Microsoft OS 描述符定义兼容 Id。 Subcompatible 和兼容 Id 适用于各个函数。 每个配置可以有一组单独的兼容 Id，映射到该配置中的函数集。 虽然兼容和 subcompatible Id 应用于各个函数，但变形的设备可以具有单个兼容 ID 时不选择了任何配置。 此兼容和 subcompatible ID 以逻辑方式应用到整个变形设备。

**正在加载 USBCCGP**

在 Windows 8 中，USBCCGP 驱动程序需要自动选择变形的设备上的 Windows 8 配置。

若要加载 USBCCGP 驱动程序，变形设备需要时变形的设备上不选择了任何配置的报表的以下的兼容和 subcompatible Id:

-   如果变形设备分组接口使用 Iad 到函数中，兼容 ID 应作为"ALTRCFG"和 Windows 8 配置数形式的 subcompatible ID 进行报告。
-   如果变形设备使用到的函数中分组接口的 WCM Ufd，兼容 ID 应作为"WMCALTR"和 Windows 8 配置数形式的 subcompatible ID 进行报告。

例如，如果在 Windows 8 配置为配置 3，则 subcompatible ID 将在这两种情况中的"3"。

**变形兼容 Id**

在 USB 设备枚举期间 USBHUB 变形设备兼容 id 时查询变形的设备上选择了任何配置。 变形设备应返回用来加载 USBCCGP，如中所述的兼容和 subcompatible ID [MB 标识变形解决方案概述](mb-identity-morphing-solution-overview.md)。

USBHUB 加载 USBCCGP 后，USBCCGP 选择以前报告过的 subcompatible ID 所指示的配置。 USBCCGP 然后第二次查询的兼容和 subcompatible ID。 此时，变形设备应返回的配置的当前所选的兼容和 subcompatible Id。 因此，USBCCGP 加载，并选择一个特定的配置后，需要执行 morph 报告的兼容和 subcompatible Id 变形的设备。 变形的设备必须报告用于加载 USBCCGP 后选中了配置的兼容和 subcompatible Id。

![usbhub 枚举过程中查询从设备的 microsoft 操作系统描述符。](images/mbim13.png)

USBHUB 枚举过程中查询从设备的 Microsoft 操作系统描述符。

![设备处于未配置状态将恢复 compatid。 ](images/mbim14.png)

设备处于未配置状态将恢复 CompatId。 此 CompatId 用于加载 USBCCGP。

![usbccgp 选择 subcompatible id 中报告的配置。](images/mbim15.png)

USBCCGP 选择 subcompatible id。 中报告的配置

![设备采用其根据新配置的 microsoft 操作系统描述符。 microsoft 操作系统描述符的 usbccgp 查询。](images/mbim16.png)

设备采用其根据新配置的 Microsoft 操作系统描述符。 Microsoft 操作系统描述符的 USBCCGP 查询。

![设备不返回任何 compatid。 基于类 / 子类 / 协议，usbccgp 加载 usbstor 和 mbcd。](images/mbim17.png)

设备不返回任何 CompatID。 基于类 / 子类 / 协议，USBCCGP 加载 USBSTOR 和 MBCD。

 

 





