---
title: 内部和外部版本号
description: 内部和外部版本号
keywords:
- 版本号 WDK 音频
- 音频微型端口驱动程序 WDK，版本号
- 微型端口驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，版本号
- 内部版本号 WDK 音频
- 外部版本号 WDK 音频
- 文件 WDK 音频
- 驱动程序-文件版本号 WDK 音频
- 驱动程序版本号 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fddda82d48f7db5eaa41b7a51970b183ab00240
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799223"
---
# <a name="internal-and-external-version-numbers"></a>内部和外部版本号


## <span id="internal_and_external_version_numbers"></span><span id="INTERNAL_AND_EXTERNAL_VERSION_NUMBERS"></span>


驱动程序的资源文件以两种方式指定驱动程序文件版本：

-   作为在双 DWORD 值 **FILEVERSION** 中指定的内部或二进制版本号。 操作系统当前不使用此值。

-   作为在 **FileVersion** 字符串中指定的外部或显示版本号。 当用户查看各个驱动程序文件的属性时，操作系统将显示此字符串。

例如，在 Windows XP 用户界面下，有几种方法可以查看驱动程序文件的 **FileVersion** 字符串：

-   在 Windows 资源管理器中：

-   1.  右键单击文件图标。
    2.  选择驱动程序文件的 **属性** 。
    3.  在 " **版本** " 选项卡上，查看 **文件版本号** 。
-   在设备管理器中：

-   1.  选择特定音频设备的 **属性** 。
    2.  在 " **驱动程序** " 选项卡上，单击 **驱动程序详细信息**。
    3.  从驱动程序包中的文件列表中选择驱动程序文件。
    4.  查看所选驱动程序文件的 **文件版本号** 。
-   在控制面板中：

-   1.  单击 " **声音和音频设备** " 图标。
    2.  在 " **硬件** " 选项卡上，选择设备，然后单击 " **属性** " 按钮。
    3.  在 " **驱动** 程序" 选项卡上，选择 " **驱动程序详细信息**"，从驱动程序包的文件列表中选择驱动程序文件，然后查看所选驱动程序文件的 **版本号** 。

若要使驱动程序版本号与 Windows 和 DirectX 兼容，请在指定内部和外部版本号时遵循以下规则：

-   内部版本号的格式为 *x*。*xx*. 00。*xxxx*。 最后一个点之前需要两个多余的零。

-   外部版本字符串应使用格式 *x*。*xx*。*xxxx* (内部版本号中没有两个额外的零) 。

这两个内部和外部版本号应匹配 (除了两个额外的零外，如上所述) 。

 

 




