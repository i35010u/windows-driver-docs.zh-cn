---
title: 创建安全的设备安装
description: 创建安全的设备安装
ms.assetid: e92488c4-1383-4493-b229-61c646546c82
keywords:
- 设备安装程序 WDK 设备安装安全性
- 设备安装 WDK，安全性
- 安装 WDK，安全设备
- security WDK 设备安装
- 安全描述符 WDK 设备安装
- INF 文件 WDK 设备安装
- 测试安全设置 WDK 设备安装
- 注册表 WDK 设备安装
- WMI 安全 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ec18f97b7e3e4f4a2a6f0985069702dc5e6375d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392001"
---
# <a name="creating-secure-device-installations"></a>创建安全的设备安装





当您创建[驱动程序包](driver-packages.md)，您必须确保以安全的方式将始终执行你的设备的安装。 安全设备安装是指执行以下任务：

-   限制对设备和其设备接口类的访问

-   设备创建的驱动程序服务的限制访问

-   驱动程序文件可防止修改或删除操作

-   限制对设备的注册表项的访问

-   限制对设备的 WMI 类的访问

-   正确使用安装程序 Api 函数

控制设备安装的安全性*安全描述符*。 主要的介质的指定安全描述符是 INF 文件。 系统提供了默认的安全描述符，并在大多数情况下，您就不必重写这些描述符。

### <a name="security-settings-for-devices-and-interfaces"></a>设备和接口的安全设置

系统提供的所有默认安全描述符[系统提供的设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff553419)。 通常情况下，这些描述符允许系统管理员的完全访问权限和读取/写入/执行访问权限的用户。 (控制对设备的访问也控制对设备的访问的安全描述符[设备接口类](device-interface-classes.md)(如果有）。)

用于 WDM 驱动程序的 INF 文件可以指定安全设置，每个类或每个设备，系统的默认设置会重写的。 供应商创建一个新的设备安装程序类应指定类的安全描述符。 通常情况下，指定特定于设备的安全描述符不是必需的。 它可能很有用，如果不同类型的属于同一类的设备具有明显不同类型的用户提供特定于设备的安全描述符。

若要指定属于 WDM 设备安装程序类的所有设备的安全描述符，请使用[ **INF AddReg 指令**](inf-addreg-directive.md)内[ **INF ClassInstall32 部分**](inf-classinstall32-section.md)的类安装程序的 INF 文件。 **AddReg**指令必须指向*添加注册表部分*设置的值**DeviceType**并**安全**注册表项. 这些注册表值指定指定的设备类型的所有设备的安全描述符。

若要指定属于 WDM 设备安装程序类的单个设备的安全描述符，请使用[ **INF AddReg 指令**](inf-addreg-directive.md)内[ **INF DDInstall.HW 部分**](inf-ddinstall-hw-section.md)的设备的 INF 文件。 **AddReg**指令必须指向*添加注册表部分*设置的值**DeviceType**并**安全**注册表项. 这些注册表值指定匹配的所有设备的安全描述符[硬件 ID](hardware-ids.md)或[兼容 Id](compatible-ids.md)指定由关联[ **INF 模型部分**](inf-models-section.md).

默认情况下，系统将应用的设备设置为打开表示设备的设备对象的请求的安全描述符 (例如，若要打开其 NT 设备名称是该设备的请求 *\\设备\\DeviceName*)。

但是，系统不会不默认情况下应用设置的设备对打开的设备，命名空间中的某个对象的请求的设备命名空间，包括其名称采用以下形式的所有对象的安全描述符 *\\设备\\DeviceName\\ObjectName*。 若要确保相同的安全设置应用以打开设备的命名空间中的对象的请求，设置设备的 FILE_DEVICE_SECURE_OPEN 设备特征标志。 有关安全的设备访问的详细信息，请参阅[控制设备 Namespace 访问 （Windows 驱动程序）](https://msdn.microsoft.com/library/windows/hardware/ff542068)。 有关如何设置 FILE_DEVICE_SECURE_OPEN 设备特征标志的信息，请参阅[指定设备特征 （Windows 驱动程序）](https://msdn.microsoft.com/library/windows/hardware/ff563818)。

PnP 管理器在后它会调用驱动程序的设备对象上设置安全值[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程。 通过调用创建一个物理设备对象 (PDO) 时，某些 WDM 驱动程序可以指定特定于设备的安全描述符[ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)。 有关详细信息，请参阅[保护设备对象](https://msdn.microsoft.com/library/windows/hardware/ff563688)。

### <a name="security-settings-for-driver-files"></a>驱动程序文件的安全设置

通过使用复制文件时[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)，则可以指定*文件列表部分*。**安全**部分。 本部分中指定的复制的所有文件的安全描述符**CopyFiles**指令。 但是，供应商无需指定驱动程序文件的安全描述符如果安装的目标是一个系统的子目录 *%systemroot%* 。 (有关这些子目录的详细信息，请参阅[使用 Dirids](using-dirids.md)。)系统提供了默认安全描述符的这些子目录，并默认描述符不应被替代。

### <a name="security-settings-for-driver-services"></a>驱动程序服务的安全设置

驱动程序 INF 文件内*服务安装部分*(请参阅[ **INF AddService 指令**](inf-addservice-directive.md))，可以包括**安全**条目。 此项指定执行诸如启动、 停止和配置与你的设备相关联的驱动程序服务所需的权限。 但是，系统对驱动程序服务提供的默认安全描述符和此默认描述符通常不需要重写。

### <a name="security-settings-for-device-and-driver-registry-entries"></a>设备和驱动程序注册表项的安全设置

通过使用在 INF 文件中指定的注册表项时[ **INF AddReg 指令**](inf-addreg-directive.md)，可以包括*添加注册表部分*。**安全**部分，了解每个*添加注册表部分*。 *添加注册表部分*。**安全**节指定对创建创建的注册表项的访问权限由关联*添加注册表部分*部分。 系统提供的所有注册表项下创建的默认安全描述符**HKR**相对的根。 因此，无需创建相对根目录下的注册表项时指定的安全描述符。

### <a name="security-settings-for-wmi-classes"></a>WMI 类的安全设置

系统将默认安全描述符分配给标识 WMI 类的 Guid。 对于 Windows XP 和早期操作系统版本，WMI Guid 的默认安全描述符允许完全访问权限的所有用户。 从 Windows Server 2003 开始，默认安全描述符允许仅对管理员的访问。

如果您的驱动程序定义的 WMI 类，并且您不希望使用这些类系统的默认安全描述符，则可以通过使用提供安全描述符[ **INF DDInstall.WMI 部分**](inf-ddinstall-wmi-section.md)在设备的 INF 文件。

### <a name="using-setupapi-functions-correctly"></a>正确使用安装程序 Api 函数

如果你[驱动程序包](driver-packages.md)包括安装程序、 共同安装程序或调用安装程序 Api 函数的其他安装应用程序必须遵循[使用 SetupAPI 指南](guidelines-for-using-setupapi.md)。

### <a href="" id="testing-installation-security-settings-"></a>测试安装安全设置

使用[SetupAPI 日志记录](setupapi-logging--windows-server-2003--windows-xp--and-windows-2000-.md)以验证该安全设置与安装你的设备关联的正确指定。 日志记录级别设置为 verbose (0x0000FFFF)，然后尝试不同安装方案。

这种情况下应包括初始安装和重新安装，从用户帐户和系统管理员帐户。 请尝试之前安装软件，将在你的设备，反之亦然。

如果安装成功，请查看日志以确认未发生错误。 如果应用安装失败，请查看日志以确定失败的原因。

此外，安装完成后可以执行以下操作：

-   使用注册表编辑器中查看分配到注册表项的安全设置。

-   使用**我的电脑**若要查看分配给文件的安全设置。

 

 





