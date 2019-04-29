---
title: 将安全描述符应用到设备对象上
description: 将安全描述符应用到设备对象上
ms.assetid: c0697021-cf78-4b85-b959-342179da5621
keywords:
- 安全描述符 WDK 文件系统，将应用于设备对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9db2ced158caf82095c3c1cfbe506add1d69806
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322289"
---
# <a name="applying-security-descriptors-on-the-device-object"></a>将安全描述符应用到设备对象上


## <span id="ddk_applying_security_descriptors_on_the_device_object_if"></span><span id="DDK_APPLYING_SECURITY_DESCRIPTORS_ON_THE_DEVICE_OBJECT_IF"></span>


大多数驱动程序使用情况下对其设备的对象的 I/O 管理器应用的访问控制保护自身免遭不适当的访问。 大多数驱动程序的最简单方法是将显式安全描述符应用时安装该驱动程序。 在 INF 文件中，此类安全描述符由 AddReg 部分的"安全性"项描述。 有关完整的语言来描述安全描述符的详细信息，请参阅 Microsoft Windows SDK 文档中的安全描述符定义语言。

使用安全描述符定义语言 (SDDL) 的安全描述符的基本格式包括以下不同的标准安全描述符：

-   所有者的 SID。

-   组 SID。

-   自由访问控制列表 (DACL)。

-   系统访问控制列表 (SACL)。

因此，安全描述符的 INF 脚本中的说明为：

```cpp
O:owner-sidG:group-sidD:dacl-flags(ace)(ace)S:sacl-flags(ace)(ace)
```

单独的访问控制项描述的访问权限将授予或拒绝特定组或用户指定的安全标识符或 SID。 例如，一个 INF 文件可能包含一个行如：

```cpp
"D:P(A;CI;GR;;;BU)(A;CI;GR;;;PU)(A;CI;GA;;;BA)(A;CI;GA;;;SY)(A;CI;GA;;;NS)(A;CI;GA;;;LS)(A;CI;CCDCLCSWRPSDRC;;;S-1-5-32-556)"
```

上面的示例来自 NETTCPIP。从 Microsoft Windows XP Service Pack 1 (SP1) 系统的 INF 文件。

在此情况下，没有所有者或组指定，因此它们默认为预定义或默认值。 **D**指示这是 DACL。 **P**指示这是一个受保护的 ACL，不会包含对象的安全描述符中继承任何权限。 受保护的 ACL 可防止父更宽松的安全性继承而来的。 带括号的表达式指示单一访问控制项 (ACE)。 使用 SDDL 的访问控制项由多个以分号分隔的不同组件组成。 按顺序，它们是按如下所示：

-   Ace 类型指示符。 有四种唯一类型设置 dacl 和四种不同类型的 Sacl。

-   **标志**用于描述此 ACE 的子对象的 Sacl 的审核和警报策略继承的字段。

-   **Rights**字段指示哪些权限是授予或拒绝 ACE。 此字段可以指定特定的数字值，该值指示适用于此 ACE 的泛型、 标准版和特定权限，或使用公共访问权限的字符串说明。

-   如果 DACL 受到特定于对象的 ACE 结构的 GUID 对象。

-   继承的对象 GUID 如果 DACL 受到特定于对象的 ACE 结构

-   一个，该值指示此 ACE 所应用到的安全实体的 SID。

因此，解释示例安全描述符，"A"导致 ACE 指示这是一个"允许访问"项。 替代项为"拒绝访问"项，后者仅不常使用，并由前导"D"字符表示。 **标志**字段指定容器继承 (CI)，这表示此 ACE 由子对象继承。

**Rights**字段值进行编码的特定权限，包括泛型权利和标准的权限。 例如，"GR"表示"泛型读取"访问权限，"GA"表示"泛型所有"访问权限，这两者都是通用的权限。 特殊权限的数目，请遵循这些泛型权利。 在上例中，"CC"指示创建子访问权限，这是特定于文件和目录的权限。 上面的示例还包括其他标准权限时后删除子访问，包括"DC"的"CC"字符串"LC"列表子访问，为自右键访问"软件"为"RP"读取属性访问、 标准的"SD"删除访问权限和"RC"读取的控制访问.

上面的示例中的 SID 条目字符串包括"PU"用于 power users"BU"为内置 users"BA"的"内置的管理员，为本地服务帐户，为本地系统"SY"和"NS"网络服务帐户的"LS"。 因此在上面的示例中，为用户提供通用的读取访问权限的对象上。 与此相反，有内置管理员、 本地服务帐户、 本地系统和网络服务提供通用的所有访问权限 （读取、 写入和执行）。 Windows SDK 中记录了所有可能的权限和标准 SID 字符串的完整集。

这些 Acl 将应用于给定的驱动程序创建的所有设备对象。 驱动程序还可以通过使用新函数，控制特定对象的安全设置[ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)，当创建一个命名的设备对象。 **IoCreateDeviceSecure**函数是适用于 Windows XP Service Pack 1 和 Windows Server 2003 及更高版本。 使用**IoCreateDeviceSecure**，使用适用于设备对象的完整安全描述符定义语言子集描述要应用于设备对象的安全描述符。

将特定的安全描述符应用到的设备对象的用途是确保应用程序尝试访问设备本身时，针对设备执行适当的安全检查。 包含名称结构 （文件系统，例如的命名空间） 的设备对象，用于管理此设备命名空间的访问权限的详细信息属于该驱动程序，不适用于 I/O 管理器。

在这些情况下一个有趣的问题是如何处理 I/O 管理器负责检查访问驱动程序设备对象和设备驱动程序，可实现任何安全策略是适当的驱动程序之间的边界的安全性。 传统上，打开的对象是否在设备本身的名称，I/O 管理器将执行对直接使用其安全描述符的设备对象的完全访问权限检查。 但是，如果要打开该对象指示驱动程序本身内的路径，I/O 管理器仅会检查以确保遍历访问权限授予设备对象。 因为大多数线程已被授予通常情况下，授予适当此遍历**SeChangeNotifyPrivilege**，这对应于授予从右到目录遍历。 通常情况下，不支持结构的设备将请求 I/O 管理器执行完整的安全检查。 这是通过设置**文件\_设备\_SECURE\_打开**位设备特征字段中。 包括此类设备对象的组合的驱动程序应设置为这些设备不支持结构的这一特性。 例如，文件系统会将其命名的设备对象 （它不支持命名结构），此选项设置，但不是会设置此选项未命名的设备对象 （卷，例如），支持命名结构上。 无法设置此位正确是驱动程序中的常见 bug，可允许与设备不适当的访问。 使用附件接口的驱动程序 ([**IoAttachDeviceToDeviceStackSafe**](https://msdn.microsoft.com/library/windows/hardware/ff548236)，例如)，则**文件\_设备\_安全\_打开**如果驱动程序将附加到的设备中设置此字段设置位。 因此，筛选器驱动程序无需担心此特定方面的安全检查。

 

 




