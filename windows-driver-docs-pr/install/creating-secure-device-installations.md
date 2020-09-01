---
title: 创建安全的设备安装
description: 创建安全的设备安装
ms.assetid: e92488c4-1383-4493-b229-61c646546c82
keywords:
- 设备设置 WDK 设备安装，安全性
- 设备安装 WDK，安全性
- 安装设备 WDK，安全性
- 安全 WDK 设备安装
- 安全描述符中的 WDK 设备安装
- INF 文件 WDK 设备安装
- 测试安全设置 WDK 设备安装
- 注册表 WDK 设备安装
- WMI 安全 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02635a6c13efe3b44fefc570399d0f75ff67ee72
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097149"
---
# <a name="creating-secure-device-installations"></a>创建安全的设备安装





当你创建 [驱动程序包](driver-packages.md)时，你必须确保始终以安全的方式执行你的设备安装。 安全设备安装是指执行以下操作的设备：

-   限制对设备及其设备接口类的访问

-   限制对为设备创建的驱动程序服务的访问权限

-   保护驱动程序文件不被修改或删除

-   限制对设备的注册表项的访问

-   限制对设备的 WMI 类的访问

-   正确使用 Setupapi.log 函数

设备安装安全性由 *安全描述符*控制。 用于指定安全描述符的主要媒体是 INF 文件。 系统提供默认安全描述符，在大多数情况下，您不必重写这些描述符。

### <a name="security-settings-for-devices-and-interfaces"></a>设备和接口的安全设置

系统为所有 [系统提供的设备安装程序类](/previous-versions/ff553419(v=vs.85))提供默认安全描述符。 通常，这些描述符允许对系统管理员具有完全访问权限，并为用户提供读取/写入/执行访问权限。  (控制设备访问权限的安全描述符也控制对设备的 [设备接口类](./overview-of-device-interface-classes.md)（如果有）的访问。 ) 

WDM 驱动程序的 INF 文件可以指定每个类或每个设备的安全设置，这些设置会覆盖系统的默认设置。 创建新设备安装程序类的供应商应为类指定安全描述符。 通常，指定设备特定的安全描述符不是必需的。 如果属于同一类的不同类型设备具有明显不同类型的用户，则提供设备特定的安全描述符可能会很有用。

若要为属于 WDM 设备安装程序类的所有设备指定安全描述符，请在类安装程序的 INF 文件的[**Inf ClassInstall32 部分**](inf-classinstall32-section.md)中使用[**inf AddReg 指令**](inf-addreg-directive.md)。 **AddReg**指令必须指向为**DeviceType**和**Security**注册表项设置值的 "*添加注册表" 部分*。 这些注册表值为指定设备类型的所有设备指定安全描述符。

若要为属于 WDM 设备安装程序类的单个设备指定安全描述符，请在设备 INF 文件的[**Inf DDInstall 部分**](inf-ddinstall-hw-section.md)中使用[**inf AddReg 指令**](inf-addreg-directive.md)。 **AddReg**指令必须指向为**DeviceType**和**Security**注册表项设置值的 "*添加注册表" 部分*。 这些注册表值指定与相关[**INF 模型部分**](inf-models-section.md)指定的[硬件 ID](hardware-ids.md)或[兼容 id](compatible-ids.md)匹配的所有设备的安全描述符。

默认情况下，系统会将设备的安全描述符集应用于请求，以打开代表设备的设备对象 (例如，打开设备（其 NT 设备名为* \\ 设备 \\ DeviceName*) ）的请求。

但是，系统不会默认情况下将设备的安全描述符集应用于请求，以打开设备命名空间中的对象，其中设备命名空间包含其名称格式为* \\ 设备 \\ DeviceName \\ ObjectName*的所有对象。 若要确保对设备的命名空间中的对象的打开请求应用相同的安全设置，请为设备设置 FILE_DEVICE_SECURE_OPEN 设备特征标志。 有关安全设备访问的详细信息，请参阅 [ (Windows 驱动程序) 控制设备命名空间访问 ](../kernel/controlling-device-namespace-access.md)。 有关如何设置 FILE_DEVICE_SECURE_OPEN 设备特征标志的信息，请参阅 [ (Windows 驱动程序) 指定设备特征 ](../kernel/specifying-device-characteristics.md)。

PnP 管理器在调用驱动程序的 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程后设置设备对象上的安全值。 某些 WDM 驱动程序可以在通过调用 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)创建 (PDO) 的物理设备对象时指定设备特定的安全描述符。 有关详细信息，请参阅 [保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)。

### <a name="security-settings-for-driver-files"></a>驱动程序文件的安全设置

使用 [**INF CopyFiles 指令**](inf-copyfiles-directive.md)复制文件时，可以指定 *文件列表部分*。**安全性** 部分。 此部分指定 **CopyFiles** 指令复制的所有文件的安全描述符。 但是，如果安装目标是 *% SystemRoot%* 的系统子目录之一，则供应商永远无需为驱动程序文件指定安全描述符。  (有关这些子目录的详细信息，请参阅 [使用 Dirids](using-dirids.md)。 ) 系统为这些子目录提供默认安全描述符，而不应重写默认说明符。

### <a name="security-settings-for-driver-services"></a>驱动程序服务的安全设置

在驱动程序 INF 文件的 *服务安装部分* (参阅 [**INF AddService 指令**](inf-addservice-directive.md)) ，你可以包含一个 **安全** 条目。 此条目指定执行此类操作所需的权限，这些操作包括启动、停止和配置与设备关联的驱动程序服务。 但是，系统为驱动程序服务提供了一个默认的安全描述符，并且通常不需要重写此默认说明符。

### <a name="security-settings-for-device-and-driver-registry-entries"></a>设备和驱动程序注册表项的安全设置

使用[**Inf AddReg 指令**](inf-addreg-directive.md)在 INF 文件中指定注册表项时，可以包含 "*添加注册表" 部分*。每个*添加注册表部分*的**安全性**部分。 " *添加注册表" 部分*。**安全** 部分指定由关联的 " *添加注册表* " 部分创建的注册表项的访问权限。 系统为在 **HKR** 相对根下创建的所有注册表项提供默认安全描述符。 因此，在相对根下创建注册表项时，无需指定安全描述符。

### <a name="security-settings-for-wmi-classes"></a>WMI 类的安全设置

系统会将默认安全描述符分配给标识 WMI 类的 Guid。 对于 Windows XP 和早期版本的操作系统版本，WMI Guid 的默认安全描述符允许所有用户完全访问。 从 Windows Server 2003 开始，默认的安全描述符仅允许管理员访问。

如果你的驱动程序定义 WMI 类，并且你不希望将系统的默认安全描述符用于这些类，则可以通过使用设备 INF 文件中的 [**Inf DDInstall 部分**](inf-ddinstall-wmi-section.md) 来提供安全描述符。

### <a name="using-setupapi-functions-correctly"></a>正确使用 Setupapi.log 函数

如果你的 [驱动程序包](driver-packages.md) 包括安装程序、共同安装程序或调用 setupapi.log 函数的其他安装应用程序，则必须遵循 [使用 setupapi.log 的指导原则](guidelines-for-using-setupapi.md)。

### <a name="testing-installation-security-settings"></a><a href="" id="testing-installation-security-settings-"></a>测试安装安全设置

使用 [setupapi.log 日志记录](setupapi-logging--windows-server-2003--windows-xp--and-windows-2000-.md) 来验证是否已正确指定与安装设备关联的安全设置。 将日志记录级别设置为 "详细 (0x0000FFFF") ，然后尝试各种安装方案。

此类方案应同时包括用户帐户和系统管理员帐户中的初始安装和 reinstallations。 在安装软件之前，请尝试插入设备，反之亦然。

如果安装成功，请查看日志以确认未发生错误。 如果安装失败，请查看日志以确定失败的原因。

此外，在安装完成后，可以执行以下操作：

-   使用注册表编辑器查看分配给注册表项的安全设置。

-   使用 **我的电脑** 查看分配给文件的安全设置。

 

