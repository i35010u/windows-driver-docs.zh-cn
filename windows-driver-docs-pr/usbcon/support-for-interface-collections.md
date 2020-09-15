---
description: '复合 USB 设备上的接口可以分组到集合中。 USB 泛型父驱动程序 ( # A0) 可以通过四种方式枚举接口集合。'
title: 枚举 USB 复合设备上的接口集合的概述
ms.date: 01/07/2019
ms.assetid: aa68a774-d5b2-4fd8-aee9-9b72b1e4ad4f
ms.localizationpriority: medium
ms.openlocfilehash: 5766f5b5c92309d29aacc7eabf6d15a71a0c01f1
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107458"
---
# <a name="overview-of-enumeration-of-interface-collections-on-usb-composite-devices"></a>枚举 USB 复合设备上的接口集合的概述


复合 USB 设备上的接口可以分组到集合中。 [USB 泛型父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md)可以通过四种方式枚举接口集合。

接口集合的这四个枚举方法按层次结构排列，如下所示：

1.  **供应商提供的回调例程**

    如果供应商已向 [ ( # A0) 的 USB 泛型父驱动程序 ](usb-common-class-generic-parent-driver.md)注册了一个回调例程，则泛型父驱动程序将优先于回调例程，并允许回调例程将接口分组，而不是使用其他方法。 有关使用供应商提供的回调例程枚举接口集合的详细信息，请参阅 [USB 复合设备上的接口集合枚举](support-for-interface-collections.md)。

2.  **联合功能说明符**

    . 如果供应商已在 USB 泛型父驱动程序中启用了 CDC 和 WMCDC 枚举，则泛型父驱动程序将使用 *联合功能描述符* (ufd) 将接口分组到集合中。 启用后，此方法优先于除供应商提供的回调例程之外的所有其他方法。 有关 Ufd 设备枚举的详细信息，请参阅 [对无线移动通信设备类的支持]()。

3.  **接口关联描述符**

    如果 *接口关联描述符* (IADs) 存在，则 USB 泛型父驱动程序始终使用 IADs （而不是使用旧方法）对接口进行分组。 Microsoft 建议供应商使用 IADs 来定义界面集合。 有关 IADs 设备枚举的详细信息，请参阅对 [无线移动通信设备类的支持]()。

4.  **旧音频方法。**

    USB 泛型父驱动程序可以通过使用为音频函数保留的旧技术来枚举接口集合。 如果设备上有任何 IADs，则泛型父驱动程序不会使用此方法。 有关旧音频枚举方法的详细信息，请参阅对 [无线移动通信设备类的支持]()。

##  <a name="customizing-enumeration-of-interface-collections-for-composite-devices"></a>自定义复合设备的接口集合的枚举


某些 USB 设备包含 USB 接口关联描述符 (IAD) 无法描述的接口集合。 在 Windows Vista 和更高版本的操作系统中，供应商可以自定义 [USB 一般父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md) 定义和枚举设备的接口集合的方式。 这是通过筛选器驱动程序中的 *枚举回调例程* 来完成的。 回调例程可帮助通用父驱动程序定义设备的自定义界面集合。

为了使通用父驱动程序定义自定义接口集合，复合设备的供应商必须：

1.   ([**USBC \_ 启动 \_ 设备 \_ 回调**](/windows-hardware/drivers/ddi/usbbusif/nc-usbbusif-usbc_start_device_callback)) 实现枚举回调例程。
2.  提供一个指针，该指针指向*USB 设备配置界面*中的回调例程 ([**USBC \_ 设备 \_ 配置 \_ 接口 \_ V1**](/windows-hardware/drivers/ddi/usbbusif/ns-usbbusif-_usbc_device_configuration_interface_v1)) 的**StartDeviceCallback**成员。
3.  提供一个 INF 文件，使其与复合设备的设备 ID 相匹配，并显式加载 USB 泛型父驱动程序和筛选器驱动程序。

### <a name="implementation-considerations"></a>实现注意事项


包含枚举回调例程的筛选器驱动程序可以是大写或较低的筛选器驱动程序。 当 USB 通用父驱动程序收到 [**IRP \_ MN \_ start \_ 设备**](../kernel/irp-mn-start-device.md) 请求以启动复合设备时，它会通过将 [**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md) 请求发送到驱动程序堆栈的顶部来查询 USB 设备配置接口。

收到 [**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md) 请求后，筛选器驱动程序必须检查请求的 **InterfaceType** 成员中的 GUID 类型，以验证所请求的接口的类型是否为 USB \_ 总线 \_ 接口 \_ USBC \_ 配置 \_ GUID。 如果是，筛选器驱动程序将返回指向 IRP 的 **接口** 成员中的接口的指针。

枚举回调例程必须返回一个指针，该指针指向一个 *函数描述符* 数组， ([**USBC \_ 函数 \_ 描述符**](/windows-hardware/drivers/ddi/usbbusif/ns-usbbusif-_usbc_function_descriptor)) 描述接口集合。 每个函数说明符都包含一个接口说明符数组， (用于描述接口集合的 [**USB \_ 接口 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)) 。 回调例程必须从非分页池分配函数描述符和接口描述符。 通用父驱动程序释放此内存。 回调例程必须确保每个**USB \_ 接口 \_ 描述符**的**NumberOfInterfaces**成员准确地报告接口集合中的接口数。

通用父驱动程序为每个函数描述符 (PDO) 创建物理设备对象。

在 [泛型父驱动程序例程](/windows-hardware/drivers/ddi/_usbref/#usbccgp)中汇总了 USB 设备配置界面和枚举回调例程。

### <a name="usb-generic-parent-driver-loading-mechanism"></a>USB 一般父驱动程序加载机制


当复合设备满足 [USB 复合设备枚举](enumeration-of-the-composite-parent-device.md)中所述的要求时，操作系统将生成一个兼容的 ID， `USB\COMPOSITE` 以指示设备是复合设备。 兼容 ID 在 Usb 中生成匹配项，操作系统会自动加载 USB 通用父驱动程序，而无需提供供应商提供的 INF 文件的帮助。

但是，此默认机制对于需要接口集合的自定义枚举的复合设备不起作用，因为在默认机制中，系统不会加载所需的供应商提供的筛选器驱动程序。 若要使枚举回调例程机制正常工作，当 USB 泛型父代枚举复合设备的接口集合时，必须已加载公开 USB 设备配置界面的筛选器驱动程序。 这要求复合设备的供应商安装一个 INF 文件，该文件与复合设备的设备 ID 相匹配，并显式加载 USB 泛型父驱动程序和筛选器驱动程序。


## <a name="support-for-the-wireless-mobile-communication-device-class"></a>对无线移动通信设备类的支持


在 Windows Vista 中， [Usb 通用父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md) 为通用串行总线 (USB) 通信设备类 (CDC) 和 Usb 无线移动通信设备类 (WMCDC) 中包含的设备提供支持。

USB 无线移动通信设备类 (WMCDC) 规范为主机与无线移动设备之间的连接、控制和内容交换建立了标准 (例如，当设备连接到 USB 端口时，手机) 。 WMCDC 是 (CDC) 的通信设备类的扩展，其中包括各种通信和网络设备。 本部分介绍支持 Windows 操作系统中的 CDC 和 WMCDC 设备的体系结构。

WMCDC 设备包含多个按 *逻辑话机*分组的函数。 大多数 WMCDC 设备都有一个逻辑耳机，但一个设备可能有多个逻辑话机。 逻辑话机通常包括诸如数据/传真调制解调器、对象存储和呼叫控制设施等功能。 逻辑耳机还可能包括由其他 USB 规范定义的支持函数，例如 USB 音频类规范、USB 人体输入设备 (HID) 类规范和 USB 视频类规范。

Windows WMCDC 体系结构使用本机 Windows 驱动程序来管理 WMCDC 设备的功能。 例如，你可以使用 Windows 电话应用程序界面 (TAPI) 子系统来管理设备的语音和数据/传真调制解调器功能，并使用 Windows 网络驱动程序接口规范 (NDIS) 子系统来管理设备的以太网 LAN 函数。 此外，你还可以在用户模式软件中管理一些函数（例如对象交换协议 (OBEX) 函数），并在 [WinUSB](winusb.md) ( # A0) 中获得帮助。

此图显示了 WMCDC 设备的示例驱动程序堆栈。

![示例设备配置和驱动程序堆栈](images/wmcdc-architecture.png)

在上图中，WMCDC 设备包含一个逻辑耳机： OBEX 函数和调制解调器函数。 供应商提供的 INF 文件加载本机 Windows 驱动程序来管理调制解调器。 OBEX 函数由供应商提供的用户模式驱动程序管理，该驱动程序在 [用户模式驱动程序框架](../wdf/user-mode-driver-framework-design-guide.md) (UMDF) 中运行。 用户模式驱动程序使用 (WPD) 协议的 Windows 便携式设备与用户应用程序以及 [WinUSB](winusb.md) 导出以与 USB 堆栈通信的接口进行通信。 通常情况下，供应商提供的 INF 文件会为使用 Winusb.sys 的每个接口集合加载单独 Winusb.sys 的实例。

### <a name="registry-settings"></a>注册表设置

USB stack 不会自动支持 WMCDC。 您必须提供一个 INF 文件，用于加载 Usbccgp.sys 的实例。 INF 文件必须包含 **AddReg** 部分，该部分将与 Usbccgp.sys 关联的软件密钥中的 **EnumeratorClass** 注册表值设置为 \_ 从三个数字构造的注册表项二进制值：0x02、0x00 和 0x 00。 下面的示例 INF 文件中的代码示例演示如何将 **EnumeratorClass** 设置为合适的值。

```INF
[CCGPDriverInstall.NT]
Include=usb.inf
Needs=Composite.Dev.NT
AddReg=CCGPDriverInstall.AddReg

[CCGPDriverInstall.NT.Services]
Include=usb.inf
Needs=Composite.Dev.NT.Services

[CCGPDriverInstall.AddReg]
HKR,,EnumeratorClass, 0x00000001,02,00,00
```

必须分配给 **EnumeratorClass** 的值是从在 INF 文件中通过十六进制数字成对表示的三个1字节的二进制值构造的。 这三个数字对应于 USB 实现者论坛分配给 CDC 设备类的值，分别为 cdc 设备子类和 CDC 设备协议。

有关如何配置注册表以正确枚举 WMCDC 设备的详细信息，请参阅 [对无线移动通信设备类的支持]()。

以下主题进一步介绍了 WMCDC：

### <a name="enumerating-interface-collections-on-wmcdc"></a>枚举 WMCDC 上的接口集合


USB 无线移动通信设备类 (WMCDC) 是 (CDC) 的 USB 通信设备类的子类。 WMCDC 规范可扩展，但不会对定义接口集合的 CDC 准则进行重大更改。 特别是，WMCDC 设备必须遵守定义接口集合的 CDC 准则。

CDC 接口集合包含一个 ([**USB \_ 接口 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)) 的主接口，该接口属于通信接口类 (`bInterfaceClass = 0x02`) 或数据接口类 (`bInterfaceClass = 0x0A`) 。 如果主接口属于通信接口类 (这是) 的典型情况，则主接口 (**bInterfaceSubClass**) 的子类指定 CDC *控制模型*。 控件模型指示接口集合中包含的接口类型。 有关 USB 实现者论坛定义的控制模型的说明，请参阅 CDC 规范和 WMCDC 规范。

接口集合的主接口后跟一组必需的特定于类的函数描述符，其中包括联合功能描述符 (UFD) 。 UFD 会列出属于该集合的接口数。 UFD 的 **bMasterInterface** 字段包含主接口的编号。 零个或多个 **bSubordinateInterface** 字段包含集合中其他 (从属) 接口的编号。

对于大多数类型的控件模型， [USB 泛型父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md) 为每个 UFD (PDO) 创建一个物理设备对象。 但有些控制模型包含一个音频接口，该接口是泛型父驱动程序与音频接口所属的接口集合分开枚举的。 音频接口显示在接口集合的 " **bSubordinateInterface**) 的从属接口列表中 ("，但通用父驱动程序为音频接口创建单独的 PDO。 音频接口的 PDO 和音频接口所属接口集合的 PDO 直接位于功能设备对象的正上方 (设备对象树中父复合设备的 FDO) 。 音频接口的 PDO 不是接口集合的子接口。 [无线移动通信设备类的支持]()中介绍了音频接口的枚举。

在注册表中，有两种可配置枚举特性的控件模型：无线话筒控制模型 (WHCM) ，用于定义逻辑耳机， (OBEX) 控制模型。 若要配置这两个控件模型的枚举特征，您必须提供一个 INF 文件，该文件加载 Usbccgp.sys 的实例，并在该实例的 Usbccgp.sys 的软件密钥中设置 **CdcFlags** 的值。 下表描述了 **CdcFlags**的配置选项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>CdcFlags 位</th>
<th>位设置为0</th>
<th>位设置为1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0 (掩码 = 0x00000001) </p></td>
<td><p>USB 通用父驱动程序为每个 OBEX 接口创建一个单独的 PDO。</p></td>
<td><p>USB 通用父驱动程序为所有 OBEX 接口创建单个 PDO。</p></td>
</tr>
<tr class="even">
<td><p>1 (掩码 = 0x00000010) </p></td>
<td><p>USB 通用父驱动程序不会 (逻辑话机) 创建 WHCM 接口的 PDOs。 从设备对象树的角度来看，这些接口保持隐藏状态。</p></td>
<td><p>USB 通用父驱动程序为每个 WHCM 接口创建一个 PDO。</p></td>
</tr>
</tbody>
</table>

 

例如，若要清除两个位 (将其设置为 0) ，则 INF 文件应在 **DDInstall. AddReg** 部分中包含以下行。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000000
```

若要将这两个位设置为1，INF 文件应具有以下行。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000011
```

若要将 "位 0" 设置为 "1"，将 "位 1" 设置为0，则 INF 文件应包含以下行。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000001
```

可以设置或重置其中的任何一个，而与另一位无关。

下图说明了不同的注册表配置如何为同一设备创建不同的设备树。

下图说明了 **CdcFlags** 的位0和第1位均为0时的 PDO 配置。

![说明 cdcflags = 0x00000000 的设备对象映射的接口集合的关系图](images/cdcflags.png)

上图中 (WHCM) 接口集合的无线话筒控制模型包含三个从属接口集合 (**bSubordinateInterface**) ：两个 OBEX 集合和一个调制解调器集合。 **CdcFlags**的位0为0，因此 USB 通用父驱动程序不会为 WHCM 接口集合创建 PDO。 **CdcFlags**的第1位为0，因此 USB 通用父驱动程序为每个 OBEX 接口集合生成单独的 PDO。

下图说明了设置 **CdcFlags** 的位0和第1位时的 PDO 配置。

![说明 cdcflags = 0x00010001 的设备对象映射的接口集合的关系图](images/cdcflags-wpd.png)

由于 **CdcFlags** 的位0设置为1，因此 USB 通用父驱动程序将为 WHCM 接口集合创建 PDO。 由于 **CdcFlags** 的第1位设置为1，因此 USB 通用父驱动程序会将两个 OBEX 集合组合在一起，并为两个 OBEX 集合生成一个 PDO。

你可能想要在内核级别使用单个 PDO 表示 OBEX 集合，并在用户模式驱动程序中区分每个单独的 OBEX 集合。 当所有 OBEX 函数在内核级别上分组到单个 PDO 中时，Windows 可移植设备 (WPD) 协议可帮助你在用户级别上多路复用不同 OBEX 函数之间的数据流。

以下示例 INF 文件加载了 USB 通用父驱动程序来管理 WMCDC 设备，并指示 USB 通用父驱动程序为逻辑话机创建 PDOs，并为逻辑耳机中的所有 OBEX 集合创建单个 PDO。

```INF
[Version]
signature="$Windows NT$"
Class=USB
ClassGUID={36FC9E60-C465-11CF-8056-444553540000}
Provider=%MSFT%
DriverVer=07/01/2001,5.1.2600.0

[ControlFlags]
ExcludeFromSelect=*

[Manufacturer]
CompanyName=CompanyName

[CompanyName]
%COMPANYNAME.DeviceDesc%=CCGPDriverInstall,USB\Vid_????&Pid_????

[CCGPDriverInstall.NT]
Include=usb.inf
Needs=Composite.Dev.NT
AddReg=CCGPDriverInstall.AddReg

[CCGPDriverInstall.NT.Services]
Include=usb.inf
Needs=Composite.Dev.NT.Services

[CCGPDriverInstall.AddReg]
HKR,,EnumeratorClass,0x00000001,02,00,00
HKR,,CdcFlags,0x00010001,0x00010001

[Strings]
MSFT="Microsoft"
COMPANYNAME.DeviceDesc="USB Phone Parent"
```
### <a name="handling-cdc-and-wmcdc-interface-collections"></a>处理 CDC 和 WMCDC 接口集合


USB 通用父驱动程序以特殊方式处理无线话筒控制模型 (WHCM) 接口，如 [对无线移动通信设备类的支持]()中所述。

下面的列表汇总了 CDC 和 WMCDC 接口集合处理与其他接口集合的处理方式的最重要方式：

-   无线移动通信设备类允许有限数量的接口集合嵌套。 具体而言，逻辑耳机接口集合 (即，) 可以包含其他从属接口集合的 WHCM 接口集合。 例如，WMCDC 兼容电话可以有一个 WHCM 接口集合，后者又包含一个抽象控件模型集合和一个 OBEX 集合。
-   可以将 USB 泛型父驱动程序配置为不枚举 WHCM 接口集合。 未枚举的 WHCM 接口集合保持隐藏状态，但泛型父驱动程序使用联合函数描述符 (Ufd) 中的信息，这些信息属于 WHCM 接口集合，用于分组和枚举从属接口集合。
-   你可以配置 USB 通用父驱动程序，以便为 OBEX 控件模型接口集合 (PDOs) 创建单独的物理设备对象，或为所有 OBEX 控件模型接口集合创建单个 PDO。
-   UFD 中的接口编号列表可以有空白。 也就是说，UFD 的接口号可以引用不连续的接口。 这种类型的编号无效，例如，对于 [USB 接口关联描述符 (IAD) ](usb-interface-association-descriptor.md)，其接口必须是连续的并且具有顺序号。
-   Ufd 可以包括相关音频接口集合
-   CDC 和 WMCDC 接口集合)  (Id 的硬件标识符必须包含 interface 子类。 其他 USB 接口（其硬件 Id 包含 \_ 用于指定接口号的 MI% 02x 后缀）不包含接口子类的相关信息。 在硬件 ID 中包含子类信息，以允许供应商为特定接口集合提供具有硬件 ID 匹配项的 INF 文件，而不是依赖于描述符布局中接口的位置来确定要为集合加载哪个驱动程序。 硬件 ID 中的子类信息还允许来自当前供应商提供的驱动程序的逐步迁移路径，该驱动程序将 WMCDC interface 集合管理为替代方法，例如用户模式驱动程序。 有关 CDC 和 WMCDC 硬件 Id 的示例，请参阅对 [无线移动通信设备类的支持]()。 有关如何格式化 USB 接口硬件 Id 的一般讨论，请参阅 [Usb 设备的标识符](../install/identifiers-for-usb-devices.md)。

### <a name="cdc-and-wmcdc-control-models"></a>CDC 和 WMCDC 控件模型


CDC 和 WMCDC 控件模型部分介绍了 Microsoft Windows 操作系统中支持的接口集合的属性。 每个说明包括硬件和设备标识符的列表， (Id) USB 通用父驱动程序为接口集合生成的 Id。

Windows 支持的大多数接口集合对应于属于通信设备类 (CDC) 和无线移动通信设备类 (WMCDC) 的控制模型，但操作系统还支持旧的音频和视频接口集合，以及移动计算升级联盟 (MCPC) 定义的接口集合。

本部分中描述的接口集合如下所示：

#### <a name="audio-class-interfaces"></a>音频类接口


在 CDC 和 WMCDC 设备上发生的 USB 音频设备类接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>音频设备的通用串行总线设备类定义</em>，版本1.0。</p></td>
</tr>
<tr class="even">
<td><p>类</p></td>
<td><p>接口集合中的所有接口都必须属于音频设备类 (0x01) 。</p></td>
</tr>
<tr class="odd">
<td><p>子类</p></td>
<td><p>接口集合中的每个接口必须与集合中的第一个接口具有不同的子类。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) 。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>属于流式处理子类 (0x02) 的零个或多个连续接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&MI_%02x
USB\Vid_%04x&Pid_%04x&MI_%02x</code></pre>
<p>音频接口集合的硬件 Id 不包含接口类特定的信息。 有关与音频接口集合关联的硬件 Id 的格式的说明，请参阅对 <a href="/windows-hardware/drivers/usbcon/support-for-interface-collections" data-raw-source="[Support for the Wireless Mobile Communication Device Class]()">无线移动通信设备类的支持</a>。</p></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_01&SubClass_01&Prot_00
USB\Class_01&SubClass_01
USB\Class_01</code></pre>
<p>音频接口集合的兼容 Id 的格式包含有关接口类、接口子类和协议的嵌入信息。 对于 CDC 或 WMCDC 设备上的音频接口集合，接口类为01，子类为01，协议为00。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-abstract-control-model"></a>CDC 抽象控件模型


 (的) ，抽象控件模型有两个版本。 原始版本是在 (CDC) 规范的 *USB 通信设备类* 中定义的。 *USB 无线移动通信设备类* (WMCDC) 规范包含对所进行的扩展定义。

[支持无线移动通信设备类]()中描述了符合 WMCDC 规范的接口集合。

符合 CDC 规范的接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>用于通信设备的通用串行总线类定义</em>，版本1.1，节3.6.2。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>)  (0x02。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>随时.</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的一个数据类接口和可选的音频类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_02&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_02
USB\Vid_%04x&Pid_%04x&Cdc_02&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_02</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_02&Prot_%02X
USB\Class_02&SubClass_02
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>UFD 可以引用独立于工作类型接口集合枚举的音频接口集合。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-atm-networking-control-model"></a>CDC ATM 网络控制模型


USB CDC ATM 网络控制模型 (ANCM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>用于通信设备的通用串行总线类定义</em>，版本1.1，节3.8。3</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) </p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>ANCM (0x07) </p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) </p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能说明符引用的一个数据类接口 (UFD) </p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_07&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_07
USB\Vid_%04x&Pid_%04x&Cdc_07&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_07</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_07&Prot_00
USB\Class_02&SubClass_07
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>


#### <a name="cdc-capi-control-model"></a>CDC CAPI 控制模型


 (CAPI) 控制模型接口集合的 USB CDC 常见 ISDN API 具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em></em></p>
<p><em>用于通信设备的通用串行总线类定义</em>，版本1.1，节3.7。2</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) </p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>CAPI (0x05) </p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) </p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能说明符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_05&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_05</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_05&Prot_00
USB\Class_02&SubClass_05</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-direct-line-control-model"></a>CDC 直接连线控件模型


USB CDC 直接线路控制模型 (DLCM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>用于通信设备的通用串行总线类定义</em>，版本1.1，第3.6.1 节。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>DLCM (0x01) 。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) 。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的音频类或供应商定义的接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_01&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_01
USB\Vid_%04x&Pid_%04x&Cdc_01&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_01</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_01&Prot_00
USB\Class_02&SubClass_01
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>UFD 引用音频类接口集合，该集合独立于 DLCM 接口集合进行枚举。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-ethernet-networking-control-model"></a>CDC 以太网网络控制模型


USB CDC 以太网网络控制模型 (ENCM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>用于通信设备的通用串行总线类定义</em>，版本1.1，节3.8.2。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>ENCM (0x06) 。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) 。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能说明符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_06&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_06
USB\Vid_%04x&Pid_%04x&Cdc_06&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_06</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_06&Prot_00
USB\Class_02&SubClass_06
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>此控件模型的兼容 Id 在 Microsoft 提供的 INF 文件中匹配。 如果操作系统在供应商提供的 INF 文件中找不到其中一个硬件 Id 的匹配项，系统会自动加载本机 NDIS 微型端口驱动程序以管理接口集合。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-multi-channel-isdn-control-model"></a>CDC 多通道 ISDN 控制模型


USB CDC 多通道 ISDN 控制模型 (MCCM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>用于通信设备的通用串行总线类定义</em>，版本1.1，节3.7。1</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) </p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>MCCM (0x04) </p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) </p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能说明符 (UFD) 引用的多个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_04&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_04
USB\Vid_%04x&Pid_%04x&Cdc_04&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_04</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_04&Prot_00
USB\Class_02&SubClass_04
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 
#### <a name="cdc-telephone-control-model"></a>CDC 电话控制模型


 (TCM) 接口集合的 USB CDC 电话控制模型具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>用于通信设备的通用串行总线类定义</em>，版本1.1，节3.6.3。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>TCM (0x03) 。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>随时.</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>Union 功能说明符 (UFD) 引用的音频类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 ID</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_03&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_03
USB\Vid_%04x&Pid_%04x&Cdc_03&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_03</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 ID</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_03&Prot_%02X
USB\Class_02&SubClass_03
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>UFD 可以引用音频类接口集合，该集合独立于 TCM 接口集合进行枚举。</p></td>
</tr>
</tbody>
</table>

#### <a name="mcpc-vendor-unique-interfaces"></a>MCPC 供应商唯一接口


移动计算促销联盟 (MCPC) 在无线移动通信设备类 (WMCDC) 规范为供应商唯一的 CDC 设备提供格式之前，定义了接口集合的格式。 因此，MCPC 接口集合不符合 WMCDC 标准。

但是，如果启用了 WMCDC，则 USB 泛型父驱动程序可以枚举 MCPC 接口集合。 MCPC 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p>移动计算促销协会 (MCPC) GL-004 规范</p></td>
</tr>
<tr class="even">
<td><p>类</p></td>
<td><p>CDC (0x02) </p></td>
</tr>
<tr class="odd">
<td><p>子类</p></td>
<td><p>0x88</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) </p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能说明符 (UFD) 引用的零个或多个数据类接口</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_88&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_88
USB\Vid_%04x&Pid_%04x&Cdc_88&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_88</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_88&Prot_00
USB\Class_02&SubClass_88
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

#### <a name="video-class-interfaces"></a>视频类接口


在 CDC 和 WMCDC 设备上发生的 USB 视频设备类接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>视频设备的通用串行总线设备类定义</em>，版本1.0。</p></td>
</tr>
<tr class="even">
<td><p>类</p></td>
<td><p>视频 (0x0E) 。</p></td>
</tr>
<tr class="odd">
<td><p>子类</p></td>
<td><p>视频控制 (0x01) 。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) 。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>属于流式处理子类 (0x02) 的零个或多个连续接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&MI_%02x
USB\Vid_%04x&Pid_%04x&MI_%02x</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_0E&SubClass_01&Prot_00
USB\Class_0E&SubClass_01
USB\Class_0E</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>视频类接口集合接收 CDC 设备上的特殊处理。 在非 CDC 设备上，视频类接口集合由接口关联描述符 (IADs) 定义。 在 CDC 设备上，视频类接口集合由联合功能说明符定义 (Ufd) 。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-abstract-control-model"></a>WMCDC 抽象控件模型


 (的) ，抽象控件模型有两个版本。 原始版本是在 (CDC) 规范的 USB 通信设备类中定义的。 USB 无线移动通信设备类 (WMCDC) 规范包含对所进行的扩展定义。 包含传真/调制解调器功能的工作集集合应使用 WMCDC 的定义，而不是使用原始的 CDC 运行定义。

[支持无线移动通信设备类]()中描述了符合 CDC 规范的接口集合。

符合 WMCDC 规范的接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>适用于无线移动通信设备的通用串行总线 CDC 子类规范</em>，版本1.0，第6.2 节。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>)  (0x02。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>如果集合使用 AT 命令集协议，则在兼容 Id 中嵌入的协议值为0x01。 如果集合使用 WMCDC 规范描述的一种协议，则在兼容 Id 中嵌入的协议值将是0x2 到0x06 或0xFE。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能说明符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_Modem&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_Modem
USB\Vid_%04x&Pid_%04x&Cdc_Modem&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_Modem</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_Modem&Prot_%02X
USB\Class_02&SubClass_Modem
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>UFD 可能会引用一个音频接口集合，该集合是独立于工作类型接口集合枚举的。</p>
<p>接口集合必须符合 WMCDC 规范的6.2 节中指定的特殊描述符和终结点要求。 如果接口集合不符合 WMCDC 要求，但接口符合 CDC 要求，则 USB 通用父驱动程序将用 CDC 格式枚举接口集合和通用硬件 Id，如对 <a href="/windows-hardware/drivers/usbcon/support-for-interface-collections" data-raw-source="[Support for the Wireless Mobile Communication Device Class]()">无线移动通信设备类的支持</a>中所述。</p>
<p>此控件模型的兼容 Id 在 Microsoft 提供的 INF 文件中匹配。 如果操作系统在供应商提供的 INF 文件中找不到某个硬件 Id 的匹配项，则系统会自动加载本地电话应用程序编程接口 (TAPI) 调制解调器筛选器驱动程序来管理调制解调器功能并设置相应的 TAPI 注册表设置，除非协议代码为0xFE。 如果协议代码为0xFE，则供应商必须提供设备或类共同安装程序，才能正确地填充 TAPI 注册表设置。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-device-management-model"></a>WMCDC 设备管理模型


USB WMCDC 设备管理模型 (CALL CENTER.DMM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>适用于无线移动通信设备的通用串行总线 CDC 子类规范</em>，版本1.0，第6.6 节。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>CALL CENTER.DMM (0x09) 。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>随时.</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_09&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_09
USB\Vid_%04x&Pid_%04x&Cdc_09&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_09</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_09&Prot_%02X
USB\Class_02&SubClass_09
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>此控件模型不使用联合功能描述符 (UFD) 。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-mobile-direct-line-model"></a>WMCDC Mobile 直接连线模型


USB WMCDC Mobile 直接线路型号 (MDLM) 接口集合具有以下属性：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>适用于无线移动通信设备的通用串行总线 CDC 子类规范</em>，版本1.0，第6.7 节</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) </p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>MDLM (0x0A) </p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>任意</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的一个或多个数据类接口</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_0A&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_0A
USB\Vid_%04x&Pid_%04x&Cdc_0A&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_0A</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_0A&Prot_%02X
USB\Class_02&SubClass_0A
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-obex-control-model-multiple-pdos"></a>WMCDC OBEX 控件模型 (多个 PDOs) 


可以通过两种方法来枚举对象交换协议 (OBEX) 控制模型接口集合： USB 泛型父驱动程序可以将所有 OBEX 接口组合在一起，并为所有 OBEX 接口创建一个物理设备对象 (PDO) ，或者父驱动程序可以为每个 OBEX 接口创建一个单独的 PDO。 有关 USB 通用父驱动程序为组合在一起的 OBEX 接口生成的硬件 Id 的说明，请参阅对 [无线移动通信设备类的支持]()。

当 USB 通用父驱动程序为每个 OBEX 接口分配单独的 PDOs 时，PDOs 具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>适用于无线移动通信设备的通用串行总线 CDC 子类规范</em>，版本1.0，第6.5 节。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>OBEX (0x0B) 。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) 。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能说明符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_0B&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_0B
USB\Vid_%04x&Pid_%04x&Cdc_0B&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_0B</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_0B&Prot_00
USB\Class_02&SubClass_0B
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>与管理复合设备的 USB 通用父驱动程序实例关联的注册表设置确定是使用单个 PDO 还是多个 PDOs 来管理 OBEX 接口。 有关指定 USB 通用父驱动程序如何枚举 OBEX 接口的注册表设置说明，请参阅对 <a href="/windows-hardware/drivers/usbcon/support-for-interface-collections" data-raw-source="[Support for the Wireless Mobile Communication Device Class]()">无线移动通信设备类的支持</a>。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-obex-control-model-single-pdo"></a>WMCDC OBEX 控制模型 (单个 PDO) 


可以通过两种方法来枚举对象交换协议 (OBEX) 控制模型接口集合： USB 泛型父驱动程序可以将所有 OBEX 接口组合在一起，并为所有 OBEX 接口创建一个物理设备对象 (PDO) ，或者父驱动程序可以为每个 OBEX 接口创建一个单独的 PDO。 有关 USB 通用父驱动程序为单独枚举的 OBEX 接口生成的硬件 Id 的说明，请参阅对 [无线移动通信设备类的支持]()。

当 USB 通用父驱动程序将单个 PDO 分配给所有 OBEX 接口时，PDO 具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>适用于无线移动通信设备的通用串行总线 CDC 子类规范</em>，版本1.0，第6.5 节。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>OBEX (0x0B) 。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) 。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>联合功能说明符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&WPD_OBEX&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&WPD_OBEX
USB\Vid_%04x&Pid_%04x&WPD_OBEX&MI_%02x
USB\Vid_%04x&Pid_%04x&WPD_OBEX</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&WPD_OBEX
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>与管理复合设备的 USB 通用父驱动程序实例关联的注册表设置确定是使用单个 PDO 还是多个 PDOs 来管理 OBEX 接口。 有关指定 USB 通用父驱动程序如何枚举 OBEX 接口的注册表设置说明，请参阅 <a href="support-for-interface-collections.md" data-raw-source="[Enumeration of Interface Collections on USB Composite Devices](support-for-interface-collections.md)">Usb 复合设备上的接口集合枚举</a>。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-wireless-handset-control-model"></a>WMCDC 无线话筒控制模型


USB 泛型父驱动程序并不总是枚举无线耳机控制模型 (WHCM) 接口集合。 与管理 WHCM 接口集合的 USB 泛型父驱动程序的实例关联的注册表设置确定 USB 泛型父驱动程序是否为接口集合 (PDO) 创建物理设备对象。 有关指定 USB 通用父驱动程序如何枚举 WHCM 接口的注册表设置说明，请参阅 [Usb 复合设备上的接口集合枚举](support-for-interface-collections.md)。

枚举的 WHCM 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>适用于无线移动通信设备的通用串行总线 CDC 子类规范</em>，版本1.0，第6.1 节。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02) 。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>WHCM (0x08) 。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00) 。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>可以。</p></td>
</tr>
<tr class="even">
<td><p>相关接口</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_08&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_08
USB\Vid_%04x&Pid_%04x&Cdc_08&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_08</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_08&Prot_00
USB\Class_02&SubClass_08
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>联合功能描述符 (UFD) 标识与逻辑耳机关联的接口。</p></td>
</tr>
</tbody>
</table>

上述主题中的硬件 ID 格式介绍了如何使用以下约定：

- C 语言 **printf** 格式表示整数。 例如，"% 04x" 表示四位十六进制整数，"% 02x" 表示2位十六进制整数，依此类推。

- 字符串 "Vid" 后面的整数 \_ 是由 USB 委员会 (www.usb.org) 分配给供应商的供应商代码的四位十六进制表示形式。

- 字符串 "Pid" 后面的整数 \_ 是供应商分配给设备的产品代码的四位十六进制表示形式。

- 字符串 "Rev" 后面的整数 \_ 是设备修订号的四位十六进制表示形式。

- 字符串 "Cdc" 后面的整数 \_ 是接口子类。

- 字符串 "Prot" 后面的整数 \_ 是协议号。

- 字符串 "MI" 后面的整数 \_ 是接口号的2位十六进制表示形式，它是从接口描述符的 **bInterfaceNumber** 字段中提取的。


### <a name="enumeration-of-interface-collections-on-usb-devices-with-iads"></a>在带有 IADs 的 USB 设备上枚举接口集合


如果 USB 复合设备在其固件中有一个 (IAD) 的接口关联描述符，Windows 会枚举接口集合，就好像每个集合都是单个设备，并将一个物理设备对象 (PDO) 分配给每个接口集合，并将硬件与兼容标识符 (Id) 与 PDO 关联。 有关 IADs 的详细说明，请参阅 [USB 接口关联描述符](usb-interface-association-descriptor.md)。 本部分介绍 (Id 的硬件 Id 和兼容标识符) 分配给与 IAD 关联的接口集合。

##  <a name="hardware-ids"></a>硬件 Id


`USB\VID_v(4)&PID_p(4)&Rev_r(4)&MI_z(2)`

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

在这些硬件 Id 中，

-   * (4) * 是 USB 委员会分配给供应商并从设备描述符的 **idVendor** 字段中提取的四位供应商代码。
-   *p (4) * 是供应商分配给设备并从设备描述符的 **idProduct** 字段中提取的四位数产品代码。
-   *r (4) * 是由供应商分配给设备并从设备描述符的 **bcdDevice** 字段中提取的四位设备版本号，采用二进制编码的十进制版本。
-   *z (2) * 是从 IAD 的 **bFirstInterface** 字段中提取的两位数接口号。

#### <a name="compatible-ids"></a>兼容 Id


`USB\Class_c(2)&SubClass_s(2)&Prot_p(2)`

`USB\Class_c(2)&SubClass_s(2)`

`USB\Class_c(2)`

在这些兼容的 Id 中，c (2) ，s (2) ，p (2) 包含 **bFunctionClass**、 **bFunctionSubClass**和 **bFunctionProtocol** 字段中分别采用的值。

不能以递归方式使用 IADs 来绑定函数的函数。 特别是，如果设备在其固件中具有 IAD 的描述符，则一般父驱动程序将不会按音频设备类对接口分组，如 [USB 复合设备上的接口集合枚举](support-for-interface-collections.md)中所述。

### <a name="enumeration-of-interface-collections-on-audio-devices-without-iads"></a>在音频设备上枚举接口集合而不 IADs


对于音频设备，Windows 操作系统可以枚举与函数关联) 的接口组 (接口集合，并为每个组分配一个物理设备对象 (PDO) ，即使在设备没有 (IAD) 的接口关联描述符时也是如此。

如果接口满足以下条件，操作系统会将复合音频设备的接口分组为接口集合：

-   接口集合中的所有接口都必须是连续的。 换句话说，接口必须在固件内存中彼此相邻。
-   接口集合中的所有接口都必须属于音频设备类。 设备制造商指定接口属于音频设备类，方法是将值0x01 分配给接口描述符的 **bInterfaceClass** 字段。
-   接口集合中的每个接口必须与集合中的第一个接口具有不同的子类。接口描述符的 **bInterfaceSubClass** 字段指定接口的设备子类。

如果接口不满足这三个条件中的所有条件，则 Windows 将尝试单独枚举它，而不是将其与其他音频类接口分组。

如果接口关联描述符 (IAD) 存在于设备固件中，操作系统不会以特殊方式分组音频类接口。 IAD 方法始终是组合 USB 接口的首选方法。

本部分介绍与操作系统为其接口属于音频设备类的接口集合所创建的 PDO) 相关联的硬件和兼容标识符 (Id。

#### <a name="hardware-ids"></a>硬件 Id


`USB\VID_v(4)&PID_p(4)&Rev_r(4)&MI_z(2)`

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

在这些硬件 Id 中，

-   * (4) * 是 USB 标准委员会分配给供应商并从设备描述符的 **idVendor** 字段中提取的四位供应商代码。
-   *p (4) * 是供应商分配给设备并从设备描述符的 **idProduct** 字段中提取的四位数产品代码。
-   *r (4) * 是由供应商分配给设备并从设备描述符的 **bcdDevice** 字段中提取的四位设备版本号，采用二进制编码的十进制版本。
-   *z (2) * 是从接口描述符的 **bInterfaceNumber** 字段中提取的两位数接口号。

##### <a name="compatible-ids"></a>兼容 Id

`USB\Class_c(2)&SubClass_s(2)&Prot_p(2)`

`USB\Class_c(2)&SubClass_s(2)`

`USB\Class_c(2)`

在这些兼容 Id 中，c (2) ，s (2) ，p (2) 包含分别从每个接口集合中第一个 USB 接口描述符的 bInterfaceClass、bInterfaceSubClass 和 bInterfaceProtocol 字段中提取的值。

## <a name="related-topics"></a>相关主题
[USB 常规父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)