---
title: 枚举已安装的设备接口
description: 枚举已安装的设备接口
ms.assetid: 14A9E6DD-58A9-4af0-B469-7CCF4596BE27
keywords:
- 枚举已安装的设备接口 WDK
- 安装设备接口 WDK
- 安装设备接口 WDK，枚举
- 设备接口 WDK 设备安装，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ea0698accf70230a3a9fc08cb7a202376ba17ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543304"
---
# <a name="enumerating-installed-device-interfaces"></a>枚举已安装的设备接口


您必须通过直接访问注册表项在系统中枚举设备接口类。 与任何注册表项，如位置、 名称或密钥的格式可能会更改的 Windows 不同版本之间。

使用以下准则来安全地发现设备接口的属性：

-   用户模式应用程序应执行以下步骤：

    1.  使用[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)或[ **SetupDiGetClassDevsEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551072)检索支持的接口为指定的设备设备接口的类。 您必须在设置 DIGCF_DEVICEINTERFACE 标志*标志*参数，并且你必须设置*枚举器*到特定设备实例标识符的参数。

        若要包含在系统中存在的设备接口，在中设置 DIGCF_PRESENT 标志*标志*参数。

    2.  使用[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)要枚举已被注册为设备接口类的接口。 通过指定此接口类*InterfaceClassGuid*参数。

-   内核模式驱动程序应使用[ **IoGetDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff549186)枚举系统中安装的设备接口类。

 

 





