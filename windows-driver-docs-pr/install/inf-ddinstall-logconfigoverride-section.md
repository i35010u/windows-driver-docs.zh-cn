---
title: INF DDInstall.LogConfigOverride 节
description: DDInstall. LogConfigOverride 部分用于创建替代配置来替代硬件资源要求。
ms.assetid: 7ee8d221-7cdb-4373-aa8b-2d5164f6a636
keywords:
- INF DDInstall. LogConfigOverride 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.LogConfigOverride Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 875376b3c81d1e7784e027d76f5a9820fa2439ab
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095117"
---
# <a name="inf-ddinstalllogconfigoverride-section"></a>INF DDInstall.LogConfigOverride 节


**注意**   如果要构建通用或移动驱动程序包，此部分无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

<em>DDInstall</em>**。LogConfigOverride** 节用于创建 [替代配置](../kernel/hardware-resources.md#logical-configuration-types-for-resource-requirements-lists)，该配置将覆盖即插即用设备的总线驱动程序报告的硬件资源需求。

```inf
[install-section-name.LogConfigOverride] |
[install-section-name.nt.LogConfigOverride] |
[install-section-name.ntx86.LogConfigOverride] |
[install-section-name.ntarm.LogConfigOverride] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.LogConfigOverride] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.LogConfigOverride] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.LogConfigOverride]  (Windows XP and later versions of Windows)
 
LogConfig=log-config-section[,log-config-section]...] 
```

## <a name="entries"></a>项


用于<em>DDInstall</em>的条目项和值 **。LogConfigOverride**节在由[**INF LogConfig 指令**](inf-logconfig-directive.md)引用的*日志配置部分*中指定。

<a name="remarks"></a>备注
-------

即插即用设备的 *日志配置部分* 中指定的配置数据是首选的硬件资源配置，但不是绝对要求。 部分或全部指定的硬件资源配置数据可能不会被设备的底层总线驱动程序接受。 在这种情况下，会为设备驱动程序分配总线驱动程序最初报告的硬件资源。

<a name="examples"></a>示例
--------

下面的示例演示了一个 <em>DDInstall</em>**。** PCMCIA 设备的 LogConfigOverride 部分和相应的 *日志配置部分* 。

```inf
[XYZDevice.LogConfigOverride]
LogConfig = XYZDevice.Override0

[XYZDevice.Override0]
IOConfig=2f8-2ff
IOConfig=20@100-FFFF%FFE0
IRQConfig=3,4,5,7,9,10,11
MemConfig=4000@0-FFFFFFFF%FFFFC000
PcCardConfig=41:100000(W)
```

有关在 *日志配置部分*中指定的硬件资源配置数据值的详细信息，请参阅 [**INF LogConfig 指令**](inf-logconfig-directive.md)。

## <a name="see-also"></a>另请参阅


[***DDInstall***](inf-ddinstall-section.md)

 

