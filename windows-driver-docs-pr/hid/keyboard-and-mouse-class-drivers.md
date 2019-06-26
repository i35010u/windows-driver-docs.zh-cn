---
title: 键盘和鼠标类驱动程序
description: 非 HID 键盘和鼠标可以通过多个旧式总线连接，但仍使用相同的类驱动程序。
ms.assetid: 0771D802-4F1D-4612-8376-ED3113DCC652
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d44c3ddb3563d0d1f5f8d40f947656a6d4c882f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384838"
---
# <a name="keyboard-and-mouse-class-drivers"></a>键盘和鼠标类驱动程序


非 HID 键盘和鼠标可以通过多个旧式总线连接，但仍使用相同的类驱动程序。 本部分包含的类驱动程序本身的详细信息。 在控制器上，以下各节将进入的详细信息。

本主题介绍典型的物理配置的键盘和鼠标设备在 Microsoft Windows 2000 及更高版本。

下图显示两个采用单一键盘和鼠标的常见配置。

![说明采用单一键盘和鼠标的两个配置的关系图](images/kemocfg1.png)

在左侧图显示了键盘和鼠标连接到系统总线通过独立的控制器。 典型配置由运营 i8042 控制器通过 PS/2 式键盘和通过串行端口控制器操作序列样式鼠标组成。

以下附加信息非常重要的键盘和鼠标制造商：

-   键盘以独占方式打开由操作系统堆栈出于安全原因
-   Windows 支持多个键盘和鼠标设备的同时进行连接。
-   Windows 不支持到每个设备的客户端通过独立的访问。

## <a name="class-driver-features"></a>类驱动程序功能


本主题介绍以下 Microsoft Windows 2000 和更高版本的系统类驱动程序的功能：

-   **Kbdclass**，设备的 GUID 的类驱动程序\_类\_键盘设备类

-   **Mouclass**，设备的 GUID 的类驱动程序\_类\_鼠标设备类

Kbdclass 实现 Kbdclass 服务，其可执行映像将 kbdclass.sys。

Mouclass 实现 Mouclass 服务，其可执行映像将 mouclass.sys。

Kbdclass 和 Mouclass 每项功能：

-   设备类的泛型和独立于硬件的操作。

-   Plug and Play、 电源管理和 Windows Management Instrumentation (WMI)。

-   旧设备的操作。

-   多个设备同步操作。

-   连接[类服务的回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/kbdmou/nc-kbdmou-pservice_callback_routine)功能驱动程序用于将数据从设备的输入的数据缓冲区传输到的数据缓冲区的类驱动程序。

## <a name="configuration-of-device-objects"></a>设备对象的配置


下图显示了插 PS/2-样式键盘和鼠标设备的设备对象的配置。 每个类驱动程序将创建一个较高级别类*筛选设备对象*（筛选器执行操作） 附加到函数设备对象 (*FDO*) 通过可选的较高级别设备筛选器执行操作。 较高级别设备筛选器驱动程序创建的较高级别设备筛选器执行操作。 I8042prt 创建函数执行操作，并将其附加到一个物理设备对象 (*PDO*) 创建的根总线驱动程序。

![说明的插 ps/2 式键盘和鼠标设备的设备对象的配置的关系图](images/km-ovr2.png)

*Ps/2 键盘*

键盘驱动程序堆栈由以下内容组成。

-   Kbdclass，较高级别键盘类筛选器驱动程序
-   一个或多个可选的较高级别键盘筛选器驱动程序
-   I8042prt，功能驱动程序

*Ps/2 鼠标*

鼠标驱动程序堆栈由以下内容组成。

-   Mouclass，较高级别鼠标类筛选器驱动程序
-   一个或多个可选的较高级别鼠标筛选器驱动程序
-   I8042prt，功能驱动程序

Kbdclass 和 Mouclass 可以在两个不同的模式下支持多个设备。 在中*一对一模式*，每个设备都有一个独立设备堆栈。 在类驱动程序创建，并将一个独立的类附加到每个设备堆栈。 每个设备堆栈都有其自己的控件状态和输入的缓冲区。 Microsoft Win32 子系统访问每个设备通过唯一的文件对象中的输入。

在中*grandmaster 模式*，类驱动程序将所有设备都运行如下所示：

-   类驱动程序创建这*grandmaster 类是否*表示的所有设备和一个*从属类执行*为每个设备。

    在类驱动程序将附加到每个设备堆栈的从属类执行操作。 下面的从属类执行操作，设备堆栈是为与在一对一模式下创建相同的。

-   Grandmaster 类执行控制所有从属 DOs 的操作。

-   Win32 子系统通过表示 grandmaster 类设备的文件对象来访问设备的所有输入。

-   所有设备输入 grandmaster 数据队列中进行缓冲处理。

-   Grandmaster 维护单个全局设备状态。

在一对一模式下如果操作 Kbdclass 和 Mouclass 注册表条目值，其**ConnectMultiplePorts**设置为 0x00 (项下**HKLM\\Services\\CurrentControlSet\\ ***&lt;类服务&gt;***\\参数**，其中*类服务*Kbdclass 或 Mouclass)。 否则 Kbdclass 和 Mouclass 在 grandmaster 模式下操作。

## <a name="open-and-close-via-the-class-driver"></a>打开和关闭通过类驱动程序


Microsoft Win32 子系统打开供其独占使用的所有键盘和鼠标设备。 对于每个设备类，Win32 子系统处理时输入来自单个输入设备来处理来自所有设备的输入。 应用程序不能请求从只有一个特定的设备接收输入。

从插管理器收到通知后的 Win32 子系统将动态打开插输入的设备的一个 GUID\_类\_键盘或 GUID\_类\_鼠标设备接口已启用。 Win32 子系统关闭插设备接收通知，禁用打开的接口之后。 Win32 子系统还按名称打开旧设备 (例如，"\\设备\\KeyboardLegacyClass0")。 请注意，Win32 子系统已成功打开后旧设备，它不能确定是否更高版本以物理方式删除该设备。

Kbdclass 和 Mouclass 收到创建请求后它们将执行以下操作插和旧的操作：

-   **Plug and Play 操作**

    如果设备处于即插即用和播放已启动状态，在类驱动程序将发送 IRP\_MJ\_向驱动程序堆栈下的创建请求。 否则类驱动程序完成请求，而无需发送关闭驱动程序堆栈请求。 在类驱动程序设置具有读取访问权限的设备的受信任的文件。 如果没有 grandmaster 设备，在类驱动程序将创建请求发送到与从属类设备相关联的所有端口。

-   **旧的操作**

    在类驱动程序将内部设备控制请求发送到端口驱动程序，以使设备。

## <a name="connect-a-service-callback-to-a-device"></a>连接到设备的服务回调


类驱动程序必须连接到设备及其服务级别，然后才能打开设备。 类驱动程序连接其类服务后它们附加到设备堆栈类执行操作。 功能驱动程序使用类服务回调将输入的数据从设备传输到设备的类数据队列。 设备功能驱动程序的 ISR 调度完成例程调用类服务回调。 Kbdclass 提供类服务回调[ **KeyboardClassServiceCallback**](https://docs.microsoft.com/previous-versions/ff542324(v=vs.85))，并 Mouclass 提供类服务回调[ **MouseClassServiceCallback**](https://docs.microsoft.com/previous-versions/ff542394(v=vs.85)).

供应商可以通过安装设备的较高级别筛选器驱动程序更改类服务回调的操作。 示例筛选器驱动程序[Kbfiltr](https://go.microsoft.com/fwlink/p/?linkid=256125)定义[ **KbFilter\_ServiceCallback** ](https://docs.microsoft.com/previous-versions/ff542297(v=vs.85))回调和示例筛选器驱动程序[Moufiltr](https://go.microsoft.com/fwlink/p/?linkid=256135)定义[ **MouFilter\_ServiceCallback** ](https://docs.microsoft.com/previous-versions/ff542380(v=vs.85))回调。 示例筛选器服务回调可以配置为修改的输入的数据，从设备的端口输入缓冲区传输到类数据队列。 例如，筛选器服务回调可以删除、 转换或插入数据。

按以下方式连接的类和筛选器服务回调：

-   在类驱动程序发送内部设备连接设备在堆栈的下层的请求 ([**IOCTL\_内部\_键盘\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/kbdmou/ni-kbdmou-ioctl_internal_keyboard_connect)或[ **IOCTL\_内部\_鼠标\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/kbdmou/ni-kbdmou-ioctl_internal_mouse_connect))。 类将数据连接的连接指定\_数据结构，其中包括指向类设备对象和一个指向类服务回调。

-   筛选器驱动程序收到连接请求后，它将保存一份类连接数据，并使用筛选器连接数据替换请求的连接数据。 筛选器将数据连接指定的筛选器设备对象指针和指向筛选器驱动程序服务回调。 然后，筛选器驱动程序将筛选的连接请求发送到功能驱动程序。

类和筛选器服务回调调用如下所示：

-   该函数驱动程序使用筛选器连接的数据，使初始回调到筛选器服务回调。

-   筛选输入的数据后, 筛选器服务回调使用此类连接保存它以对类服务回调进行回调的数据。

## <a name="query-and-set-a-keyboard-device"></a>查询和设置键盘设备


I8042prt 支持以下内部设备控制请求有关的键盘设备，以及键盘设备上设置参数的查询信息：

[**IOCTL\_键盘\_查询\_属性**](https://docs.microsoft.com/windows/desktop/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_query_attributes)

[**IOCTL\_键盘\_查询\_指示器\_翻译**](https://docs.microsoft.com/windows/desktop/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_query_indicator_translation)

[**IOCTL\_键盘\_查询\_指示器**](https://docs.microsoft.com/windows/desktop/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_query_indicators)

[**IOCTL\_键盘\_查询\_字符重复**](https://docs.microsoft.com/windows/desktop/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_query_typematic)

[**IOCTL\_键盘\_设置\_指示器**](https://docs.microsoft.com/windows/desktop/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_set_indicators)

[**IOCTL\_键盘\_设置\_字符重复**](https://docs.microsoft.com/windows/desktop/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_set_typematic)

有关所有键盘设备控制请求的详细信息，请参阅[I8042prt 键盘内部设备控制请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

## <a name="scan-code-mapper-for-keyboards"></a>扫描码映射程序键盘


Microsoft Windows 操作系统中提供的输入设备的 ps/2 扫描代码转换为虚拟键，通过 Windows 消息的窗体中的系统传播。 如果设备生成某些密钥不正确的扫描代码，将发送错误的虚拟键消息。 这可以通过编写的筛选器驱动程序，可以分析生成的固件的扫描代码并修改系统理解的一个不正确的扫描代码修复。 但是，这是一个乏味的过程，可能有时会导致严重问题，如果内核级筛选器驱动程序中存在错误。

Windows 2000 和 Windows XP 包括一个新扫描代码映射器，它提供一种允许的扫描代码映射的方法。 Windows 扫描代码映射存储在以下注册表项：

``` syntax
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout
```

**请注意**  此外，还有**键盘布局**不应修改控制密钥，但该注册表项下的项 （请注意，复数形式）。

 

在中**键盘布局**密钥**Scancode 映射**必须添加值。 此值为类型 REG\_（little Endian 格式） 的二进制文件中，并且在下表中指定的数据格式。

|                         |                 |                              |
|-------------------------|-----------------|------------------------------|
| 开始偏移量 （以字节为单位） | 大小 （以字节为单位） | 数据                         |
| 0                       | 4               | 标头：版本信息  |
| 4                       | 4               | 标头：Flags                |
| 8                       | 4               | 标头：映射数   |
| 12                      | 4               | 单独的映射           |
| ...                     | ...             | ...                          |
| 最后 4 个字节            | 4               | 空终止符 (0x00000000) |

 

第一个和第二个 dword 值存储标头信息，并应设置为零的扫描代码映射器的当前版本。 第三个 DWORD 项保存的遵循，包括 null 终止的映射的映射数总数的计数。 因此，最小计数应为 1 （无指定的映射）。 单项映射按照标头。 每个映射是一个 dword 值的长度，并且分为两个单词长度字段。 每个 WORD 字段存储要映射的键的扫描代码。

一旦映射存储在注册表中，系统必须重新启动的映射才会生效。 请注意，是否在按键上必要的扫描代码映射，该步骤执行在用户模式下之前的扫描代码转换为虚拟键。 此转换在用户模式下可以存在某些限制，例如未正常工作，在终端服务下运行时的映射。

若要删除这些映射，Scancode 映射注册表值中删除并重新启动。

*示例 1*

下面提供了一个示例。 若要交换 CAPS LOCK 键与左的 CTRL 键，使用注册表编辑器 (最好是 Regedt32.exe) 修改 Scancode 映射键具有以下值：

``` syntax
00000000 00000000 03000000 3A001D00 1D003A00 00000000
```

下表包含这些项分解为 DWORD 字段和交换的字节数。

|            |                                                    |
|------------|----------------------------------------------------|
| ReplTest1      | 解释                                     |
| 0x00000000 | 标头：“版本”旁边的数字。 设置为零。                |
| 0x00000000 | 标头：标志。 设置为零。                  |
| 0x00000003 | 地图 （包括 null 项） 中的三个条目。   |
| 0x001D003A | 左 CTRL 键-&gt; CAPS LOCK (0x1D-&gt; 0x3A)。 |
| 0x003A001D | CAPS LOCK-&gt;左 CTRL 键 (0x3A-&gt; 0x1D)。 |
| 0x00000000 | Null 终止符。                                   |

 

*示例 2*

还有可能键盘上添加密钥通常不可用或删除从未使用过的密钥。 下面的示例演示中存储的值**Scancode 映射**删除右 CTRL 键并更改要静音键作为工作的右边的 ALT 键的功能：

``` syntax
00000000 00000000 03000000 00001DE0 20E038E0 00000000
```

下表包含这些项分解为 DWORD 字段和交换的字节数。

|            |                                                       |
|------------|-------------------------------------------------------|
| ReplTest1      | 解释                                        |
| 0x00000000 | 标头：“版本”旁边的数字。 设置为零。                   |
| 0x00000000 | 标头：标志。 设置为零。                     |
| 0x00000003 | 地图 （包括 null 项） 中的三个条目。      |
| 0xE01D0000 | 删除右 CTRL 键 (0xE01D-&gt; 0x00)。       |
| 0xE038E020 | 右 ALT 键-&gt;静音键 (0xE038-&gt; 0xE020)。 |
| 0x00000000 | Null 终止符。                                      |

 

生成所需的数据后，它能够将其插入注册表中通过多种方式。

-   可以生成的.reg 文件，可以轻松地合并到系统注册表使用注册表编辑器。
-   此外可以使用创建的.inf 文件\[AddReg\]节，其中包含要添加的注册表信息。
-   可以使用 Regedt32.exe 手动将信息添加到注册表。

扫描代码映射器有几个优点和缺点。

优点包括：

-   映射器可以作为简单的解决方法，用于更正固件错误。
-   通过修改注册表中的映射，经常使用的键可以添加到键盘。 可以映射到 null （删除） 或为其他密钥交换密钥不是通常使用 （例如右 CTRL 键）。
-   可以轻松地更改密钥的位置。 用户可以轻松地自定义其权益的常用项的位置。

识别以下缺点：

-   映射存储在注册表中后, 重新启动系统需要激活它。
-   存储在注册表中的映射在系统级别上工作，并将应用于所有用户。 无法设置这些映射为具体取决于当前用户的工作方式不同。
-   当前实现将限制映射的功能，以便映射始终适用于所有键盘连接到系统。 不是当前无法在每个键盘的基础上创建映射。

## <a name="query-a-mouse-device"></a>查询鼠标设备


I8042prt 支持以下内置设备控制请求来查询有关鼠标设备信息：

[**IOCTL\_鼠标\_查询\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff542085(v=vs.85))

有关所有鼠标设备控制请求的详细信息，请参阅[I8042prt 鼠标内部设备控制请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

## <a name="registry-settings-associated-with-mouse-class-driver"></a>与鼠标类驱动程序相关联的注册表设置


下面是与鼠标类驱动程序相关联的注册表项的列表。

\[密钥：HKLM\\SYSTEM\\CurrentControlSet\\Services\\Mouclass\\Parameters\]

-   MaximumPortsServiced – 不使用 Windows XP 及更高版本。 仅为 Windows NT4。
-   PointerDeviceBaseName – 指定鼠标类设备驱动程序创建的设备对象的基名称
-   ConnectMultiplePorts – 确定是否存在一个或多个类设备的每个对象的一个端口设备对象。 主要由设备驱动程序使用此项。
-   MouseDataQueueSize-指定鼠标事件缓冲的鼠标驱动程序的数。 它还在计算时使用的鼠标驱动程序的内部缓冲区中的非分页的内存池的大小。

每个特定的注册表项的其他详细信息位于 https://technet.microsoft.com

## <a name="absolute-pointing-devices"></a>绝对指针设备


适用于设备的类型为 GUID\_类\_鼠标设备的功能驱动程序：

-   处理特定于设备的输入。

-   创建[**鼠标\_输入\_数据**](https://docs.microsoft.com/windows/desktop/api/ntddmou/ns-ntddmou-_mouse_input_data)结构所需的[ **MouseClassServiceCallback**](https://docs.microsoft.com/previous-versions/ff542394(v=vs.85))。

-   将传输鼠标\_输入\_数据结构与通过调用 Mouclass 数据队列**MouseClassServiceCallback**中其 ISR 调度完成例程。

对于绝对的指针设备，设备的功能驱动程序必须设置**LastX**，**最后**，并**标志**鼠标成员\_输入\_数据结构如下所示：

-   除了设备输入的值除以该设备的最大功能，该驱动程序通过 0xFFFF 来缩放设备输入的值：

    ```cpp
    LastX = ((device input x value) * 0xFFFF ) / (Maximum x capability of the device)
    LastY = ((device input y value) * 0xFFFF ) / (Maximum y capability of the device)
    ```

-   驱动程序设置鼠标\_移动\_中的绝对标志**标志**。

-   如果输入应为一个完整的虚拟桌面映射由窗口管理器中，驱动程序设置鼠标\_虚拟\_桌面中的标志**标志**。 如果鼠标\_虚拟\_桌面标志未设置，窗口管理器映射仅主监视器的输入。

以下示例指定，由类型的设备，如何实现这些要求特殊的绝对的指针设备：

-   HID 的设备：

    Mouhid，HID 鼠标设备的 Windows 功能驱动程序可自动实现这些特殊的要求。

-   PS/2-样式的设备：

    较高级别筛选器驱动程序是必需的。 筛选器驱动程序提供 IsrHook 回调和类服务回调。 I8042prt 调用 IsrHook 来处理原始设备输入，并调用筛选器类服务回调来筛选输入。 筛选器类服务回调，反过来，调用**MouseClassServiceCallback**。 IsrHook 回调和类服务回调的组合处理特定于设备的输入，创建所需的鼠标\_输入\_数据结构、 扩展设备输入的数据，以及设置鼠标\_移动\_绝对标志。

-   通过 Serenum 枚举插 COM 端口设备：

    插功能驱动程序是必需的。 功能驱动程序将创建所需的鼠标\_输入\_数据结构、 扩展设备输入的数据，以及设置鼠标\_移动\_绝对标志调用之前**MouseClassServiceCallback**.

-   非即插即用播放 COM 端口设备：

    特定于设备的功能驱动程序是必需的。 功能驱动程序将创建所需的鼠标\_输入\_数据结构、 扩展设备输入的数据，以及设置鼠标\_移动\_绝对标志调用之前**MouseClassServiceCallback**.

-   不受支持的总线上的设备：

    特定于设备的功能驱动程序是必需的。 功能驱动程序将创建所需的鼠标\_输入\_数据结构、 扩展设备输入的数据，以及设置鼠标\_移动\_绝对标志调用之前**MouseClassServiceCallback**.

 

 




