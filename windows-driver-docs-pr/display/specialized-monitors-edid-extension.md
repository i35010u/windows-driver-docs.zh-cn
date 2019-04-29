---
title: HMD 和专用监视器的 EDID 扩展
description: HMD 和专用监视器的 EDID 扩展
keywords:
- 显示设备 WDK
- 显示器驱动程序 WDK
- 显示驱动程序 WDK，显示器驱动程序
- 监视器
- HMD
- 虚拟现实
ms.author: windowsdriverdev
ms.date: 11/30/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: b3d0009724a22ad2aceb221c4dc99d89c21e8bc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382335"
---
# <a name="edid-extension-vsdb-for-hmds-and-specialized-displays"></a>EDID HMDs 和专用的显示扩展插件 (VSDB)

*显示设备制造商的规范*

本文档提供有关如何实现指导[EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data) HMD （Head 装载显示） 中的 CTA （使用者技术关联） 扩展或将允许 Windows 识别为特殊显示专门的显示固件从而在将其正确处理在 Windows OS 中的每一层。 在本文档显示条款和监视器是同义的。

不带此 EDID 扩展名，HMDs 和专用的显示具有以下问题：

* 在 Windows 桌面上，将提供对显示、 放到它，则应用可以启动和鼠标光标可以漫游到显示器上。 如果用户不应为此，它可能会令人困惑，若要从此状态中恢复。
* 第三方排序器必须使用基于 HWND 的或基于 CoreWindow 的演示文稿不允许对显示进行独占访问的 Api。 Windows 桌面复合器负责向显示，可能会产生额外的非确定性延迟在某些情况下的路由有窗口演示 Api。

两个部分所需的此文档，以解决以上问题中的规范：

1. 中包含的显示器的固件[EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data)将被修改为包含[供应商特定的数据块](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data#EIA.2FCEA-861_extension_block)来标识特定于 Windows 的用例的显示。
2. Windows 显示子系统将正确识别此文档中所述供应商特定数据块，并相应地将显示。 请注意，不同版本的 Windows OS 可能具有不同的行为，调出下面。

1 的组合。 和 2。 更高版本会显示第一次插入后立即正确的 Windows 行为。 具体而言，HMDs 和某些专用的显示不会包含在常规的 Windows 桌面环境，并且有权使用 display [Windows.Devices.Display.Core](https://docs.microsoft.com/en-us/uwp/api/windows.devices.display.core) Api 会向第三方可用排序器。

视频电子标准协会 (VESA) 在其可以访问的类似信息作为本文档中定义 VSDB DisplayId 2.0 版中定义了标准化的字段。  DisplayID v2.0 或更高版本的首选的机制，用于将此数据传送的 HMDs，但是如果出于其他原因，设备必须使用 EDID，则应使用此 VSDB。

## <a name="vendor-specific-data-block-vsdb"></a>供应商特定的数据块 (VSDB)

负责编写包含 EDID 的固件代码的参与方必须包含 CTA 扩展块放在该块中 Microsoft 定义供应商特定数据块 (VSDB)。 "VESA 增强扩展显示标识数据 Standard"中描述的 EDIDs 结构 ([E EDID](https://www.vesa.org/vesa-standards/standards-summaries/))，请参阅版本 1.4，发布一个修订版 2 使用部分 2.2 描述扩展基块。  CTA 扩展块 CTA 861 系列文档"数字电视配置文件的未压缩高速数字接口"中定义。  中 （在撰写本文时） 的最新的部分 7.5.4 已发布版本中所述 VSDBs [CTA 861 G](https://standards.cta.tech/kwspub/published_docs/CTA-861-G-Preview.pdf)包括 VSDB 相对于其他数据块的顺序。 

VSDB 结构必须具有的格式和下表中所述的值。

![VSDB 规范](images/specialized-displays-vsdb.png)

### <a name="vendor-specific-tag-code-3-bits"></a>供应商特定的标记代码 [3 位]

此字段必须设置为`0x3`。

### <a name="length-5-bits"></a>长度 [5 位]

数据块，不包括此字节的总长度。  此字段必须设置为`0x15`。

### <a name="ieee-oui-3-bytes"></a>IEEE OUI [3 个字节]

IEEE 组织唯一标识符 (OUI) 用于标识显示分配给 Microsoft: `0x5C`， `0x12`， `0xCA`，按顺序字节顺序。

### <a name="version-1-byte"></a>版本 [1 个字节]

Microsoft 显示特定于供应商的数据块的内容与关联的版本号。

| 建议的用例 | Version | 受支持的 Windows 版本 |
|----------------------|---------|---------------------------|
| 将由 Windows Mixed Reality 的 HMD (VR/AR) 显示设备体验 | `0x1` | 支持 Windows 10 创意者更新及更高版本 |
| 将由第三方 （而不是 Windows Mixed Reality 体验中） 的排序器的 HMD (VR/AR) 显示设备 | `0x2` | 支持在 Windows 10 2018 年 10 月更新及更高版本 |
| 不是 HMDs 的专用的显示设备 | `0x3` | 在下一步 Windows vNext 和更高版本支持 |

### <a name="desktop-usage-flag-1-bit"></a>桌面用法标志 [1 的位]

在版本`0x3`和上面的此 VSDB 此位指示是否显示应为 desktop 的一部分。

* 如果显示应该是桌面的一部分，这应设置为`0x1`。
* 如果显示不应是桌面的一部分，这应设置为`0x0`。

在版本`0x1`并`0x2`的此 VSDB，此值应始终设置为`0x0`。

### <a name="third-party-usage-flag-1-bit"></a>第三方用法标志 [1 的位]

在版本`0x3`和上面的此 VSDB 此位指示是否显示应可供第三方排序器或仅由 Microsoft 提供 Windows 复合器。

* 如果显示应可由非 Windows 软件排序器，这应设置为`0x1`。
* 如果显示仅应由 Windows 复合器，这应设置为 0x0。

在版本`0x1`并`0x2`的此 VSDB，此值应始终设置为`0x0`。

### <a name="display-product-primary-use-case-5-bits"></a>显示产品主要用例 [5 位]

主要用例的显示设备：

* 测试设备- `0x1`
* 泛型显示- `0x2`
* 电视节目显示- `0x3`
* 桌面生产力显示- `0x4`
* 桌面游戏显示- `0x5`
* 演示文稿显示- `0x6`
* 虚拟现实耳机- `0x7`
* 增强的现实- `0x8`
* 视频墙上显示- `0x10`
* 医学成像显示- `0x11`
* 专用的游戏显示- `0x12`
* 专用视频监视器显示区域的 `0x13`
* 附件显示- `0x14`

### <a name="containerid-16-bytes"></a>ContainerID [16 个字节]

16 位全局唯一标识符是唯一的每个设备。 这是在工厂车间刻录中的标识符。 

## <a name="remarks"></a>备注

请注意，为了保持与早期版本的操作系统的最大兼容性，建议继续使用版本 HMDs`0x1`和`0x2`此 EDID 扩展。 要用于 HMDs 哪些值的版本上，请参阅上面的部分。
