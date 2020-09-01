---
title: 将安全描述符应用到设备对象上
description: 将安全描述符应用到设备对象上
ms.assetid: c0697021-cf78-4b85-b959-342179da5621
keywords:
- 安全描述符 WDK 文件系统，在设备对象上应用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f4e8591ec0b6df2f2ef0d4472129663c8567e9
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066218"
---
# <a name="applying-security-descriptors-on-the-device-object"></a>将安全描述符应用到设备对象上


## <span id="ddk_applying_security_descriptors_on_the_device_object_if"></span><span id="DDK_APPLYING_SECURITY_DESCRIPTORS_ON_THE_DEVICE_OBJECT_IF"></span>


大多数驱动程序使用 i/o 管理器针对其设备对象应用的访问控制，以防止其受到不正当的访问。 大多数驱动程序的最简单方法是在安装驱动程序时应用显式安全描述符。 在 INF 文件中，AddReg 部分中的 "安全" 条目描述了此类安全描述符。 有关用于描述安全描述符的完整语言的详细信息，请参阅 Microsoft Windows SDK 文档中的安全描述符定义语言。

安全描述符的基本格式使用安全描述符定义语言 (SDDL) 包含标准安全描述符的以下不同部分：

-   所有者 SID。

-   组 SID。

-   自由访问控制列表 (DACL)。

-   系统访问控制列表 (SACL)。

因此，安全描述符的 INF 脚本中的说明如下：

```cpp
O:owner-sidG:group-sidD:dacl-flags(ace)(ace)S:sacl-flags(ace)(ace)
```

各个访问控制项描述了对由安全标识符或 SID 指定的特定组或用户授予或拒绝的访问权限。 例如，INF 文件可能包含以下行：

```cpp
"D:P(A;CI;GR;;;BU)(A;CI;GR;;;PU)(A;CI;GA;;;BA)(A;CI;GA;;;SY)(A;CI;GA;;;NS)(A;CI;GA;;;LS)(A;CI;CCDCLCSWRPSDRC;;;S-1-5-32-556)"
```

上面的示例来自 NETTCPIP。Microsoft Windows XP Service Pack 1 (SP1) 系统中的 INF 文件。

在此实例中，没有指定所有者或组，因此默认为预定义值或默认值。 **D**指示这是一个 DACL。 **P**指示这是受保护的 ACL，并且不从包含对象的安全说明符继承任何权限。 受保护的 ACL 可防止继承父项的更宽松安全性。 括号中的表达式指示 (ACE) 的单个访问控制项。 使用 SDDL 的访问控制项由几个不同的分号分隔的组件组成。 按照顺序，它们如下所示：

-   ACE 的类型指示符。 有四种不同类型的 Dacl，这四种不同类型的 Sacl。

-   用于描述此 ACE 对于子对象的继承或 Sacl 的审核和警报策略的 **标志** 字段。

-   **权限**字段指示 ACE 授予或拒绝的权限。 此字段可以指定特定的数值，指示适用于此 ACE 的泛型、标准和特定权限，或者使用常见访问权限的字符串说明。

-   如果 DACL 是特定于对象的 ACE 结构，则为对象 GUID。

-   如果 DACL 是特定于对象的 ACE 结构，则为继承对象 GUID

-   一个 SID，指示此 ACE 适用的安全实体。

因此，解释示例安全描述符时，ACE 的 "A" 表示这是 "允许访问" 条目。 替代项是 "拒绝访问" 条目，它只是不常使用的，并由前导 "D" 字符表示。 " **标志** " 字段指定容器继承 (CI) ，这指示此 ACE 由子对象继承。

**权限**字段值对包含一般权限和标准权限的特定权限进行编码。 例如，"GR" 表示 "一般读取" 访问权限，"GA" 表示 "一般全部" 访问，这两个都是通用权限。 有一些特殊权限遵循这些一般权限。 在上面的示例中，"CC" 指示特定于文件和目录权限的 "创建子访问权限"。 上面的示例还包括 "CC" 字符串后的其他标准权利，包括用于删除子访问的 "DC"、用于列表子访问的 "LC"、用于自右访问的 "软件"、用于读属性访问的 "RP"、用于标准删除访问的 "SD" 和用于读取控制访问的 "RC"。

上面示例中的 SID 输入字符串包括适用于高级用户的 "PU"、内置用户的 "BU"、用于本地服务帐户的 "BA"、"SY" （对于本地系统）和 "NS" （用于网络服务帐户）。 因此，在上面的示例中，用户对对象具有通用读取访问权限。 与此相反，内置管理员、本地服务帐户、本地系统和网络服务均被指定为通用的所有访问 (读取、写入和执行) 。 Windows SDK 中介绍了所有可能的权限和标准 SID 字符串的完整集。

这些 Acl 将应用于给定驱动程序创建的所有设备对象。 创建命名设备对象时，驱动程序还可以通过使用新函数 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)来控制特定对象的安全设置。 **IoCreateDeviceSecure**函数在 Windows XP Service Pack 1 和 windows Server 2003 及更高版本上可用。 使用 **IoCreateDeviceSecure**，将应用于设备对象的安全描述符描述为适用于设备对象的完整安全描述符定义语言子集。

将特定安全描述符应用到设备对象的目的是确保在应用程序尝试访问设备本身时对设备进行适当的安全检查。 对于包含名称结构 (文件系统的命名空间的设备对象（例如) ），管理对此设备命名空间的访问的详细信息属于驱动程序，而不是 i/o 管理器。

在这些情况下，一种有趣的问题是如何处理负责检查对驱动程序设备对象的访问的 i/o 管理器和设备驱动程序（实现适用于驱动程序的任何安全策略）之间的安全性。 传统上，如果打开的对象是设备本身的名称，i/o 管理器将使用其安全描述符直接对设备对象执行完全访问权限检查。 但是，如果打开的对象指示驱动程序本身中的路径，则 i/o 管理器将仅检查以确保向设备对象授予遍历访问权限。 通常，将授予此遍历权限，因为大多数线程已被授予 **SeChangeNotifyPrivilege**，这与授予目录的遍历权限相对应。 不支持名称结构的设备通常会请求 i/o 管理器执行完整安全检查。 为此，可在 "设备特征" 字段中设置 " **文件 \_ 设备 \_ 安全 \_ 打开** 位"。 包含此类设备对象的驱动程序应为不支持名称结构的设备设置此特性。 例如，文件系统会在其命名设备对象上设置此选项 (该选项不支持命名结构) ，但不 (卷上的未命名设备对象上设置此选项，例如) ，它支持命名结构。 如果未能正确设置此项，则是驱动程序中常见的错误，可能会允许不适当的设备访问。 对于使用附件接口 ([**IoAttachDeviceToDeviceStackSafe**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)的驱动程序，例如) ，如果此字段是在驱动程序所附加到的设备中设置的，则会设置 **文件 \_ 设备 \_ 安全 \_ 打开** 位。 因此，筛选器驱动程序无需担心这一特定方面的安全检查。

 

