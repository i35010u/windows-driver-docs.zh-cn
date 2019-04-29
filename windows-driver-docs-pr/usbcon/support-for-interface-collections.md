---
Description: 可以在集合中分组复合的 USB 设备上的接口。 USB 通用父驱动程序 (Usbccgp.sys) 可以枚举中四种方法的接口集合。
title: 枚举 USB 复合设备上的接口集合
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 912d9a75ae21c48fc47ddf1a8c5d7a46527974b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324500"
---
# <a name="enumeration-of-interface-collections-on-usb-composite-devices"></a>枚举 USB 复合设备上的接口集合


可以在集合中分组复合的 USB 设备上的接口。 [USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)可以枚举中四种方法的接口集合。

按以下方式按层次结构排列的接口集合的枚举这四个方法：

1.  **供应商提供的回调例程**

    如果供应商已注册的回调例程[USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)，泛型父驱动程序，优先采用回调例程，并允许组接口的回调例程而非使用其他方法。 使用供应商提供的回调例程的接口集合的枚举的详细信息，请参阅[枚举的接口集合 USB 复合设备上](support-for-interface-collections.md)。

2.  **联合功能描述符**

    . 如果供应商启用了 CDC 和 WMCDC 枚举 USB 泛型父驱动程序中的，泛型父驱动程序将使用*联合功能描述符*(Ufd) 到组接口，用于集合。 启用时，此方法的优先级高于所有其他方法，但供应商提供的回调例程除外。 使用 Ufd 设备的枚举的详细信息，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

3.  **接口关联描述符**

    如果*接口关联描述符*(Iad) 是否存在后，USB 泛型父驱动程序始终组接口，通过使用 Iad 而不是使用旧方法。 Microsoft 建议供应商使用 Iad 定义接口集合。 枚举具有下列设备的详细信息，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

4.  **旧的音频方法。**

    USB 泛型父驱动程序都可以通过保留的旧技术用于音频函数枚举接口集合。 如果在设备上有任何 Iad 泛型父驱动程序不使用此方法。 旧的音频方法枚举的详细信息，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

##  <a name="customizing-enumeration-of-interface-collections-for-composite-devices"></a>自定义复合设备的接口集合的枚举


某些 USB 设备有 USB 接口关联描述符 (IAD) 不能描述的接口集合。 在 Windows Vista 和更高版本操作系统中，供应商可以自定义的方式[USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)定义并枚举设备的接口集合。 这是通过*枚举回调例程*筛选器驱动程序中。 回调例程可帮助定义设备的自定义接口集合泛型父驱动程序。

若要定义自定义接口集合的泛型父驱动程序，复合设备的供应商必须：

1.  实现枚举回调例程 ([**USBC\_启动\_设备\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff539007))。
2.  提供指向中的回调例程的指针*USB 设备配置界面*(**StartDeviceCallback**的成员[ **USBC\_设备\_配置\_界面\_V1**](https://msdn.microsoft.com/library/windows/hardware/ff538990))。
3.  提供了一个 INF 文件相匹配的设备 ID 的复合设备和显式加载 USB 泛型父驱动程序和筛选器驱动程序。

### <a name="implementation-considerations"></a>实现注意事项


包含枚举回调例程的筛选器驱动程序可以是大写或较低的筛选器驱动程序。 当 USB 泛型父驱动程序收到[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求以启动复合设备，它会询问是否 USB 设备通过发送配置界面[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)请求到驱动程序堆栈的顶部。

在收到[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)请求，筛选器驱动程序必须检查 GUID 类型， **InterfaceType**成员的请求，以验证所请求接口属于类型 USB\_总线\_接口\_USBC\_配置\_GUID。 如果是，筛选器驱动程序的界面中返回指向**接口**IRP 的成员。

枚举回调例程必须返回一个指向数组*函数描述符*([**USBC\_函数\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539001))用于描述的接口集合。 每个函数描述符包含接口描述符的数组 ([**USB\_界面\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff540065))，用于描述的接口集合。 回调例程必须从非分页缓冲池分配功能描述符和接口描述符。 泛型父驱动程序释放此内存。 回调例程必须确保**NumberOfInterfaces**的每个成员**USB\_接口\_描述符**准确地报告中的接口的数量接口集合。

泛型父驱动程序创建每个函数描述符的物理设备对象 (PDO)。

USB 设备配置接口和枚举回调例程中进行了总结[通用父驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usbccgp)。

### <a name="usb-generic-parent-driver-loading-mechanism"></a>USB 泛型父驱动程序加载机制


当复合设备满足所述的要求[枚举的 USB 复合设备](enumeration-of-the-composite-parent-device.md)，操作系统生成的一个兼容 ID `USB\COMPOSITE` ，表示设备是复合。 兼容 ID 生成 Usb.inf 中的匹配项，并在操作系统 USB 泛型父驱动程序，会自动加载，而无需帮助供应商提供的 INF 文件。

但是，这种默认机制并不适用于复合设备，需要自定义枚举的接口集合，因为在默认的机制在系统不会加载需供应商提供的筛选器驱动程序。 使枚举回调例程机制发挥作用，公开的 USB 设备配置接口的筛选器驱动程序必须已加载时 USB 泛型父枚举复合设备的接口集合。 这需要复合设备的供应商联系，以安装与复合设备的设备 ID 相匹配，并显式加载 USB 泛型父驱动程序和筛选器驱动程序的 INF 文件。


## <a name="support-for-the-wireless-mobile-communication-device-class"></a>对无线移动通信设备类的支持


在 Windows Vista [USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)支持通用串行总线 (USB) 通信设备类 (CDC) 和 USB 无线移动通信设备类 （中包含的设备WMCDC)。

USB 无线移动通信设备类 (WMCDC) 规范建立连接、 控制和在主机和无线移动设备 （例如，移动电话） 之间的内容交换的标准时将设备连接到 USB 端口。 WMCDC 是通信设备类 (CDC)，其中包含各种通信和网络设备的扩展。 本部分介绍在 Windows 操作系统中支持 CDC 和 WMCDC 设备的体系结构。

WMCDC 设备包含的分组为多个函数*逻辑手机*。 大多数 WMCDC 设备都有单个逻辑手机，但设备可能有多个逻辑手机。 逻辑手机通常包括诸如数据/传真调制解调器、 对象存储事件和调用控制设备。 逻辑手机可能还包括支持 USB 音频类规范、 USB 人工输入设备 (HID) 类规范和 USB 视频类规范等其他 USB 规范定义的函数。

Windows WMCDC 体系结构使用本机 Windows 驱动程序来管理 WMCDC 设备的功能。 例如，可以使用 Windows 电话服务应用程序程序接口 (TAPI) 子系统来管理你的设备和 Windows 网络驱动程序接口规格 (NDIS) 子系统来管理设备的以太网的语音和数据/传真调制解调器函数LAN 函数。 此外，你可以管理一些函数，如一个对象交换协议 (OBEX) 函数，在用户模式软件中的帮助下[WinUSB](winusb.md) (Winusb.sys)。

此图显示了 WMCDC 设备的示例驱动程序堆栈。

![示例设备配置和驱动程序堆栈](images/wmcdc-architecture.png)

在上图中，WMCDC 设备包含单个逻辑话筒： OBEX 函数和调制解调器函数。 供应商提供的 INF 文件加载本机 Windows 驱动程序来管理调制解调器。 OBEX 函数由运行中的供应商提供的用户模式驱动程序[用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff561365)(UMDF)。 用户模式驱动程序使用 Windows 便携式设备 (WPD) 协议与用户应用程序和接口进行通信， [WinUSB](winusb.md)导出与 USB 堆栈进行通信。 一般情况下，供应商提供的 INF 文件将加载的每个接口集合使用 Winusb.sys Winusb.sys 的单独实例。

### <a name="registry-settings"></a>注册表设置

USB 堆栈不会自动支持 WMCDC。 必须提供加载 Usbccgp.sys 的实例的 INF 文件。 INF 文件必须包含**AddReg**设置部分**EnumeratorClass**到 REG Usbccgp.sys 与相关联的软件密钥中的注册表值\_二进制值。从三个数字构造：0x02，0x00，和 0x00。 示例 INF 文件从下面的代码示例演示了如何设置**EnumeratorClass**为适当的值。

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

必须将分配给的值**EnumeratorClass**从 INF 文件中由对的十六进制数字表示的三个 1 字节二进制值构造：02、 00 和 00。 以下三个数字对应于 USB 实现论坛分配给 CDC 设备类、 CDC 设备子类和 CDC 设备协议，分别的值。

有关如何配置注册表，以正确地枚举 WMCDC 设备的详细信息，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

进一步的以下主题介绍 WMCDC:

### <a name="enumerating-interface-collections-on-wmcdc"></a>枚举 WMCDC 上的接口集合


USB 无线移动通信设备类 (WMCDC) 是 USB 通信设备类 (CDC) 的子类。 WMCDC 规范扩展，但从根本上改变定义接口集合 CDC 准则。 具体而言，WMCDC 设备必须遵从的 CDC 准则定义接口集合。

CDC 接口集合包含主接口 ([**USB\_界面\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff540065)) 属于通信接口类 (`bInterfaceClass = 0x02`) 或数据接口类 (`bInterfaceClass = 0x0A`)。 如果主接口属于通信接口类 （这是典型的情况下），主接口的子类 (**bInterfaceSubClass**) 指定 CDC*控制模型*。 控制模型表示的接口集合中包含的接口的类型。 有关 USB 实现论坛定义的控件模型的说明，请参阅 CDC 规范和 WMCDC 规范。

主接口的接口集合后跟一系列必需类特定于功能描述符，包括联合功能描述符 (UFD)。 UFD 列出了属于该集合的接口的数字。 **BMasterInterface** UFD 字段包含的主接口数。 零个或多**bSubordinateInterface**字段包含在集合中的其他 （从属） 接口的数字。

对于大多数类型的控件模型[USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)会为每个 UFD 创建一个物理设备对象 (PDO)。 但某些控件模型包括音频接口的泛型父驱动程序枚举单独从音频接口所属的接口集合。 在从属接口列表中显示的音频界面 (**bSubordinateInterface**) 的接口集合，但泛型父 UFD 驱动程序创建一个单独的 PDO 音频接口。 音频接口对 PDO 和音频接口所属的接口集合 PDO 是正上方的功能的设备对象 (FDO) 的设备对象树中父复合设备。 PDO 音频接口不是接口集合的子级。 音频接口的枚举中所述[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

在注册表中的枚举特征是可配置的两种控件模型： 无线手持控制模型 (WHCM)，它定义逻辑的话筒，以及对象交换协议 (OBEX) 控件模型。 若要配置这两个控件模型的枚举特征，必须提供 INF 文件加载的 Usbccgp.sys 实例和设置的值**CdcFlags** Usbccgp.sys 该实例的 software 项中。 下表描述了的配置选项**CdcFlags**。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>CdcFlags 位</th>
<th>位设置为 0</th>
<th>位设置为 1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0 (掩码 = 0x00000001)</p></td>
<td><p>USB 泛型父驱动程序创建一个单独的 PDO 为每个 OBEX 接口。</p></td>
<td><p>USB 泛型父驱动程序创建一个单一的 PDO 所有 OBEX 接口。</p></td>
</tr>
<tr class="even">
<td><p>1 (掩码 = 0x00000010)</p></td>
<td><p>USB 泛型父驱动程序不会为 WHCM 接口 （逻辑手机） 创建 PDOs。 这些接口保持隐藏状态的设备对象树的角度来看。</p></td>
<td><p>USB 泛型父驱动程序创建每个 WHCM 接口的 PDO。</p></td>
</tr>
</tbody>
</table>

 

例如，若要清除两个位 （将它们设置为 0），您的 INF 文件应具有以下行**DDInstall.AddReg**部分。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000000
```

若要将这两种位设置为 1，INF 文件应具有以下行。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000011
```

若要设置位 0 到 1，位 0 到 1，您的 INF 文件应具有以下行。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000001
```

其中一个位可以设置或重置，请独立于其他位。

下图演示了如何将不同的注册表配置可以创建不同的设备树，以便在同一设备。

下图演示了 PDO 配置，当这两位 0 和 1 的位**CdcFlags**均为 0。

![说明 cdcflags 的设备对象映射到的接口集合的关系图 = 0x00000000](images/cdcflags.png)

在上图中的无线手持控制模型 (WHCM) 接口集合包含三个从属的接口集合 (**bSubordinateInterface**): 两个 OBEX 集合和调制解调器集合。 位 0 的**CdcFlags**为 0，因此 USB 泛型父驱动程序不会创建 PDO WHCM 接口集合。 1 位**CdcFlags**为 0，因此 USB 泛型父驱动程序将生成一个单独的 PDO 为每个 OBEX 接口集合。

下图演示了 PDO 配置，当这两位 0 和 1 的位**CdcFlags**设置。

![说明 cdcflags 的设备对象映射到的接口集合的关系图 = 0x00010001](images/cdcflags-wpd.png)

因为位 0 个，共**CdcFlags**设置为 1，USB 泛型父驱动程序创建 PDO WHCM 接口集合。 由于第 1 的位**CdcFlags**与设置为 1，USB 泛型父驱动程序组两个 OBEX 集合在一起，并生成一个单一的 PDO 为两个 OBEX 集合。

您可能希望以表示与在内核级别单一 PDO OBEX 集合和以区分每个单独的 OBEX 集合内的用户模式驱动程序。 Windows 便携式设备 (WPD) 协议可以帮助您进行多路复用不同的 OBEX 函数在用户级别，当所有 OBEX 函数分组到一个单一的 PDO 在内核级别之间的数据流。

下面的示例 INF 文件加载 USB 泛型父驱动程序管理 WMCDC 设备，并指示 USB 泛型父 PDOs 创建逻辑手机，在逻辑手机中创建一个单一的 PDO 所有 OBEX 集合。

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


USB 泛型父驱动程序以特殊方式处理无线手持控制模型 (WHCM) 接口，如中所述[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

以下列表总结了 CDC 和 WMCDC 接口的集合处理不同于其他接口集合的最重要方法：

-   无线移动通信设备类允许有限的数量的嵌套的接口集合。 具体而言，逻辑话筒接口集合 （即，WHCM 接口集合） 可以包含其他从属接口集合。 例如，WMCDC 符合 phone 可以 WHCM 接口集合，其中又包含抽象控件模型集合和 OBEX 集合。
-   你可以配置 USB 泛型父驱动程序不能枚举 WHCM 接口集合。 不会枚举的 WHCM 接口集合保持为隐藏，但泛型父驱动程序将使用联合功能描述符 (Ufd) 属于 WHCM 接口集合进行分组和枚举从属接口集合中的信息。
-   对于 OBEX 控件模型接口集合，或创建一个单一的 PDO 所有 OBEX 控件模型接口集合，你可以配置 USB 泛型父驱动程序创建单独的物理设备对象 (PDOs)。
-   接口中的数字 UFD 列表可能具有间断。 也就是说，UFD 接口号可以引用并不连续的接口。 这种类型的编号不是有效的例如，对于[USB 接口关联描述符 (IAD)](usb-interface-association-descriptor.md)、 必须是连续的其接口和具有连续数字。
-   Ufd 可以包含相关的音频接口集合
-   CDC 和 WMCDC 接口集合的硬件标识符 (Id) 必须包含接口子类。 其他 USB 接口，其硬件 Id 包含 MI\_%02x X 后缀指定接口数，不包含信息的接口子类。 子类信息包含在硬件 ID，以允许供应商的硬件 ID 匹配项，对于特定的接口集合，而不是依赖于接口的描述符布局，以确定要加载的驱动程序中的位置提供 INF 文件找不到。 中的硬件 ID 的子类信息还允许从当前供应商提供的驱动程序管理 WMCDC 替代项，例如用户模式驱动程序的接口集合的逐步迁移路径。 有关 CDC 和 WMCDC 硬件 Id 的示例，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。 Id 的格式有关的如何 USB 接口硬件的一般讨论，请参阅[USB 设备的标识符](https://msdn.microsoft.com/library/windows/hardware/ff546284)。

### <a name="cdc-and-wmcdc-control-models"></a>CDC 和 WMCDC 控件模型


CDC 和 WMCDC 控件模型部分介绍在 Microsoft Windows 操作系统中支持的接口集合的属性。 此外，每个说明包括 USB 泛型父驱动程序将生成的接口集合硬件和设备标识符 (Id) 的列表。

大多数 Windows 支持的接口集合的对应于控件模型属于的通信设备类 (CDC) 和无线移动通信设备类 (WMCDC)，但操作系统也支持旧的音频和视频接口集合，并且移动计算提升联盟 (MCPC) 定义的接口集合。

在本部分中描述的接口集合如下所示：

#### <a name="audio-class-interfaces"></a>音频类接口


发生在 CDC 和 WMCDC 设备的 USB 音频设备类接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线的设备类定义音频设备</em>，版本 1.0。</p></td>
</tr>
<tr class="even">
<td><p>类</p></td>
<td><p>接口集合中的所有接口必须都属于音频设备类 (0x01)。</p></td>
</tr>
<tr class="odd">
<td><p>子类</p></td>
<td><p>从集合中的第一个接口，接口集合中的每个接口必须具有不同子类。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>零个或多个连续接口属于流式处理子类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;MI_%02x</code></pre>
<p>硬件 Id 的音频的接口集合不包含接口类特定的信息。 有关硬件与音频接口集合关联的 Id 的格式设置的说明，请参阅<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">支持无线移动通信设备类</a>。</p></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_01&amp;SubClass_01&amp;Prot_00
USB\Class_01&amp;SubClass_01
USB\Class_01</code></pre>
<p>对于音频接口集合兼容 Id 的格式包含嵌入的接口类、 接口子类和协议有关的信息。 对于 CDC 或 WMCDC 设备上的音频的接口集合，接口类为 01，子类是 01，协议为 00。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-abstract-control-model"></a>CDC 抽象控制模型


有两个版本的抽象控制模型 (ACM)。 中定义的原始版本*USB 通信设备类*(CDC) 规范。 *USB 无线移动通信设备类*(WMCDC) 规范包含 ACM 的扩展的定义。

符合 WMCDC 规范的接口集合中所述[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

符合 CDC 规范的接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.6.2。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>ACM (0X02)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>任何。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>一个数据类接口和可选的音频类接口的联合功能描述符 (UFD) 引用。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_02&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_02
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_02&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_02</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_02&amp;Prot_%02X
USB\Class_02&amp;SubClass_02
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>UFD 可以引用一个音频接口集合，这些枚举独立于 ACM 接口集合。</p></td>
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
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.8.3 将现有</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>ANCM (0x07)</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>通过联合功能描述符 (UFD) 引用的一个数据类接口</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_07&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_07
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_07&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_07</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_07&amp;Prot_00
USB\Class_02&amp;SubClass_07
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>


#### <a name="cdc-capi-control-model"></a>CDC CAPI 控制模型


USB CDC 常见 ISDN API (CAPI) 控件模型接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em></em></p>
<p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.7.2</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>CAPI (0x05)</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_05&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_05</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_05&amp;Prot_00
USB\Class_02&amp;SubClass_05</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-direct-line-control-model"></a>CDC 直接行控制模型


USB CDC 直接行控制模型 (DLCM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.6.1。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>DLCM (0x01).</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>音频类或供应商定义的接口的联合功能描述符 (UFD) 引用。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_01&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_01
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_01&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_01</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_01&amp;Prot_00
USB\Class_02&amp;SubClass_01
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>UFD 引用独立于 DLCM 接口集合枚举的音频类接口集合。</p></td>
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
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.8.2。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>ENCM (0X06:SP)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_06&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_06
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_06&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_06</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_06&amp;Prot_00
USB\Class_02&amp;SubClass_06
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>此控件模型的兼容 Id 有匹配项，Microsoft 提供的 INF 文件中。 如果操作系统不会在供应商提供 INF 文件中找到一个硬件 Id 的匹配项，系统会自动加载的本机 NDIS 微型端口驱动程序管理的接口集合。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-multi-channel-isdn-control-model"></a>CDC 多渠道 ISDN 控制模型


USB CDC 多渠道 ISDN 控制模型 (MCCM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.7.1</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>MCCM (0x04)</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的多个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_04&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_04
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_04&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_04</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_04&amp;Prot_00
USB\Class_02&amp;SubClass_04
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 
#### <a name="cdc-telephone-control-model"></a>CDC 电话控制模型


USB CDC 电话控制模型 (TCM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线类定义通信设备</em>，版本 1.1 中，部分 3.6.3。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>TCM (0X03)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>任何。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的音频类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 ID</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_03&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_03
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_03&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_03</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 ID</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_03&amp;Prot_%02X
USB\Class_02&amp;SubClass_03
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>UFD 可以引用一个音频类接口集合，这些枚举独立于 TCM 接口集合。</p></td>
</tr>
</tbody>
</table>

#### <a name="mcpc-vendor-unique-interfaces"></a>MCPC 供应商独特的接口


移动计算提升联盟 (MCPC) 定义的接口集合之前提供一种格式的唯一供应商 CDC 设备的无线移动通信设备类 (WMCDC) 规范的格式。 因此，MCPC 接口集合不符合 WMCDC 标准。

但是，如果启用 WMCDC USB 泛型父驱动程序，就可以枚举 MCPC 接口集合。 MCPC 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p>移动计算提升联盟 (MCPC) GL 004 规范</p></td>
</tr>
<tr class="even">
<td><p>类</p></td>
<td><p>CDC (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>子类</p></td>
<td><p>0x88</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的零个或多个数据类接口</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_88&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_88
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_88&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_88</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_88&amp;Prot_00
USB\Class_02&amp;SubClass_88
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

#### <a name="video-class-interfaces"></a>视频类接口


发生在 CDC 和 WMCDC 设备的 USB 视频设备类接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线的设备类定义视频设备</em>，版本 1.0。</p></td>
</tr>
<tr class="even">
<td><p>类</p></td>
<td><p>视频 (0x0E)。</p></td>
</tr>
<tr class="odd">
<td><p>子类</p></td>
<td><p>视频控件 (0x01)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>零个或多个连续接口属于流式处理子类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;MI_%02x</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_0E&amp;SubClass_01&amp;Prot_00
USB\Class_0E&amp;SubClass_01
USB\Class_0E</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>视频类接口集合接收 CDC 设备上的特殊处理。 在非 CDC 设备上由接口关联描述符 (Iad) 定义视频类接口集合。 CDC 设备上由联合功能描述符 (Ufd) 定义视频类接口集合。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-abstract-control-model"></a>WMCDC 抽象控制模型


有两个版本的抽象控制模型 (ACM)。 USB 通信设备类 (CDC) 规范中定义的原始版本。 USB 无线移动通信设备类 (WMCDC) 规范包含 ACM 的扩展的定义。 ACM 集合，其中包含传真调制解调器函数应使用的 ACM WMCDC 定义而不是原始的 CDC ACM 定义。

符合 CDC 规范的接口集合中所述[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

符合 WMCDC 规范的接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线 CDC 子类规范适用于无线移动通信设备</em>，版本 1.0，第 6.2 节。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>ACM (0X02)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>如果集合使用一个在命令设置协议，在兼容 Id 中嵌入的协议值是 0x01。 如果集合使用 WMCDC 规范描述的协议之一，在兼容 Id 中嵌入的协议值是 0x2 通过 0x06:sp 或 0xFE。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_Modem&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_Modem
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_Modem&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_Modem</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_Modem&amp;Prot_%02X
USB\Class_02&amp;SubClass_Modem
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>UFD 可能引用一个音频接口集合，这些枚举独立于 ACM 接口集合。</p>
<p>接口集合必须符合 WMCDC 规范第 6.2 节中指定的特殊描述符和终结点要求。 如果接口集合不符合 WMCDC 要求，但接口符合 CDC 要求，USB 泛型父驱动程序将枚举的接口集合和泛型硬件 Id 与 CDC 格式中所述<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">支持的无线移动通信设备类</a>。</p>
<p>此控件模型的兼容 Id 有匹配项，Microsoft 提供的 INF 文件中。 如果操作系统不会在供应商提供 INF 文件中找到一个硬件 Id 的匹配项，系统会自动加载本机电话应用程序编程接口 (TAPI) 调制解调器筛选器驱动程序管理的调制解调器函数和集除非协议代码是 0xFE 适当 TAPI 注册表设置。 如果协议代码是 0xFE，供应商必须提供设备或类共同安装程序来正确填充 TAPI 注册表设置。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-device-management-model"></a>WMCDC 设备管理模型


USB WMCDC 设备管理模型 (DMM) 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线 CDC 子类规范适用于无线移动通信设备</em>，1.0，部分 6.6 版。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>DMM (0X09)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>任何。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_09&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_09
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_09&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_09</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_09&amp;Prot_%02X
USB\Class_02&amp;SubClass_09
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>此控件模型不使用联合功能描述符 (UFD)。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-mobile-direct-line-model"></a>WMCDC 移动的直拨电话模型


USB WMCDC 移动直接行模型 (MDLM) 接口集合具有以下属性：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线 CDC 子类规范适用于无线移动通信设备</em>，版本 1.0，部分 6.7</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>MDLM (0x0A)</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>Any</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>一个或多个数据类接口的联合功能描述符 (UFD) 引用</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_0A&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_0A
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_0A&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_0A</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_0A&amp;Prot_%02X
USB\Class_02&amp;SubClass_0A
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>无。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-obex-control-model-multiple-pdos"></a>WMCDC OBEX 控制模型 (多个 PDOs)


有两种方法来枚举对象交换协议 (OBEX) 控件模型接口集合： USB 泛型父驱动程序可以组合所有组合在一起的 OBEX 接口，并为所有 OBEX 接口中，都创建单个物理设备对象 (PDO) 或父驱动程序可以创建一个单独的 PDO 为每个 OBEX 接口。 有关硬件 USB 泛型父驱动程序组合在一起的 OBEX 接口生成的 Id 的说明，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

当 USB 泛型父驱动程序将单独 PDOs 分配给每个 OBEX 接口时，PDOs 具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线 CDC 子类规范适用于无线移动通信设备</em>，1.0，部分 6.5 版。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>OBEX (0X0B)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_0B&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_0B
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_0B&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_0B</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_0B&amp;Prot_00
USB\Class_02&amp;SubClass_0B
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>管理复合设备的 USB 泛型父驱动程序的实例相关联的注册表设置确定是否使用单一 PDO 或多个 PDOs 管理 OBEX 接口。 指定 USB 泛型父驱动程序如何枚举 OBEX 接口的注册表设置的说明，请参阅<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">支持无线移动通信设备类</a>。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-obex-control-model-single-pdo"></a>WMCDC OBEX 控制模型 (单个 PDO)


有两种方法来枚举对象交换协议 (OBEX) 控件模型接口集合： USB 泛型父驱动程序可以组合所有组合在一起的 OBEX 接口，并为所有 OBEX 接口中，都创建单个物理设备对象 (PDO) 或父驱动程序可以创建一个单独的 PDO 为每个 OBEX 接口。 有关硬件 USB 泛型父驱动程序为单独枚举的 OBEX 接口生成的 Id 的说明，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

当 USB 泛型父驱动程序将单个 PDO 分配给所有的 OBEX 接口时，PDO 具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线 CDC 子类规范适用于无线移动通信设备</em>，1.0，部分 6.5 版。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>OBEX (0X0B)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>联合功能描述符 (UFD) 引用的一个数据类接口。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;WPD_OBEX&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;WPD_OBEX
USB\Vid_%04x&amp;Pid_%04x&amp;WPD_OBEX&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;WPD_OBEX</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;WPD_OBEX
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>管理复合设备的 USB 泛型父驱动程序的实例相关联的注册表设置确定是否使用单一 PDO 或多个 PDOs 管理 OBEX 接口。 指定 USB 泛型父驱动程序如何枚举 OBEX 接口的注册表设置的说明，请参阅<a href="support-for-interface-collections.md" data-raw-source="[Enumeration of Interface Collections on USB Composite Devices](support-for-interface-collections.md)">枚举的接口集合 USB 复合设备上</a>。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-wireless-handset-control-model"></a>WMCDC 无线手持控制模型


USB 泛型父驱动程序不会始终枚举无线手持控制模型 (WHCM) 接口集合。 与 USB 泛型父驱动程序，用于管理 WHCM 接口集合的实例相关联的注册表设置确定是否 USB 泛型父驱动程序为创建一个物理设备对象 (PDO) 接口集合或不。 指定 USB 泛型父驱动程序如何枚举 WHCM 接口的注册表设置的说明，请参阅[枚举的接口集合 USB 复合设备上](support-for-interface-collections.md)。

枚举的 WHCM 接口集合具有以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>参考</p></td>
<td><p><em>通用串行总线 CDC 子类规范适用于无线移动通信设备</em>，1.0，部分 6.1 版。</p></td>
</tr>
<tr class="even">
<td><p>主接口的类</p></td>
<td><p>通信接口类 (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>主接口的子类</p></td>
<td><p>WHCM (0X08)。</p></td>
</tr>
<tr class="even">
<td><p>协议</p></td>
<td><p>无 (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>枚举</p></td>
<td><p>是。</p></td>
</tr>
<tr class="even">
<td><p>相关的接口</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p>硬件 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_08&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_08
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_08&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_08</code></pre></td>
</tr>
<tr class="even">
<td><p>兼容 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_08&amp;Prot_00
USB\Class_02&amp;SubClass_08
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特殊处理</p></td>
<td><p>联合功能描述符 (UFD) 标识与逻辑话筒相关联的接口。</p></td>
</tr>
</tbody>
</table>

在前面的主题中的硬件 ID 格式描述使用以下约定：

- C 语言**printf**格式表示的整数。 例如，"%04x x"表示一个 4 位十六进制整数时，"%02x x"意味着 2 位数字表示十六进制整数，依次类推。

- 字符串之后的整数"Vid\_"是 USB 委员会 (www.usb.org) 将分配给供应商的供应商代码 4 位十六进制表示形式。

- 字符串之后的整数"Pid\_"是供应商将分配给设备的产品代码 4 位十六进制表示形式。

- 字符串之后的整数"Rev\_"是设备的修订号的 4 位十六进制表示形式。

- 字符串之后的整数"Cdc\_"是接口子类。

- 字符串之后的整数"端口是否\_"协议号。

- 字符串之后的整数"MI\_"是接口数量，从提取的 2 位数字表示十六进制表示形式**bInterfaceNumber**接口描述符字段。


### <a name="enumeration-of-interface-collections-on-usb-devices-with-iads"></a>在使用 Iad USB 设备上的接口集合的枚举


如果 USB 复合设备具有在其固件中的接口关联描述符 (IAD)，Windows 枚举接口集合，就好像每个集合是单个设备，并将单个物理设备对象 (PDO) 分配到每个接口集合和PDO 相关联的硬件和兼容的标识符 (Id)。 Iad 的详细说明，请参阅[USB 接口关联描述符](usb-interface-association-descriptor.md)。 本部分介绍的硬件 Id 和兼容标识符 (Id) 分配给 IAD 与关联的接口集合。

##  <a name="hardware-ids"></a>硬件 Id


`USB\VID_v(4)&PID_p(4)&Rev_r(4)&MI_z(2)`

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

在这些硬件 Id

-   *v(4)* 是 USB 委员会将分配给供应商的四位数字表示供应商代码并从提取**idVendor**设备描述符字段。
-   *p(4)* 是供应商将分配给设备的四位数字产品代码和从提取**idProduct**设备描述符字段。
-   *r(4)* 是四位数字设备发行版号，在二进制编码的十进制修订版本，供应商将分配给设备并从提取**bcdDevice**设备描述符字段。
-   *z(2)* 是从提取的两位数字接口编号**bFirstInterface** IAD 字段。

#### <a name="compatible-ids"></a>兼容 Id


`USB\Class_c(2)&SubClass_s(2)&Prot_p(2)`

`USB\Class_c(2)&SubClass_s(2)`

`USB\Class_c(2)`

在这些兼容 Id c(2)、 s(2) 和 p(2) 包含获取的值分别从**bFunctionClass**， **bFunctionSubClass**，并**bFunctionProtocol**IAD 字段。

不能使用 Iad 以递归方式将绑定的函数的函数。 具体而言，如果设备具有在其固件中 IAD 描述符，泛型父驱动程序将不进行分组接口由音频设备类，如中所述[枚举的接口集合 USB 复合设备上](support-for-interface-collections.md)。

### <a name="enumeration-of-interface-collections-on-audio-devices-without-iads"></a>而无需 Iad 音频设备上的接口集合的枚举


对于音频设备，Windows 操作系统可枚举的接口 （接口集合） 与函数相关联的组并将单个物理设备对象 (PDO) 分配给每个组，即使设备没有接口关联描述符 (IAD)。

操作系统为接口集合，如组复合音频设备的接口，如果接口满足以下条件：

-   接口集合中的所有接口必须都是连续的。 换而言之，接口必须与另一个在固件内存中相邻。
-   接口集合中的所有接口必须都属于的音频设备类。 设备制造商指定属于到音频设备类的接口通过赋值到 0x01 **bInterfaceClass**接口描述符字段。
-   从集合中的第一个接口，接口集合中的每个接口必须具有不同子类。**BInterfaceSubClass**接口描述符字段指定该接口的设备子类。

如果接口不符合以下所有三个条件，则 Windows 将尝试单独而不是其分组的其他音频类接口对其进行枚举。

如果接口关联描述符 (IAD) 设备固件中存在，操作系统不对音频类接口分组以特殊方式。 IAD 方法始终是分组 USB 接口的首选的方法。

本部分介绍硬件和与 PDO 创建的适用于其接口属于音频设备类的接口集合相关联的标识符 (Id) 兼容。

#### <a name="hardware-ids"></a>硬件 Id


`USB\VID_v(4)&PID_p(4)&Rev_r(4)&MI_z(2)`

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

在这些硬件 Id

-   *v(4)* 是 USB 标准委员会将分配给供应商的四位数字表示供应商代码并从提取**idVendor**设备描述符字段。
-   *p(4)* 是供应商将分配给设备的四位数字产品代码和从提取**idProduct**设备描述符字段。
-   *r(4)* 是四位数字设备发行版号，在二进制编码的十进制修订版本，供应商将分配给设备并从提取**bcdDevice**设备描述符字段。
-   *z(2)* 是从提取的两位数字接口编号**bInterfaceNumber**接口描述符字段。

##### <a name="compatible-ids"></a>兼容 Id

`USB\Class_c(2)&SubClass_s(2)&Prot_p(2)`

`USB\Class_c(2)&SubClass_s(2)`

`USB\Class_c(2)`

在这些兼容 Id c(2)、 s(2) 和 p(2) 包含取自，分别 bInterfaceClass、 bInterfaceSubClass 和每个接口集合中的第一个 USB 接口描述符 bInterfaceProtocol 字段的值。

## <a name="related-topics"></a>相关主题
[USB 泛型父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



