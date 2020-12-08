---
title: 安装非 PnP 驱动程序
description: 安装非 PnP 驱动程序
keywords:
- Kernel-Mode Driver Framework WDK，安装驱动程序
- 基于框架的驱动程序 WDK KMDF，安装
- INF 文件 WDK KMDF，非 PnP 驱动程序
- 非 PnP 驱动程序 WDK KMDF
ms.date: 03/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: aaebee444a8461b5512a65b51b53d4bdf3683c28
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814705"
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
