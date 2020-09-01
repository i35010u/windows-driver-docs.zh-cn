---
title: 安装非 PnP 驱动程序
description: 安装非 PnP 驱动程序
ms.assetid: 99676d85-feb2-482c-a91b-cfc48be5904c
keywords:
- 内核模式驱动程序框架 WDK，安装驱动程序
- 基于框架的驱动程序 WDK KMDF，安装
- INF 文件 WDK KMDF，非 PnP 驱动程序
- 非 PnP 驱动程序 WDK KMDF
ms.date: 03/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: b0a216ba87ed215cdcf20f9960874ab982328fbf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184149"
---
# <a name="installing-a-non-pnp-driver"></a>安装非 PnP 驱动程序


如果 KMDF 驱动程序支持 Windows 10 上的非即插即用 (PnP) 设备，请使用与 [非 PnP 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl/kmdf)中所示相同的方法，但删除对 INF 文件和共同安装程序的引用。 例如，不需要以下各项：

```
#define NONPNP_INF_FILENAME  L"\\nonpnp.inf"
#define WDF_SECTION_NAME L"nonpnp.NT.Wdf"
 
LoadWdfCoInstaller
UnloadWdfCoInstaller
 
PFN_WDFPREDEVICEINSTALLEX pfnWdfPreDeviceInstallEx;
PFN_WDFPOSTDEVICEINSTALL   pfnWdfPostDeviceInstall;
PFN_WDFPREDEVICEREMOVE     pfnWdfPreDeviceRemove;
PFN_WDFPOSTDEVICEREMOVE   pfnWdfPostDeviceRemove;
```

对于非 PnP KMDF 驱动程序，只需调用 SCM API 创建服务即可。 有关详细信息，请参阅 [安装服务](/windows/win32/services/installing-a-service)。