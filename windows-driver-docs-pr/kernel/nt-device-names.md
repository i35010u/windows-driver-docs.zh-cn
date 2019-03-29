---
title: NT 设备名称
description: NT 设备名称
ms.assetid: dfcc7338-7c4d-4b4c-9a13-c76bfe82f5a9
keywords:
- NT 设备名称 WDK 内核
- 设备对象 WDK 内核，名为
- 指定的设备对象 WDK 内核
- 设备名称 WDK 内核
- 非 WDM 驱动程序设备名称 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67e217f6d1e3474904de2fa9a55d96bbdd82a91c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567207"
---
# <a name="nt-device-names"></a>NT 设备名称





指定的设备对象具有窗体的名称**\\设备\\**<em>DeviceName</em>。 这称为*NT 设备名称*的设备对象。

### <a name="device-names-for-wdm-drivers"></a>用于 WDM 驱动程序的设备名称

WDM 驱动程序直接名称及其设备对象。 相反，系统会施加命名方案，以确保该设备驱动程序之间不冲突名称的统一。 用于 WDM 驱动程序的命名方案是，如下所示。

-   名为的是 PDO 设备。 总线驱动程序请求的设备，则将枚举命名的 PDOs。 总线驱动程序指定的文件\_自动生成\_设备\_名称设备特征时创建的设备对象。 有关详细信息，请参阅[指定设备特征](specifying-device-characteristics.md)。 然后系统将自动生成的设备名称。

-   FDOs 和筛选器的未命名 DOs。 创建设备对象时，函数和筛选器驱动程序不会请求一个名称。

对指定的设备对象的所有 I/O 请求将自动都转到该设备对象的堆栈中的顶级对象。 因此，仅 PDO 是必须名为。 用户模式应用程序并不指 WDM 设备对象的名称;相反，应用程序访问的设备对象通过其*设备接口*。 有关详细信息，请参阅[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)。

驱动程序编写人员必须命名设备堆栈中的多个对象。 操作系统会检查基于命名对象的安全设置。 如果两个不同的对象已命名，并且具有不同的安全描述符，发送到具有较弱的安全描述符的对象的 I/O 请求可以访问具有更强的安全描述符的设备对象。

### <a name="device-names-for-non-wdm-drivers"></a>设备名称的非 WDM 驱动程序

非 WDM 驱动程序必须显式指定任何指定的设备对象的名称。 该驱动程序必须创建至少一个指定的设备对象中**\\设备**要接收的 I/O 请求的对象目录。 该驱动程序指定作为设备名称*DeviceName*参数[ **IoCreateDeviceSecure** ](https://msdn.microsoft.com/library/windows/hardware/ff548407)时创建的设备对象。

 

 




