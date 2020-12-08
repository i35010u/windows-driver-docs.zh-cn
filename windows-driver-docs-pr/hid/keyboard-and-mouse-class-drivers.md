---
title: 键盘和鼠标类驱动程序
description: 非 HID 键盘和鼠标可通过多个旧式总线进行连接，但仍使用相同的类驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 811e08abf7e7e5f8899c99b97827c86c755969f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794992"
---
# <a name="keyboard-and-mouse-class-drivers"></a>键盘和鼠标类驱动程序

非 HID 键盘和鼠标可通过多个旧式总线进行连接，但仍使用相同的类驱动程序。 本部分包含有关类驱动程序本身的详细信息。 以下各节介绍有关控制器的详细信息。

本主题介绍 Microsoft Windows 2000 和更高版本中键盘和鼠标设备的典型物理配置。

下图显示了两种常用的配置，它们使用一个键盘和一个鼠标。

![阐释使用单个键盘和鼠标的两种配置的关系图](images/kemocfg1.png)

左侧的图形显示了通过独立控制器连接到系统总线的键盘和鼠标。 典型配置包括通过 i8042 控制器操作的 PS/2 样式键盘，以及通过串行端口控制器操作的串行样式鼠标。

以下附加信息对于键盘和鼠标制造商非常重要：

- 出于安全原因，操作系统堆栈按独占模式打开键盘
- Windows 支持同时连接多个键盘和鼠标设备。
- Windows 不支持将客户端独立访问到每个设备。

## <a name="class-driver-features"></a>类驱动程序功能

本主题介绍以下 Microsoft Windows 2000 和更高版本的系统类驱动程序的功能：

- **Kbdclass**，GUID \_ 类 \_ 键盘设备类的设备的类驱动程序

- **Mouclass**，GUID \_ 类 \_ 鼠标设备类的设备的类驱动程序

Kbdclass 实现了 Kbdclass 服务，并 kbdclass.sys 了其可执行映像。

Mouclass 实现了 Mouclass 服务，并 mouclass.sys 了其可执行映像。

每项功能 Kbdclass 和 Mouclass：

- 设备类的泛型和独立于硬件的操作。

-  (WMI) 即插即用、电源管理和 Windows Management Instrumentation。

- 旧设备的操作。

- 同时操作多台设备。

- [类服务回调例程](/windows-hardware/drivers/ddi/kbdmou/nc-kbdmou-pservice_callback_routine)的连接，函数驱动程序使用它将数据从设备的输入数据缓冲区传输到类驱动程序的数据缓冲区。

## <a name="configuration-of-device-objects"></a>设备对象的配置

下图显示了即插即用 PS/2 样式键盘和鼠标设备的设备对象的配置。 每个类驱动程序通过一个可选的上层设备筛选器来创建一个顶级类 *筛选器设备对象* (filter) ，该对象附加到函数设备对象 (*FDO*) 。 上层设备筛选器驱动程序用于创建上层设备筛选器。 I8042prt 创建函数，并将其附加到根总线驱动程序创建 (*PDO*) 的物理设备对象。

![说明即插即用 ps/2 样式键盘和鼠标设备的设备对象配置的关系图](images/km-ovr2.png)

### <a name="ps2-keyboard"></a>PS/2 键盘

键盘驱动程序堆栈包含以下各项。

- **Kbdclass**，上层键盘类筛选器驱动程序
- 一个或多个可选的高级键盘筛选器驱动程序
- **I8042prt**，函数驱动程序

### <a name="ps2-mouse"></a>PS/2 鼠标

鼠标驱动程序堆栈包含以下各项。

- **Mouclass**，上层的鼠标类筛选器驱动程序
- 一个或多个可选的上层鼠标筛选器驱动程序
- **I8042prt**，函数驱动程序

**Kbdclass** 和 **Mouclass** 可支持两种不同模式下的多个设备。 在 *一对一模式下*，每个设备都有一个独立的设备堆栈。 类驱动程序创建一个独立类并将其附加到每个设备堆栈。 每个设备堆栈都有自己的控制状态和输入缓冲区。 Microsoft Win32 子系统通过唯一的文件对象从每个设备访问输入。

在 *grandmaster 模式* 下，类驱动程序将按照以下方式操作所有设备：

- 类驱动程序创建一个表示所有设备的 *grandmaster 类* ，并为每个设备创建一个 *从属类* 。

    类驱动程序将从属类附加到每个设备堆栈。 在从属类的下面，设备堆栈与在一对一模式下创建的堆栈相同。

- Grandmaster 类控制所有从属 DOs 的操作。

- Win32 子系统通过表示 grandmaster 类设备的文件对象访问所有设备输入。

- 所有设备输入都在 grandmaster 的数据队列中进行缓冲。

- Grandmaster 维护一个全局设备状态。

如果将 Kbdclass 和 Mouclass 的注册表项值 **ConnectMultiplePorts** 设置为 (0x00，则和会在一对一模式下操作，**在 \\ \\ \\ 此**_&lt; &gt;_ 类服务 *_\\ 参数_* 下， *class service* 为 Kbdclass 或 Mouclass) 。 否则，Kbdclass 和 Mouclass 将在 grandmaster 模式下运行。

## <a name="open-and-close-via-the-class-driver"></a>通过类驱动程序打开和关闭

Microsoft Win32 子系统将打开所有键盘和鼠标设备，以供其独占使用。 对于每个设备类，Win32 子系统将从所有设备处理输入，就好像输入来自单个输入设备一样。 应用程序不能请求仅从一个特定设备接收输入。

Win32 子系统从即插即用管理器收到通知后，会动态打开即插即用输入设备，指出 \_ \_ 已启用 GUID 类键盘或 guid \_ 类 \_ 的鼠标设备接口。 Win32 子系统在收到已禁用打开的接口的通知后关闭即插即用设备。 Win32 子系统还会按名称打开旧设备 (例如，" \\ Device \\ KeyboardLegacyClass0" ) 。 请注意，一旦 Win32 子系统成功打开旧设备，它将无法确定该设备是否已被物理删除。

Kbdclass 和 Mouclass 接收到创建请求后，它们会执行以下操作来执行即插即用和旧操作：

- **即插即用操作**

    如果设备处于 "已启动即插即用" 状态，则类驱动程序会 \_ \_ 按驱动程序堆栈向下发送 IRP MJ CREATE 请求。 否则，类驱动程序完成请求，但不向下发送请求。 类驱动程序设置具有设备读取访问权限的受信任文件。 如果有 grandmaster 设备，则类驱动程序会将 "创建请求" 发送到与从属类设备关联的所有端口。

- **旧操作**

    类驱动程序将内部设备控制请求发送到端口驱动程序以启用设备。

## <a name="connect-a-service-callback-to-a-device"></a>将服务回叫连接到设备

类驱动程序必须将其类服务连接到设备，然后才能打开设备。 类驱动程序在将类服务附加到设备堆栈后连接其类服务。 函数驱动程序使用类服务回调将输入数据从设备传输到设备的类数据队列。 设备驱动程序的 ISR 调度完成例程将调用类服务回调。 Kbdclass 提供类服务回调 [**KeyboardClassServiceCallback**](/previous-versions/ff542324(v=vs.85))，Mouclass 提供类服务回调 [**MouseClassServiceCallback**](/previous-versions/ff542394(v=vs.85))。

供应商可以通过为设备安装上层筛选器驱动程序来修改类服务回调的操作。 示例键盘筛选器驱动程序 [Kbfiltr](/samples/microsoft/windows-driver-samples/keyboard-input-wdf-filter-driver-kbfiltr/) 定义 [**KbFilter \_ ServiceCallback**](/previous-versions/ff542297(v=vs.85)) 回调，并且示例鼠标筛选器驱动程序 [Moufiltr](/samples/microsoft/windows-driver-samples/mouse-input-wdf-filter-driver-moufiltr/) 定义 [**MouFilter \_ ServiceCallback**](/previous-versions/ff542380(v=vs.85)) 回调。 可以配置示例筛选器服务回调，以将从设备的端口输入缓冲区传输的输入数据修改为类数据队列。 例如，筛选器服务回调可以删除、转换或插入数据。

类和筛选器服务回调按以下方式连接：

- 类驱动程序按设备堆栈向下发送内部设备连接请求 ([**IOCTL \_ 内部 \_ 键盘 \_ 连接**](/windows-hardware/drivers/ddi/kbdmou/ni-kbdmou-ioctl_internal_keyboard_connect) 或 [**ioctl \_ 内部 \_ 鼠标 \_ 连接**](/windows-hardware/drivers/ddi/kbdmou/ni-kbdmou-ioctl_internal_mouse_connect)) 。 类连接数据由连接数据结构指定， \_ 该结构包含指向类设备对象的指针和指向类服务回调的指针。

- 筛选器驱动程序接收到连接请求后，它会保存类连接数据的副本，并将请求的连接数据替换为筛选器连接数据。 筛选器连接数据指定指向筛选器设备对象的指针和指向筛选器驱动程序服务回调的指针。 然后，筛选器驱动程序将筛选的连接请求发送到函数驱动程序。

类和筛选器服务回调的调用方式如下：

- 函数驱动程序使用筛选器连接数据将初始回调到筛选服务回调。

- 筛选输入数据后，筛选器服务回调使用其保存的类连接数据，以回调类服务回调。

## <a name="query-and-set-a-keyboard-device"></a>查询和设置键盘设备

I8042prt 支持下列内部设备控制请求，以查询有关键盘设备的信息以及设置键盘设备的参数：

[**IOCTL \_ 键盘 \_ 查询 \_ 特性**](/windows/win32/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_query_attributes)

[**IOCTL \_ 键盘 \_ 查询 \_ 指示器 \_ 转换**](/windows/win32/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_query_indicator_translation)

[**IOCTL \_ 键盘 \_ 查询 \_ 指示器**](/windows/win32/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_query_indicators)

[**IOCTL \_ 键盘 \_ 查询 \_ 按键**](/windows/win32/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_query_typematic)

[**IOCTL \_ 键盘 \_ 集 \_ 指示器**](/windows/win32/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_set_indicators)

[**IOCTL \_ 键盘 \_ SET \_ 按键**](/windows/win32/api/ntddkbd/ni-ntddkbd-ioctl_keyboard_set_typematic)

有关所有键盘设备控制请求的详细信息，请参阅 [人体学接口设备参考](/windows/win32/api/_hid/)。

## <a name="scan-code-mapper-for-keyboards"></a>扫描适用于键盘的代码映射器

在 Microsoft Windows 操作系统中，输入设备提供的 PS/2 兼容的扫描代码将转换为虚拟密钥，这些密钥将以 Windows 消息形式通过系统传播。 如果设备为某个密钥生成了错误的扫描代码，则会发送错误的虚拟密钥消息。 为此，可以编写一个筛选器驱动程序，用于分析固件生成的扫描代码，并将错误的扫描代码修改为系统可理解的代码。 但是，这是一个繁琐的过程，如果内核级筛选器驱动程序中存在错误，有时可能会导致严重的问题。

Windows 2000 和 Windows XP 包含一个新的扫描代码映射器，该映射器提供了一种允许映射扫描代码的方法。 Windows 的扫描代码映射存储在以下注册表项中：

``` syntax
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout
```

**注意**  还有一个 **键盘布局** 键 (注意控制键下) 的复数形式，但不应修改该键。

在 **键盘布局** 键中，必须添加 **Scancode 映射** 值。 此值的类型为 REG \_ BINARY (小 Endian 格式) ，并且具有下表中指定的数据格式。

| 起始偏移 (（字节）)  | 大小（以字节为单位） | 数据 |
|---|---|---|
| 0                       | 4               | 标头：版本信息  |
| 4                       | 4               | 标头：标志                |
| 8                       | 4               | 标头：映射的数目   |
| 12                      | 4               | 单个映射           |
| ...                     | ...             | ...                          |
| 最后4个字节            | 4               | 空终止符 (0x00000000)  |

第一个和第二个 DWORD 存储标头信息，并且对于扫描代码映射器的当前版本，它应设置为全零。 第三个 DWORD 项包含后面的映射的总数，包括 null 终止映射。 因此，最小计数为 1 (未) 指定任何映射。 每个映射都遵循标头。 每个映射的长度为一个 DWORD，并分为两个单词长度字段。 每个 WORD 字段存储要映射的密钥的扫描代码。

在注册表中存储映射后，必须重新启动系统才能使映射生效。 请注意，如果在按键上需要扫描代码的映射，则在将扫描代码转换为虚拟密钥之前，该步骤将在用户模式下执行。 在用户模式下执行此转换可能会出现某些限制，例如在终端服务下运行时映射不能正常工作。

若要删除这些映射，请删除 Scancode 映射注册表值并重新启动。

### <a name="example-1"></a>示例 1

下面显示了一个示例。 若要将左 CTRL 键替换为 Caps Lock 键，请使用注册表编辑器 (最好 Regedt32.exe) 修改 Scancode 映射键，使其包含以下值：

``` syntax
00000000 00000000 03000000 3A001D00 1D003A00 00000000
```

下表包含这些条目分为 DWORD 字段和交换的字节数。

**值**：解释

**0x00000000**：标头：版本。 设置为全零。

**0x00000000**：标头：标志。 设置为全零。

**0x00000003**：映射中的三个条目 (包括 null 条目) 。

**0x001D003A**：左 CTRL 键-- &gt; Caps Lock (0x1D-- &gt; 0x3A) 。

**0x003A001D**： Caps Lock-- &gt; 左键 (0x3A-- &gt; 0x1D) 。

**0x00000000**： Null 终止符。

### <a name="example-2"></a>示例 2

还可以添加键盘上未正式提供或删除从未使用的密钥的密钥。 以下示例显示了存储在 **Scancode 映射** 中的值，以删除右 CTRL 键并更改右 ALT 键的功能，使其用作静音键：

``` syntax
00000000 00000000 03000000 00001DE0 20E038E0 00000000
```

下表包含这些条目分为 DWORD 字段和交换的字节数。

**值**：解释

**0x00000000**：标头：版本。 设置为全零。

**0x00000000**：标头：标志。 设置为全零。

**0x00000003**：映射中的三个条目 (包括 null 条目) 。

**0xE01D0000**：删除右 CTRL 键 (0xE01D-- &gt; 0x00) 。

**0xE038E020**：右 ALT 键-- &gt; 静音键 (0xE038-- &gt; 0xE020) 。

**0x00000000**： Null 终止符。

生成所需的数据后，可以通过多种方式将其插入注册表中。

- 可以生成一个 .reg 文件，该文件可以使用注册表编辑器轻松地合并到系统注册表中。
- 还可以使用 \[ \] 包含要添加的注册表信息的 AddReg 部分来创建 .inf 文件。
- Regedt32.exe 可用于手动将信息添加到注册表。

扫描代码映射器具有几个优点和缺点。

优点包括：

- 映射器可用作纠正固件错误的简单修补程序。
- 通过在注册表中修改映射，可以将常用键添加到键盘。 不经常使用的密钥 (例如，右 CTRL 键) 可以映射到 null (为其他键删除) 或交换。
- 可以轻松地更改密钥位置。 用户可以轻松地自定义常用密钥的位置。

识别以下缺点：

- 在注册表中存储映射后，需要重新启动系统才能激活它。
- 注册表中存储的映射在系统级别工作，并适用于所有用户。 根据当前用户的不同，这些映射不能设置为不同的工作方式。
- 当前实现限制了地图的功能，以便映射始终适用于连接到系统的所有键盘。 目前不能基于每个键盘创建地图。

## <a name="query-a-mouse-device"></a>查询鼠标设备

I8042prt 支持使用以下内部设备控制请求来查询有关鼠标设备的信息：

[**IOCTL \_ 鼠标 \_ 查询 \_ 特性**](/previous-versions/windows/hardware/drivers/ff542085(v=vs.85))

有关所有鼠标设备控制请求的详细信息，请参阅 [人体学接口设备参考](/windows/win32/api/_hid/)。

## <a name="registry-settings-associated-with-mouse-class-driver"></a>与鼠标类驱动程序关联的注册表设置

下面是与鼠标类驱动程序相关联的注册表项的列表。

\[密钥： HKLM \\ SYSTEM \\ CurrentControlSet \\ Services \\ Mouclass \\ 参数\]

- **MaximumPortsServiced** –在 Windows XP 和更高版本上不使用。 仅适用于 Windows NT4。
- **PointerDeviceBaseName** –指定由鼠标类设备驱动程序创建的设备对象的基名称
- **ConnectMultiplePorts** –确定每个类设备对象是否有一个或多个端口设备对象。 此项主要由设备驱动程序使用。
- **MouseDataQueueSize** -指定鼠标驱动程序缓冲的鼠标事件数。 它还用于计算非分页内存池中鼠标驱动程序的内部缓冲区的大小。

## <a name="absolute-pointing-devices"></a>绝对指针设备

对于 [**GUID \_ 类 \_ 鼠标**](../install/guid-class-mouse.md)类型的设备，设备的函数驱动程序：

- 处理特定于设备的输入。

- 创建 [**MouseClassServiceCallback**](/previous-versions/ff542394(v=vs.85))所需的 [**鼠标 \_ 输入 \_ 数据**](/windows/win32/api/ntddmou/ns-ntddmou-mouse_input_data)结构。

- \_ \_ 通过在其 ISR 调度完成例程中调用 **MOUSECLASSSERVICECALLBACK** ，将鼠标输入数据结构传输到 Mouclass 数据队列。

对于绝对指针设备，设备的函数驱动程序必须 **LastX** **LastY** **Flags** \_ \_ 按以下方式设置鼠标输入数据结构的 LastX、最后和 Flags 成员：

- 除了按设备的最大容量划分设备输入值之外，驱动程序还可以通过0xFFFF 来缩放设备输入值：

    ```cpp
    LastX = ((device input x value) * 0xFFFF ) / (Maximum x capability of the device)
    LastY = ((device input y value) * 0xFFFF ) / (Maximum y capability of the device)
    ```

- 驱动程序 \_ \_ 在 **FLAGS** 中设置鼠标移动绝对标志。

- 如果应通过窗口管理器将输入映射到整个虚拟桌面，则驱动程序会 \_ \_ 在 **标志** 中设置鼠标虚拟桌面标志。 如果 \_ \_ 未设置鼠标虚拟桌面标志，则窗口管理器仅将输入映射到主监视器。

下面按设备类型指定如何实现对绝对定位设备的特殊要求：

- HID 设备：

    Mouhid 是 HID 鼠标设备的 Windows 函数驱动程序，自动实现这些特殊要求。

- PS/2 样式设备：

    需要高级筛选器驱动程序。 筛选器驱动程序提供 IsrHook 回调和类服务回调。 I8042prt 调用 IsrHook 来处理原始设备输入，并调用 filter 类服务回调来筛选输入。 然后，筛选器类服务回调调用 **MouseClassServiceCallback**。 IsrHook 回调和类服务回调的组合处理特定于设备的输入，创建所需的鼠标 \_ 输入 \_ 数据结构，缩放设备输入数据，并设置鼠标 \_ 移动 \_ 绝对标志。

- Serenum 枚举的即插即用 COM 端口设备：

    需要即插即用函数驱动程序。 函数驱动程序将创建所需的鼠标 \_ 输入 \_ 数据结构，缩放设备输入数据，并在 \_ \_ 调用 **MouseClassServiceCallback** 之前设置鼠标移动绝对标志。

- 非即插即用 COM 端口设备：

    需要设备特定的函数驱动程序。 函数驱动程序将创建所需的鼠标 \_ 输入 \_ 数据结构，缩放设备输入数据，并在 \_ \_ 调用 **MouseClassServiceCallback** 之前设置鼠标移动绝对标志。

- 不受支持的总线上的设备：

    需要设备特定的函数驱动程序。 函数驱动程序将创建所需的鼠标 \_ 输入 \_ 数据结构，缩放设备输入数据，并在 \_ \_ 调用 **MouseClassServiceCallback** 之前设置鼠标移动绝对标志。
