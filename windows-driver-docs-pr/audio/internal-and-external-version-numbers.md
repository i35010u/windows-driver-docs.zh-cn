---
title: 内部和外部版本号
description: 内部和外部版本号
ms.assetid: 705a2e5f-11b8-499c-815d-a2a54e907980
keywords:
- 版本编号 WDK 音频
- 音频的微型端口驱动程序 WDK，版本号
- 微型端口驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，版本号
- 内部版本数字 WDK 音频
- 外部版本数字 WDK 音频
- 文件 WDK 音频
- 驱动程序文件版本数字 WDK 音频
- 驱动程序版本数字 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c62927fc6aee38f0e4d69f119f50361b20e509e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333430"
---
# <a name="internal-and-external-version-numbers"></a>内部和外部版本号


## <span id="internal_and_external_version_numbers"></span><span id="INTERNAL_AND_EXTERNAL_VERSION_NUMBERS"></span>


驱动程序的资源文件指定的驱动程序文件版本中通过两种方式：

-   作为双 DWORD 值中指定的内部或二进制版本号**FILEVERSION**。 操作系统当前不使用此值。

-   作为外部或显示中指定的版本号**FileVersion**字符字符串。 当用户查看的单独的驱动程序文件的属性时，操作系统会显示此字符串。

在下 Windows XP 用户界面，例如，有多种替代方法，可以查看驱动程序文件的**FileVersion**字符串：

-   在 Windows 资源管理器：

-   1.  右键单击文件图标。
    2.  选择**属性**的驱动程序文件。
    3.  上**版本**选项卡上，查看**文件版本**数。
-   在设备管理器中：

-   1.  选择**属性**的特定音频设备。
    2.  上**驱动程序**选项卡上单击**驱动程序详细信息**。
    3.  从驱动程序包中的文件列表中选择的驱动程序文件。
    4.  视图**文件版本**选定的驱动程序文件的数目。
-   在控制面板中：

-   1.  单击**声音和音频设备**图标。
    2.  上**硬件**选项卡上选择的设备中，单击**属性**按钮。
    3.  上**驱动程序**选项卡上选择**驱动程序详细信息**，从驱动程序包和视图中的文件列表中选择的驱动程序文件**文件版本**数所选驱动程序文件。

若要使您的驱动程序版本号与 Windows 和 DirectX 兼容，请遵循以下规则时指定的内部和外部的版本号包括：

-   内部版本号采用格式*x*。*xx*.00。*xxxx*。 在最后一个点前两个多余的零是必需的。

-   外部版本字符串应采用格式*x*。*xx*。*xxxx* （不带内部版本号中的两个额外零）。

这些内部和外部的版本号应与匹配 （除外的两个额外零，上面所述）。

 

 




