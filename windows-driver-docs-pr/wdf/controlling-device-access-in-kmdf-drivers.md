---
title: 在 KMDF 驱动程序中控制设备访问权限
description: 在 KMDF 驱动程序中控制设备访问权限
ms.assetid: 62bbc69f-0754-4d37-a476-dd2ac3d70de6
keywords:
- 设备访问控制 WDK KMDF
- 命名 WDK 设备对象
- 设备对象 WDK KMDF
- framework 对象 WDK KMDF，设备访问控制
- 安全描述符 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 141639edf2d173a99cc5251c6f019f979761c372
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185321"
---
# <a name="controlling-device-access-in-kmdf-drivers"></a>在 KMDF 驱动程序中控制设备访问权限


驱动程序必须帮助防止用户不正当地访问计算机的设备和文件。 若要防止对设备和文件进行未经授权的访问，你必须：

-   仅在必要时命名设备对象。

-   提供设备对象和接口的安全描述符。

### <a name="naming-device-objects-only-when-necessary"></a><a href="" id="naming-device-objects-only-when-necessary"></a> 仅在必要时命名设备对象

与大多数 Windows 驱动模型 (WDM) 驱动程序一样，基于框架的驱动程序通常不会命名其设备对象。 应用程序可以通过指定设备对象名称来访问设备，因此，每个其他设备对象名称代表一个应用程序可用于访问该设备的其他路径。

若要防止未经授权访问设备，每个驱动程序可以在命名设备对象时指定安全描述符。 但是，操作系统提供给驱动程序的文件名 (参阅 [**WdfFileObjectGetFileName**](/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetfilename)) 不包括应用程序使用的设备对象名称。 因此，如果驱动程序堆栈中的多个驱动程序提供其设备对象的名称，则驱动程序无法确定应用程序用于打开设备的对象名称。 因此，应用程序可能会打开限制低于你的驱动程序所需的安全描述符的设备。

 (PDOs) 的物理设备对象必须具有名称。 通常，基于框架的总线驱动程序不指定 PDO 的名称，因为默认情况下，框架 () 指示操作系统生成名称。

另一方面，基于框架的驱动程序可以通过调用 [**WdfDeviceInitAssignName**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)将设备名称分配给设备对象。 驱动程序应将功能设备对象命名 (FDO) 、filter device object (filter DO) ，或仅当驱动程序必须支持需要特定设备名称的旧应用程序时，或者如果驱动程序属于其体系结构需要对象名称的较旧驱动程序堆栈。

WDM 驱动程序和基于框架的驱动程序应该提供应用程序可以访问的设备接口，而不是命名 FDOs 和筛选器 DOs。 操作系统从设备的 PDO 中获取设备接口的安全描述符，并从驱动程序包的 INF 文件指定的注册表项中获取。 如果驱动程序的设备在 raw 模式下运行（没有函数驱动程序），则总线驱动程序可以为 PDO 提供设备接口。

某些驱动程序必须调用 [**WdfDeviceCreateSymbolicLink**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink) ，才能为其设备创建符号链接名称。 例如，如果应用程序希望看到设备的 MS-DOS 名称，驱动程序可能会创建一个 [ms-dos 设备名称](../kernel/introduction-to-ms-dos-device-names.md) 。 如果驱动程序为未命名 FDO 或筛选器创建符号链接名称，则框架会将符号链接名称与 PDO 的名称关联。  (控制设备不与 PDO 关联，因此，驱动程序无法为未命名控制设备创建符号链接名称。 ) 

### <a name="providing-security-descriptors-for-device-objects-and-interfaces"></a><a href="" id="providing-security-descriptors-for-device-objects-and-interfaces"></a> 提供设备对象和接口的安全描述符

每个命名设备对象都必须有一个安全描述符。 操作系统使用设备对象的安全描述符来确定允许访问设备的用户类型及其设备接口。 可以通过以下方式将安全描述符分配给设备对象：

-   操作系统为设备对象提供默认安全描述符 (参阅 [控制设备访问](../kernel/controlling-device-access.md)) 。

-   此框架提供默认的安全描述符 (通过使用 "SDDL \_ DEVOBJ \_ SYS 所有 ADM" 的 " \_ \_ \_ 所有 ADM 全部" 值) 如果驱动程序调用 [**WdfDeviceInitAssignName**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname) 来为设备对象分配名称 (请参阅 [适用于设备对象) 的 SDDL](../kernel/sddl-for-device-objects.md) 。

-   你的驱动程序，它可以通过调用 [**WdfDeviceInitAssignSDDLString**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)替代框架的默认安全描述符。

默认情况下，操作系统还使用设备 PDO 的安全描述符来确定驱动程序提供的设备接口的访问权限。

驱动程序包可以提供一个 INF 文件，该文件使用 inf [**DDInstall 部分**](../install/inf-ddinstall-hw-section.md)中的[**inf AddReg 指令**](../install/inf-addreg-directive.md)指定设备的安全描述符。

有关在 INF 文件中指定安全描述符的详细信息，请参阅 [创建安全设备安装](../install/creating-secure-device-installations.md)。

如果驱动程序为以 raw 模式运行的设备创建 PDOs，则驱动程序在调用[**WdfPdoInitAssignRawDevice**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)时必须指定[设备安装程序类](../install/overview-of-device-setup-classes.md)。 此外，如果你的驱动程序创建控制设备，它可以调用 [**WdfDeviceInitSetDeviceClass**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass) 来指定设备安装程序类。 在这两种情况下，系统管理员都可以使用指定安装程序类的注册表项来存储设备的安全描述符。

有关操作系统如何确定要用于设备的安全描述符的信息，请参阅 [控制设备访问](../kernel/controlling-device-access.md)。

当框架创建设备对象时，它始终设置文件 \_ 设备 \_ 安全 \_ 打开标志，以便操作系统在允许应用程序访问设备的命名空间中的任何名称前检查设备的安全描述符。 有关文件 \_ 设备 \_ 安全 \_ 打开标志和设备命名空间的详细信息，请参阅 [控制设备命名空间访问](../kernel/controlling-device-namespace-access.md)。

 

