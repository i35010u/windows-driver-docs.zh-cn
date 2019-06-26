---
title: INF DDInstall.LogConfigOverride 节
description: DDInstall.LogConfigOverride 部分用于创建要重写硬件资源要求的重写配置。
ms.assetid: 7ee8d221-7cdb-4373-aa8b-2d5164f6a636
keywords:
- INF DDInstall.LogConfigOverride 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.LogConfigOverride Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e3f12cdd81e3b6348db16a6d10c282bfeec4dd6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385907"
---
# <a name="inf-ddinstalllogconfigoverride-section"></a>INF DDInstall.LogConfigOverride 节


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

<em>DDInstall</em> **。LogConfigOverride**部分用于创建[替代配置](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#logical-configuration-types-for-resource-requirements-lists)，这会重写插设备的总线驱动程序报告的硬件资源要求。

```ini
[install-section-name.LogConfigOverride] |
[install-section-name.nt.LogConfigOverride] |
[install-section-name.ntx86.LogConfigOverride] |
[install-section-name.ntarm.LogConfigOverride] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.LogConfigOverride] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.LogConfigOverride] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.LogConfigOverride]  (Windows XP and later versions of Windows)
 
LogConfig=log-config-section[,log-config-section]...] 
```

## <a name="entries"></a>条目


节条目和与一起使用的值<em>DDInstall</em> **。LogConfigOverride**部分中指定*日志配置部分*所引用的[ **INF LogConfig 指令**](inf-logconfig-directive.md)。

<a name="remarks"></a>备注
-------

中指定的配置数据*日志配置部分*Plug and play 设备是首选的硬件资源配置，但不是绝对要求。 某些或所有指定的硬件资源配置数据可能不接受的设备的基础总线驱动程序中。 在这种情况下，设备驱动程序分配最初由总线驱动程序报告的硬件资源。

<a name="examples"></a>示例
--------

下面的示例演示<em>DDInstall</em> **。LogConfigOverride**部分，并相应*日志配置部分*PCMCIA 设备。

```ini
[XYZDevice.LogConfigOverride]
LogConfig = XYZDevice.Override0

[XYZDevice.Override0]
IOConfig=2f8-2ff
IOConfig=20@100-FFFF%FFE0
IRQConfig=3,4,5,7,9,10,11
MemConfig=4000@0-FFFFFFFF%FFFFC000
PcCardConfig=41:100000(W)
```

有关详细信息中指定的硬件资源配置数据值*日志配置节*，请参阅[ **INF LogConfig 指令**](inf-logconfig-directive.md)。

## <a name="see-also"></a>请参阅


[***DDInstall***](inf-ddinstall-section.md)

 

 






