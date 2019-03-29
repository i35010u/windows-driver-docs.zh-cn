---
Description: 在本主题中，将了解如何在 Windows 8 中识别 WinUSB 设备。
title: WinUSB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab0ae35ab57fdbea90f6b7c4a143b3c36b161cfc
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464165"
---
# <a name="winusb-device"></a>WinUSB 设备


在本主题中，您将学习有关如何*WinUSB 设备*在 Windows 8 中识别。

本主题中的信息适用于您，如果您是 OEM 或独立硬件供应商 (IHV) 开发你想要为功能驱动程序使用 Winusb.sys 并且想要自动加载的驱动程序，而无需提供自定义 INF 的设备。

- [WinUSB 设备](#winusb-device)
  - [什么是 WinUSB 设备](#what-is-a-winusb-device)
  - [通过使用内置 Winusb.inf WinUSB 设备安装](#winusb-device-installation-by-using-the-in-box-winusbinf)
    - [有关使用 USBDevice 类：](#about-using-the-usbdevice-class)
  - [如何更改 WinUSB 设备的设备说明](#how-to-change-the-device-description-for-a-winusb-device)
  - [如何将 WinUSB 设备配置](#how-to-configure-a-winusb-device)
  - [相关的主题](#related-topics)

## <a name="what-is-a-winusb-device"></a>什么是 WinUSB 设备


WinUSB 设备是其固件定义某些 Microsoft 操作系统 (OS) 功能描述符"WINUSB"作为该报表的兼容 ID 的通用串行总线 (USB) 设备。

WinUSB 设备旨在启用 Windows 设备的功能驱动程序不使用自定义的 INF 文件作为加载 Winusb.sys。 对于 WinUSB 设备，不需要分发 INF 文件为你的设备，使驱动程序安装过程的最终用户更简单。 相反，如果你需要提供自定义 INF，应不为 WinUSB 设备定义你的设备，并在 INF 中指定的设备硬件 ID。

Microsoft 提供了 Winusb.inf 包含安装 Winusb.sys 为 USB 设备的设备驱动程序所需的信息。

在 Windows 8 之前加载 Winusb.sys 作为函数驱动程序，你需要提供自定义 INF。 自定义 INF 指定特定于设备的硬件 ID，并还包括从现成 Winusb.inf 的部分。 这些部分所需的实例化此服务中，复制收件箱二进制文件和注册设备接口的应用程序所需找到设备并与它交互的 GUID。 有关编写自定义 INF 的信息，请参阅[WinUSB (Winusb.sys) 安装](winusb-installation.md#inf)。

在 Windows 8 中，已更新现成 Winusb.inf 文件以启用 Windows 自动通过 WinUSB 设备匹配 INF。

## <a name="winusb-device-installation-by-using-the-in-box-winusbinf"></a>通过使用内置 Winusb.inf WinUSB 设备安装


在 Windows 8 中，已更新现成 Winusb.inf 文件。 INF 包括安装部分中引用一个兼容 ID，即"USB\\MS\_COMP\_WINUSB"。

```cpp
[Generic.Section.NTamd64]
%USB\MS_COMP_WINUSB.DeviceDesc%=WINUSB,USB\MS_COMP_WINUSB 
```

更新的 INF 还包括一个名为"USBDevice"的新安装程序类。

"USBDevice"安装程序类是适用于 Microsoft 不提供现成驱动程序这些设备。 通常情况下，此类设备不属于定义完善的 USB 类，如音频、 蓝牙等，并且需要自定义驱动程序。 如果你的设备是 WinUSB 设备，最有可能，设备不属于 USB 类。 因此，你的设备必须安装在"USBDevice"安装程序类。 更新的 Winusb.inf 促进这一要求。

### <a name="about-using-the-usbdevice-class"></a>有关使用 USBDevice 类：

不要为未分类的设备使用的"USB"安装程序类。 此类保留用于安装控制器、 中心和复合设备。 误用"USB"类可能会导致相当重要的可靠性和性能问题。 对于未分类的设备，使用"USBDevice"。

在 Windows 8 中，若要使用"USBDevice"设备类，只需添加到你 INF:

```cpp
  …
  [Version] 
  Class=USBDevice 
  ClassGuid={88BAE032-5A81-49f0-BC3D-A4FF138216D6}
  …
```

设备管理器中，您将看到新节点**USB 通用串行总线设备**和你的设备显示该节点下。
<p>在 Windows 7 中，除了前面的行中，您需要在 INF 中创建这些注册表设置：

```cpp
  ;---------- Add Registry Section ----------
  [USBDeviceClassReg] 
  HKR,,,,"Universal Serial Bus devices"
  HKR,,NoInstallClass,,1
  HKR,,SilentInstall,,1 
  HKR,,IconPath,%REG_MULTI_SZ%,"%systemroot%\system32\setupapi.dll,-20"
```

在设备管理器中，将看到设备下**USB 通用串行总线设备**。 但是，设备类描述派生自你 INF 中指定的注册表设置。

*-Eliyas Yakub，Microsoft Windows USB 核心团队*

 

请注意"USBDevice"类并不局限于 WinUSB。 如果设备有自定义驱动程序，您可以使用"USBDevice"安装程序类中自定义 INF。

在设备枚举期间 USB 驱动程序堆栈从设备读取兼容 ID。 如果兼容 ID 为"WINUSB"，Windows 将其用作设备标识符和已更新现成 Winusb.inf，找到了匹配项并加载 Winusb.sys 作为设备的功能驱动程序。

此映像是一个接口定义为 WinUSB 设备 MUTT 设备，作为设备的功能驱动程序加载 Winusb.sys 获取结果。

![显示 winusb 设备的设备管理器。](images/winusb-device.png)

对于版本的 Windows 早于 Windows 8，更新的 Winusb.inf 是可通过**Windows Update**。 如果您的计算机配置为自动获取驱动程序更新，将使用新的 INF 包而无需任何用户干预安装 WinUSB 驱动程序。

## <a name="how-to-change-the-device-description-for-a-winusb-device"></a>如何更改 WinUSB 设备的设备说明


对于 WinUSB 设备，设备管理器显示"WinUsb 设备"作为设备说明。 该字符串被派生自 Winusb.inf。 如果有多个 WinUSB 设备，所有设备都获取相同的设备说明。

唯一地标识和区分设备在设备管理器，Windows 8 提供了一个新的属性指示系统在赋予优先权设备报告的设备描述的设备类上 (在其**iProduct**字符串描述符） 通过 INF 中的说明。 在 Windows 8 中定义的"USBDevice"类设置此属性。 换而言之，"USBDevice"类下安装设备时，系统将查询设备描述的设备和设备管理器的字符串设置为在查询中检索的任何内容。 在这种情况下，将忽略 INF 中提供的设备说明。 请注意设备描述字符串："MUTT"在上图中。 通过其产品字符串描述符中的 USB 设备提供字符串。

在早期版本的 Windows 不支持新的类属性。 若要自定义的设备描述在早期版本的 Windows 上，你已将你自己的自定义 INF。

## <a name="how-to-configure-a-winusb-device"></a>如何将 WinUSB 设备配置


若要标识为 WinUSB 设备的 USB 设备，设备固件必须具有 Microsoft OS 描述符。 有关描述符信息，请参阅此处所述的规范：[Microsoft OS 描述符](microsoft-defined-usb-descriptors.md)。

**支持扩展的功能描述符**

为了使 USB 驱动程序堆栈，以了解设备支持扩展的功能描述符，设备必须定义存储在字符串索引 0xEE OS 字符串描述符。 枚举，过程将驱动程序堆栈查询字符串描述符。 如果存在描述符，则驱动程序堆栈假定设备包含一个或多个操作系统功能描述符和需要检索这些功能描述符的数据。

检索的字符串描述符**bMS\_VendorCode**字段值。 值指示 USB 驱动程序堆栈必须使用要检索的扩展的功能描述符的供应商代码。

有关如何定义 OS 信息的字符串描述符，请参阅此处所述的规范中的"OS 字符串描述符":[Microsoft OS 描述符](microsoft-defined-usb-descriptors.md)。

**设置兼容 ID**

扩展的兼容 ID 操作系统功能需要匹配现成 Winusb.inf 和加载 WinUSB 驱动程序模块的描述符。

扩展的兼容 ID 操作系统功能描述符包含后跟一个或多个函数部分，具体取决于设备是一个复合或非复合设备的标头部分。 标头部分指定整个描述符、 的函数部分数和版本号的长度。 对于非复合设备，该标头后跟与设备的唯一接口相关联的一个函数部分。 **CompatibleID**该部分的字段必须为字段值指定"WINUSB"。 对于复合设备，有多个函数部分。 **CompatibleID**每个函数部分的字段必须指定"WINUSB"。

**注册设备接口的 GUID**

应用注册其设备接口的 GUID 所需的操作系统的扩展的属性功能描述符。 GUID 是需要找到应用程序或服务从设备、 配置设备，并执行 I/O 操作。

在以前版本的 Windows 中，设备接口 GUID 注册是通过自定义 INF。 从 Windows 8 开始，你的设备应通过使用扩展的属性操作系统功能描述符报告接口的 GUID。

扩展的属性操作系统功能描述符包含后跟一个或多个自定义属性部分的标头部分。 标头部分将介绍整个扩展的属性描述符，包括其总长度、 版本号和数量的自定义属性部分。 若要注册的设备接口的 GUID，请添加设置自定义属性部分**bPropertyName** "DeviceInterfaceGUID"字段和**wPropertyNameLength**到 40 个字节。 通过使用 GUID 生成器生成唯一的设备接口的 GUID 和设置**bPropertyData**字段为该 GUID，例如"{8FE6D4D7-49DD-41E7-9486-49AFC6BFE475}"。 请注意，GUID 指定为 Unicode 字符串的字符串的长度为 78 字节 （包括 null 终止符）。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>bPropertyData</strong></td>
<td>78 字节</td>
<td><p>7B 00 38 00 46 00 45 00 36 00 44 00 34 00 44 00 37 00 00 34 00 39 00 00 44 00 2D 2D 00 34 00 31 00 45 00 37 00 00 39 00 34 00 38 00 36 00 2D 2D 00 34 00 39 00 41 0046 00 43 00 36 00 42 00 46 00 45 00 34 00 37 00 35 00 7 D 00 00 00</p></td>
<td>属性值为 {8FE6D4D7-49DD-41E7-9486-49AFC6BFE475}。</td>
</tr>
</tbody>
</table>

 

在设备枚举期间 USB 驱动程序堆栈然后检索**DeviceInterfaceGUID**的扩展的属性操作系统功能描述符中的值并注册设备中设备的硬件密钥。 应用程序可以使用检索该值**SetupDiXxx** Api (请参阅[ **SetupDiOpenDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552079))。 有关详细信息，请参阅[如何访问由使用 WinUSB 函数 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

**启用或禁用 WinUSB 电源管理功能**

在之前 Windows 8 中，若要配置电源管理功能的 WinUSB，您必须写入注册表项值**硬件。AddReg**的自定义 INF 部分。

在 Windows 8 中，可以指定在设备中的电源设置。 你可以报告通过 OS 的扩展的属性功能描述符的值启用或禁用 WinUSB 中为该设备的功能。 有两个功能，我们可以配置： 选择性挂起和系统唤醒。 选择性挂起，设备将处于空闲状态时进入低功耗状态。 系统唤醒是指到设备的功能时系统处于低电源状态下唤醒系统。

WinUSB 的电源管理功能的信息，请参阅[WinUSB 电源管理](winusb-power-management.md)。

| 属性名            | 描述                                                                                                                                                                                                                                                                                                                               |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DeviceIdleEnabled        | 此值设置为 1 以指示设备可以关闭电源，空闲时 (选择性挂起)。                                                                                                                                                                                                                                          |
| DefaultIdleState         | 此值设置为 1 以指示设备可以挂起空闲时默认情况下。                                                                                                                                                                                                                                                 |
| DefaultIdleTimeout       | 此值设置为以毫秒为单位的 5000，以指示以毫秒为单位确定设备处于空闲状态之前要等待的时间量。                                                                                                                                                                                                |
| UserSetDeviceIdleEnabled | 此值设置为 1 以允许用户控制的功能的设备启用或禁用 USB 选择性挂起。 复选框**允许计算机关闭此设备以节约电源**设备上**电源管理**属性页和用户可以选中或取消选中相应的框以启用或禁用 USB 选择性挂起。 |
| SystemWakeEnabled        | 此值设置为 1 以允许用户控制的设备的唤醒从低功耗状态系统的功能。 启用时，**允许此设备唤醒计算机**设备电源管理属性页中显示复选框。 用户可以选中或取消选中相应的框以启用或禁用 USB 系统唤醒。         |

 

例如，若要启用选择性挂起设备上，添加设置自定义属性部分**bPropertyName**字段为 Unicode 字符串，"DeviceIdleEnabled"和**wPropertyNameLength**到 36 个字节。 设置**bPropertyData** "0x00000001"字段。 属性值存储为小字节序 32 位整数。

在枚举期间 USB 驱动程序堆栈读取扩展的属性功能描述符并创建此项下的注册表项：

**HKEY\_本地\_MACHINE**\\**系统**\\**CurrentControlSet**\\**枚举**\\ **USB**\\***&lt;设备标识符&gt;***\\***&lt;实例标识符&gt;***  \\**设备参数**

此图显示了示例 WinUSB 设备的设置。

![winusb 设备的注册表设置](images/winusb-device-reg.png)

有关其他示例，请参阅 》 上的规范[Microsoft OS 描述符](microsoft-defined-usb-descriptors.md)。

## <a name="related-topics"></a>相关主题
[Microsoft 定义 USB 描述符](microsoft-defined-usb-descriptors.md)  



