---
title: 适用于驱动程序开发人员的 Windows 安全模型
description: Windows 安全模型主要基于每个对象的权限，具有少量的系统范围权限。
ms.assetid: 3A7ECA7C-1FE6-4ADB-97A9-A61C6FCE9F04
ms.date: 02/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 687aab736b2b8921ce6bf0af52f00deb2f73aaef
ms.sourcegitcommit: 6c42efc074ab939e7737d6c2b016d3f3a75954e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90741022"
---
# <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanwindows-security-model-for-driver-developers"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>驱动程序开发人员的 Windows 安全模型

Windows 安全模型基于安全对象。 操作系统的每个组件必须确保其负责的对象的安全性。 因此，驱动程序必须保护其设备和设备对象的安全性。

本主题概述了如何将 Windows 安全模型应用于内核模式驱动程序。 


## <a name="windows-security-model"></a>Windows 安全模型

Windows 安全模型主要基于每个对象的权限，具有少量的系统范围权限。 可以保护的对象包括（但不限于）进程、线程、事件和其他同步对象以及文件、目录和设备。

对于每种类型的对象，一般的 "读取"、"写入" 和 "执行" 权限映射到特定于对象的特定权限。 例如，对于文件和目录，可能的权限包括读取或写入文件或目录的权限、读取或写入扩展文件属性的权限、遍历目录的权限以及写入对象的安全描述符的权限。 

安全模式涉及以下概念：

-   Sid)  (安全标识符
-   访问令牌
-   安全描述符
-   访问控制列表 (ACL)
-   权限

### <a name="span-idsecurity_identifiers__sids_spanspan-idsecurity_identifiers__sids_spanspan-idsecurity_identifiers__sids_spansecurity-identifiers-sids"></a><span id="Security_Identifiers__SIDs_"></span><span id="security_identifiers__sids_"></span><span id="SECURITY_IDENTIFIERS__SIDS_"></span>Sid)  (安全标识符


安全标识符 (SID，也称为 *主体*) 标识用户、组或登录会话。 每个用户都有一个唯一的 SID，由操作系统在登录时检索。

Sid 由操作系统或域服务器等机构颁发。 某些 Sid 是众所周知的，并且具有名称和标识符。 例如，SID S-1-1-0 标识每个人 (或世界) 。


### <a name="access-tokens"></a>访问令牌

每个进程都有一个访问令牌。 访问令牌描述进程的完整安全上下文。 它包含用户的 SID、用户所属的组的 SID 和登录会话的 SID，以及向用户授予的系统范围的特权的列表（& a）。

默认情况下，只要进程的线程与安全对象进行交互，系统就会对进程使用主访问令牌。 但是，线程可以模拟客户端帐户。 当线程模拟时，它除了具有其自己的主令牌外，还具有一个模拟令牌。 模拟标记描述线程正在模拟的用户帐户的安全上下文。 模拟在远程过程调用 (RPC) 处理中尤其常见。

描述线程或进程受限安全上下文的访问令牌称为受限令牌。 *受限令牌*中的 sid 只能设置为拒绝访问，而不允许访问安全对象。 此外，令牌可以描述有限的系统范围权限集。 用户的 SID 和标识保持不变，但用户的访问权限会受到限制，而此过程使用的是受限令牌。 [CreateRestrictedToken](/windows/win32/api/securitybaseapi/nf-securitybaseapi-createrestrictedtoken)函数创建受限制的令牌。


### <a name="security-descriptors"></a>安全描述符

每个命名的 Windows 对象都有一个安全描述符;某些未命名对象也会这样做。 安全描述符介绍对象及其 Acl 的所有者和组 Sid。

对象的安全描述符通常由创建对象的函数创建。 当驱动程序调用 [IoCreateDevice](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 或 [IoCreateDeviceSecure](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 例程来创建设备对象时，系统会将安全描述符应用到创建的设备对象，并为该对象设置 acl。 对于大多数设备，Acl 是在设备信息 (INF) 文件中指定的。

有关详细信息，请参阅内核驱动程序文档中的 [安全描述符](../kernel/security-descriptors.md) 。

### <a name="access-control-lists"></a>访问控制列表

访问控制列表 (Acl) 启用对对象访问的精细控制。 ACL 是每个对象的安全描述符的组成部分。

每个 ACL 都包含零个或多个 (ACE) 的访问控制项。 相反，每个 ACE 都包含单个用于标识用户、组或计算机的 SID，以及该 SID 的已拒绝或允许的权限的列表。

### <a name="acls-for-device-objects"></a>设备对象的 Acl

可以通过以下三种方式之一设置设备对象的 ACL：

-   为其设备类型设置默认安全描述符。
-   由 **RtlCreateSecurityDescriptor** 函数以编程方式创建并由 **RtlSetDaclSecurityDescriptor** 函数设置。
-   在安全描述符定义语言 (SDDL) 在设备的 INF 文件中或在对 **IoCreateDeviceSecure** 例程的调用中指定。

所有驱动程序都应使用 INF 文件中的 SDDL 为其设备对象指定 Acl。

SDDL 是一种可扩展的描述语言，可让组件以字符串格式创建 Acl。 SDDL 由用户模式和内核模式代码使用。 下图显示了设备对象的 SDDL 字符串的格式。

![设备对象的 sddl 字符串](images/wsm-sddlstrings.gif)

访问值指定允许的访问类型。 SID 值指定一个安全标识符，该标识符确定访问值适用的目标 (例如，用户或组) 。

例如，以下 SDDL 字符串允许 System (SY) 对所有内容的访问，并允许 (WD 的所有用户仅) 读取访问权限：

``` syntax
“D:P(A;;GA;;;SY)(A;;GR;;;WD)”
```

标头文件 wdmsec 还包括一组适用于设备对象的预定义 SDDL 字符串。 例如，标头文件定义 SDDL \_ DEVOBJ \_ SYS \_ ALL \_ ADM \_ RWX \_ WORLD \_ RWX \_ RES \_ RWX，如下所示：

``` syntax
"D:P(A;;GA;;;SY)(A;;GRGWGX;;;BA)(A;;GRGWGX;;;WD)(A;;GRGWGX;;;RC)"
```

此字符串的第一段允许内核和操作系统 (SY) 对设备的完全控制。 第二段允许内置管理员 (组中的任何人) 访问整个设备，但不允许更改 ACL。 第三段允许 (WD) 的每个人读取或写入设备，第四段允许 (RC) 向不受信任的代码授予相同的权限。 驱动程序可以将预定义的字符串按原样使用，也可以作为特定于设备对象的字符串的模型使用。

堆栈中的所有设备对象应具有相同的 Acl。 更改堆栈中一个设备对象上的 Acl 将更改整个设备堆栈上的 Acl。

但是，如果将新设备对象添加到堆栈中，则不会更改任何 Acl，无论是新设备对象的 acl) 还是堆栈中任何现有设备对象的 Acl 都 (。 当驱动程序创建新的设备对象并将其附加到堆栈顶部时，驱动程序应该通过从下一个较低的驱动程序复制 **DeviceObject** 字段，将堆栈的 acl 复制到新设备对象。

**IoCreateDeviceSecure**例程支持使用预定义 SID 的 SDDL 字符串子集，如 WD 和 SY。 用户模式 Api 和 INF 文件支持完整的 SDDL 语法。

### <a name="security-checks-using-acls"></a>使用 Acl 的安全检查

当某个进程请求对某个对象的访问权限时，安全检查会对照调用方的访问令牌中的 Sid 来比较对象的 Acl。

系统会按严格的自顶向下顺序比较 Ace 并在第一个相关匹配上停止。 因此，在创建 ACL 时，应始终将拒绝 Ace 置于相应的 grant Ace 之上。 下面的示例演示了如何进行比较。

**示例1：将 ACL 与访问令牌进行比较**

示例1显示系统如何将 ACL 与调用方进程的访问令牌进行比较。 假设调用方想要打开具有下表所示 ACL 的文件。

**示例文件 ACL**

| 权限 | SID        | Access                |
|------------|------------|-----------------------|
| Allow      | 计帐 | 写入、删除         |
| Allow      | Sales      | 追加                |
| 拒绝       | Legal      | 追加、写入、删除 |
| Allow      | 所有人   | 读取                  |

 

此 ACL 具有四个 Ace，特别适用于会计、销售、法律和 Everyone 组。

接下来，假定请求进程的访问令牌包含一个用户和三个组的 Sid，顺序如下：

用户 Jim (S-1-5-21 ... ) 

组记帐 (S-1-5-22 ... ) 

组合法 (S-1-5-23 ... ) 

将所有人分组 (S-1-1-0) 

将文件 ACL 与访问令牌进行比较时，系统首先会在文件的 ACL 中查找用户 Jim 的 ACE。 显示 "无"，因此下一步它查找会计组的 ACE。 如上表所示，会计组的 ACE 显示为文件 ACL 中的第一项，因此 Jim 的进程被授予写入或删除该文件的权限，比较停止。 如果该合法组的 ACE 在 ACL 中的会计组前面带有 ACE，则该进程将被拒绝写入、追加和删除对该文件的访问权限。

**示例2：将 ACL 与受限制的令牌进行比较**

系统将 ACL 与受限制的令牌进行比较，其方式与在不受限制的令牌中比较它们的方式相同。 但是，受限制的令牌中的拒绝 SID 只能与 ACL 中的拒绝 ACE 匹配。

示例2显示系统如何将文件的 ACL 与受限制的令牌进行比较。 假定该文件具有与上表中显示的相同的 ACL。 但在此示例中，该进程具有包含以下 Sid 的受限令牌：

用户 Jim (S-1-5-21 ) 拒绝

组记帐 (S-1-5-22 ... ) 拒绝

组合法 (S-1-5-23 ... ) 拒绝

将所有人分组 (S-1-1-0) 

该文件的 ACL 不会列出 Jim 的 SID，因此系统将继续到会计组 SID。 尽管该文件的 ACL 包含用于会计组的 ACE，但此 ACE 允许访问;因此，它与拒绝访问的进程的受限令牌中的 SID 不匹配。 因此，系统会继续到法律组 SID。 文件的 ACL 包含拒绝访问的法律组 ACE，因此该进程无法写入、追加或删除该文件。

### <a name="privileges"></a>权限


权限是用户在本地计算机上执行与系统相关的操作的权利，例如加载驱动程序、更改时间或关闭系统。

权限不同于访问权限，因为它们适用于与系统相关的任务和资源，而不是与对象相关，因为它们被系统管理员分配给用户或组，而不是由操作系统分配给用户或组。

每个进程的访问令牌都包含授予该进程的特权列表。 必须在使用之前专门启用特权。 有关权限的详细信息，请参阅内核驱动程序文档中的 [权限](../kernel/privileges.md) 。

 

## <a name="span-idcreating-a-filespanspan-idcreating-a-filespanspan-idcreating-a-filespanwindows-security-model-scenario-creating-a-file"></a><span id="Creating-A-File"></span><span id="CREATING-A-FILE"></span><span id="creating-a-file"></span>Windows 安全模型方案：创建文件

只要进程创建文件或对象的句柄，系统就会使用 Windows 安全模型中所述的安全构造。

下图显示了在用户模式进程尝试创建文件时触发的与安全相关的操作。

![创建如下所述的文件示例](images/wsm-creatingafile.gif)

上图显示了在用户模式应用程序调用 **CreateFile** 函数时系统如何做出响应。 以下说明引用了图中的带圆圈数字：

1.  用户模式应用程序会调用 **CreateFile** 函数，并传递一个有效的 Microsoft Win32 文件名。
2.  用户模式 Kernel32.dll 将请求传递到 Ntdll.dll，后者将 Win32 名称转换为 Microsoft Windows NT 文件名。
3.  Ntdll.dll 调用具有 Windows 文件名的 **NtCreateFile** 函数。 在 Ntoskrnl.exe 中，i/o 管理器处理 **NtCreateFile**。
4.  I/o 管理器将请求重新打包到对象管理器调用。
5.  对象管理器解析符号链接，并确保用户对要在其中创建文件的路径具有遍历权限。 有关详细信息，请参阅 [对象管理器中的安全检查](#omchecks)。
6.  对象管理器调用拥有与请求关联的基础对象类型的系统组件。 对于文件创建请求，此组件是拥有设备对象的 i/o 管理器。
7.  I/o 管理器根据用户进程的访问令牌检查设备对象的安全描述符，以确保用户具有所需的设备访问权限。 有关详细信息，请参阅 [I/o 管理器中的安全检查](#iomanchecks)。
8.  如果用户进程具有所需的访问权限，则 i/o 管理器会创建一个句柄，并将 IRP \_ MJ \_ CREATE 请求发送到设备或文件系统的驱动程序。
9.  驱动程序根据需要执行其他安全检查。 例如，如果请求在设备的命名空间中指定一个对象，则驱动程序必须确保调用方具有所需的访问权限。 有关详细信息，请参阅 [驱动程序中的安全检查](#driver)。

### <a name="span-idomchecksspanspan-idomchecksspansecurity-checks-in-the-object-manager"></a><span id="omchecks"></span><span id="OMCHECKS"></span>对象管理器中的安全检查

检查访问权限的责任属于可执行此类检查的最高级别的组件。 如果对象管理器可以验证调用方的访问权限，则它会执行此操作。 如果不是，则对象管理器将请求传递给负责基础对象类型的组件。 然后，该组件会验证访问权限（如果可以）;如果不能，它会将请求传递到一个仍较低的组件，如驱动程序。

对象管理器检查 Acl 中的简单对象类型，如事件和互斥锁。 对于具有命名空间的对象，类型所有者将执行安全检查。 例如，i/o 管理器被视为设备对象和文件对象的类型所有者。 如果对象管理器在分析名称时找到设备对象或文件对象的名称，则它会将名称作为前面介绍的文件创建方案的名称。 然后，i/o 管理器会检查访问权限（如果可能）。 如果该名称指定了设备命名空间中的对象，则 i/o 管理器会依次将该名称强行关闭到设备 (或文件系统) 驱动程序，并且该驱动程序负责验证请求的访问权限。

### <a name="span-idiomanchecksspanspan-idiomanchecksspansecurity-checks-in-the-io-manager"></a><span id="iomanchecks"></span><span id="IOMANCHECKS"></span>I/o 管理器中的安全检查

当 i/o 管理器创建句柄时，它会对照进程访问令牌检查该对象的权限，然后将授予该用户的权限连同句柄一起存储。 以后 i/o 请求到达时，i/o 管理器将检查与句柄关联的权限，以确保该进程有权执行请求的 i/o 操作。 例如，如果稍后处理请求写入操作，i/o 管理器将检查与句柄关联的权限，以确保调用方具有对对象的写访问权限。 

如果复制了句柄，则可以从副本中删除权限，但不能将其添加到其中。

当 i/o 管理器创建对象时，它会将一般的 Win32 访问模式转换为特定于对象的权限。 例如，以下权限适用于文件和目录：


| Win32 访问模式 | 特定于对象的权限 |
|-------------------|------------------------|
|   通用 \_ 读取   |        ReadData        |
|  泛型 \_ 写入   |       WriteData        |
| 泛型 \_ 执行  |     ReadAttributes     |
|   \_全部通用    |          全部           |
 
若要创建文件，进程必须对目标路径中的父目录具有遍历权限。 例如，若要创建 \\ 设备 \\ CDROM0 \\ 目录 \\File.txt，进程必须有权遍历 \\ 设备、 \\ 设备 \\ CDROM0 和 \\ 设备 \\ CDROM0 \\ 目录。 I/o 管理器仅检查这些目录的遍历权限。

在分析文件名时，i/o 管理器会检查遍历权限。 如果文件名为符号链接，则 i/o 管理器会将其解析为完整路径，然后检查遍历权限（从根开始）。 例如，假设符号链接 \\ DosDevices \\ D 映射到 Windows NT 设备名称 \\ device \\ CDROM0。 该进程必须具有设备目录的遍历权限 \\ 。

有关详细信息，请参阅 [对象句柄](../kernel/object-handles.md) 和 [对象安全](https://docs.microsoft.com/windows-hardware/drivers/kernel/object-security)。

### <a name="span-iddriverspanspan-iddriverspansecurity-checks-in-the-driver"></a><span id="driver"></span><span id="DRIVER"></span>驱动程序中的安全检查

操作系统内核会将每个驱动程序视为具有自己的命名空间的文件系统。 因此，当调用方尝试在设备命名空间中创建对象时，i/o 管理器会检查进程是否有权使用路径中的目录。 

对于 WDM 驱动程序，除非已创建指定 FILE_DEVICE_SECURE_OPEN 的设备对象，否则 i/o 管理器不会对该命名空间执行安全检查。  如果未设置 FILE_DEVICE_SECURE_OPEN，驱动程序将负责确保其命名空间的安全性。 有关详细信息，请参阅 [控制设备命名空间访问](../kernel/controlling-device-namespace-access.md) 和 [保护设备对象](../kernel/controlling-device-access.md)。

对于 WDF 驱动程序，将始终设置 FILE_DEVICE_SECURE_OPEN 标志，以便在允许应用程序访问设备的命名空间中的任何名称之前，将检查设备的安全描述符。 有关详细信息，请参阅 [在 KMDF 驱动程序中控制设备访问](../wdf/controlling-device-access-in-kmdf-drivers.md)。



## <a name="windows-security-boundaries"></a>Windows 安全边界

相互通信的驱动程序和不同权限级别的用户模式调用方可以视为跨信任边界。 信任边界是从较低特权进程到较高特权进程的任何代码执行路径。

权限级别越高，差异的可能性就越多，要执行攻击的攻击者（如针对目标驱动程序或进程的权限提升攻击）的可能性就越多。

创建威胁模型的过程的一部分是检查安全边界并查找意外路径。 有关详细信息，请参阅 [驱动程序的威胁建模](threat-modeling-for-drivers.md)。 

跨信任边界的任何数据都不受信任，必须进行验证。 

此图显示了三个内核驱动程序和两个应用，一个应用容器，一个应用以管理员权限运行。 红线指示示例信任边界。

![显示三个内核驱动程序和两个应用程序（一个在应用程序容器中）的驱动程序攻击面](images/driver-security-attack-surface.png)

由于应用容器可以提供额外的限制，并且没有在管理级别运行，因此，路径 (1) 会成为升级攻击的更高风险路径，因为信任边界在应用容器 ( 非常低的特权进程) 和内核驱动程序。 

路径 (2) 的风险更低，因为该应用程序以管理员权限运行，并且正直接调用内核驱动程序。 管理员已经是系统上的一个相当高的特权，因此，从管理员到内核的攻击面对于攻击者来说不是一个有趣的目标，而是值得注意的信任边界。

路径 (3) 是与多个信任边界交叉的代码执行路径的示例，如果不创建威胁模型，则该路径会丢失。
在此示例中，驱动程序1和驱动程序3之间存在信任边界，因为驱动程序1从用户模式应用中获取输入并将其直接传递到驱动程序3。

从用户模式进入驱动程序的所有输入都不受信任，应进行验证。 来自其他驱动程序的输入也可能是不受信任的，具体取决于先前的驱动程序是否只是简单的传递 (（例如，数据是由应用程序1中的驱动程序1接收的），驱动程序1不对数据进行任何验证，只是将数据传递给驱动程序 3) 。 请确保通过创建完整的威胁模型来识别所有攻击面和信任边界，并验证与它们交叉的所有数据。


## <a name="windows-security-model-recommendations"></a>Windows 安全模型建议 

-   在对 **IoCreateDeviceSecure** 例程的调用中设置强默认 acl。
-   为每个设备指定 INF 文件中的 Acl。 如果需要，这些 Acl 可以放宽严格的默认 Acl。
-   设置 "文件 \_ 设备 \_ 安全 \_ 打开" 特性，将设备对象安全设置应用到设备命名空间。
-   不要定义允许文件任何访问的 IOCTLs， \_ \_ 除非恶意利用此类访问权限。
-   使用 **IoValidateDeviceIoControlAccess** 例程提高允许文件 \_ 任何访问权限的现有 IOCTLS 的安全性 \_ 。
-   创建威胁模型以检查安全边界并查找意外路径。 有关详细信息，请参阅 [驱动程序的威胁建模](threat-modeling-for-drivers.md)。 
-   有关其他驱动程序安全建议，请参阅 [驱动程序安全核对清单](driver-security-checklist.md) 。


### <a name="see-also"></a>另请参阅

[保护设备对象](../kernel/controlling-device-access.md)

[驱动程序安全清单](driver-security-checklist.md)