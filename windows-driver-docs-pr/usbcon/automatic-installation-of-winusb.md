---
description: 在本主题中，你将了解如何在 Windows 8 中识别 WinUSB 设备。
title: WinUSB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2458e4d33aef9d4f6b4beae802a542bb5c984a1
ms.sourcegitcommit: 022dc99fdf23dc3501a3cebeb3c0698d504e31c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107325032"
---
# <a name="winusb-device"></a>WinUSB 设备


在本主题中，你将了解如何在 Windows 8 中识别 *WinUSB 设备* 。

本主题中的信息适用于以下情况：你是 OEM 或独立硬件供应商 (IHV) 开发要使用 Winusb.sys 作为功能驱动程序的设备，并且想要自动加载驱动程序，而无需提供自定义 INF。

- [WinUSB 设备](#winusb-device)
  - [什么是 WinUSB 设备](#what-is-a-winusb-device)
  - [使用 WinUSB 设备安装-box Winusb](#winusb-device-installation-by-using-the-in-box-winusbinf)
    - [关于使用 USBDevice 类：](#about-using-the-usbdevice-class)
  - [如何更改 WinUSB 设备的设备说明](#how-to-change-the-device-description-for-a-winusb-device)
  - [如何配置 WinUSB 设备](#how-to-configure-a-winusb-device)
  - [相关主题](#related-topics)

## <a name="what-is-a-winusb-device"></a>什么是 WinUSB 设备


WinUSB 设备是通用串行总线 (USB) 设备，其固件定义了将兼容 ID 报告为 "WINUSB" 的某些 Microsoft 操作系统 (OS) 功能描述符。

WinUSB 设备的用途是使 Windows 在没有自定义 INF 文件的情况下，将 Winusb.sys 作为设备的函数驱动程序加载。 对于 WinUSB 设备，你无需为设备分发 INF 文件，使最终用户的驱动程序安装过程简单。 相反，如果需要提供自定义 INF，则不应将设备定义为 WinUSB 设备，并指定 INF 中设备的硬件 ID。

Microsoft 提供 Winusb，其中包含 Winusb.sys 作为 USB 设备的设备驱动程序安装时所需的信息。

在 Windows 8 之前，若要将 Winusb.sys 作为函数驱动程序加载，需要提供自定义 INF。 自定义 INF 指定特定于设备的硬件 ID，还包括内置 Winusb 中的部分。 这些部分是实例化服务、复制收件箱二进制文件和注册设备接口 GUID 所必需的，应用程序需要该 GUID 才能查找设备并与之通信。 有关编写自定义 INF 的信息，请参阅 [WinUSB (Winusb.sys) 安装](winusb-installation.md#inf)。

在 Windows 8 中，Winusb 文件已更新，使 Windows 能够自动将 INF 与 WinUSB 设备匹配。

## <a name="winusb-device-installation-by-using-the-in-box-winusbinf"></a>使用 WinUSB 设备安装-box Winusb


在 Windows 8 中，已更新了内置 Winusb 文件。 INF 包含一个 "安装" 部分，该部分引用名为 "USB \\ MS \_ COMP WINUSB" 的兼容 ID \_ 。

```cpp
[Generic.Section.NTamd64]
%USB\MS_COMP_WINUSB.DeviceDesc%=WINUSB,USB\MS_COMP_WINUSB 
```

更新的 INF 还包括一个名为 "USBDevice" 的新安装类。

Microsoft 不提供内置驱动程序的设备可以使用 "USBDevice" 安装程序类。 通常，此类设备不属于明确定义的 USB 类，如音频、蓝牙等，并且需要自定义驱动程序。 如果设备是 WinUSB 设备，则很可能是设备不属于 USB 类。 因此，您的设备必须安装在 "USBDevice" 安装程序类下。 更新后的 Winusb 有助于实现这一要求。

### <a name="about-using-the-usbdevice-class"></a>关于使用 USBDevice 类：

不要对未分类设备使用 "USB" 安装程序类。 此类保留用于安装控制器、集线器和复合设备。 滥用 "USB" 类可能导致重大的可靠性和性能问题。 对于未分类设备，请使用 "USBDevice"。

在 Windows 8 中，若要使用 "USBDevice" 设备类，只需将其添加到 INF 即可：

```cpp
  …
  [Version] 
  Class=USBDevice 
  ClassGuid={88BAE032-5A81-49f0-BC3D-A4FF138216D6}
  …
```

在 Device Manager 中，你将看到一个新的节点 **USB 通用串行总线设备** ，你的设备将显示在该节点下。
<p>在 Windows 7 中，除了上述行以外，还需要在 INF 中创建以下注册表设置：

```cpp
  ;---------- Add Registry Section ----------
  [USBDeviceClassReg] 
  HKR,,,,"Universal Serial Bus devices"
  HKR,,NoInstallClass,,1
  HKR,,SilentInstall,,1 
  HKR,,IconPath,%REG_MULTI_SZ%,"%systemroot%\system32\setupapi.dll,-20"
```

在 Device Manager 中，你的设备将显示在 " **USB 通用串行总线设备**" 下。 不过，设备类说明派生于 INF 中指定的注册表设置。

请注意，"USBDevice" 类不限于 WinUSB。 如果你的设备有自定义驱动程序，则可以在自定义 INF 中使用 "USBDevice" 安装程序类。

在设备枚举过程中，USB 驱动程序堆栈从设备读取兼容 ID。 如果兼容 ID 是 "WINUSB"，则 Windows 将使用它作为设备标识符，并在更新的内置 Winusb 中找到匹配项，然后加载 Winusb.sys 作为设备的函数驱动程序。

此映像适用于定义为 WinUSB 设备并作为 Winusb.sys 加载到设备的函数驱动程序的单个 interface MUTT 设备。

![显示 winusb 设备的设备管理器。](images/winusb-device.png)

对于早于 Windows 8 的 Windows 版本，更新的 Winusb 通过 **Windows 更新** 提供。 如果你的计算机配置为自动获取驱动程序更新，则将使用新的 INF 包在无需任何用户干预的情况下安装 WinUSB 驱动程序。

## <a name="how-to-change-the-device-description-for-a-winusb-device"></a>如何更改 WinUSB 设备的设备说明


对于 WinUSB 设备，Device Manager 显示 "WinUsb 设备" 作为设备描述。 该字符串是从 Winusb 派生的。 如果有多个 WinUSB 设备，则所有设备会获得相同的设备说明。

为了唯一标识和区分 Device Manager 设备，Windows 8 在设备类上提供了一个新的属性，该属性指示系统将设备 (在其 **iProduct** 字符串描述符中报告的设备说明的优先级，) INF 中的说明。 Windows 8 中定义的 "USBDevice" 类设置此属性。 换句话说，当设备安装在 "USBDevice" 类下时，系统将在设备上查询设备说明，并将 Device Manager 字符串设置为在查询中检索到的任何内容。 在这种情况下，将忽略 INF 中提供的设备说明。 请注意上图中的设备说明字符串： "MUTT"。 此字符串由 USB 设备在其产品字符串描述符中提供。

在早期版本的 Windows 上不支持新的类属性。 若要在较早版本的 Windows 上拥有自定义的设备说明，则必须编写自己的自定义 INF。

## <a name="how-to-configure-a-winusb-device"></a>如何配置 WinUSB 设备


若要将 USB 设备标识为 WinUSB 设备，设备固件必须具有 Microsoft OS 描述符。 有关描述符的信息，请参阅此处所述的规范： [MICROSOFT OS 描述符](microsoft-defined-usb-descriptors.md)。

**支持扩展的功能描述符**

为了使 USB 驱动程序堆栈知道设备支持扩展功能描述符，设备必须定义存储在字符串索引0xEE 的 OS 字符串描述符。 在枚举过程中，驱动程序堆栈会查询字符串说明符。 如果描述符存在，则驱动程序堆栈假设设备包含一个或多个 OS 功能描述符和检索这些功能描述符所需的数据。

检索到的字符串描述符具有 **bMS \_ VendorCode** 字段值。 值指示 USB 驱动程序堆栈必须用于检索扩展功能描述符的供应商代码。

有关如何定义 OS 字符串描述符的信息，请参阅此处所述规范中的 "OS 字符串描述符"： [MICROSOFT OS 描述符](microsoft-defined-usb-descriptors.md)。

**设置兼容 ID**

一种扩展的兼容 ID OS 功能描述符，它需要与内置 Winusb 相匹配，并加载 WinUSB 驱动程序模块。

扩展兼容 ID OS 功能描述符包含一个标头部分，后跟一个或多个函数部分，具体取决于设备是复合设备还是非复合设备。 标头部分指定整个描述符的长度、函数部分的数目和版本号。 对于非复合设备，标头后跟一个与设备的唯一接口相关联的函数部分。 该部分的 **compatibleID** 字段必须将 "WINUSB" 指定为字段值。 对于复合设备，有多个函数部分。 每个函数部分的 **compatibleID** 字段必须指定 "WINUSB"。

**注册设备接口 GUID**

注册其设备接口 GUID 所需的扩展属性 OS 功能描述符。 GUID 是从应用程序或服务中查找设备、配置设备和执行 i/o 操作所必需的。

在以前版本的 Windows 中，设备接口 GUID 注册是通过自定义 INF 来完成的。 从 Windows 8 开始，设备应使用扩展属性 OS 功能描述符报告接口 GUID。

扩展属性 OS 功能描述符包含后面跟有一个或多个自定义属性部分的标头部分。 标头部分描述了整个扩展属性说明符，其中包括其总长度、版本号和自定义属性节的数目。 若要注册设备接口 GUID，请添加自定义属性部分，将 **bPropertyName** 字段设置为 "DeviceInterfaceGUID"，将 **wPropertyNameLength** 设置为40字节。 使用 GUID 生成器生成唯一的设备接口 GUID，并将 " **bPropertyData** " 字段设置为该 guid，例如 "{8FE6D4D7-49DD-41E7-9486-49AFC6BFE475}"。 请注意，GUID 指定为 Unicode 字符串，字符串长度为78字节 (包括 null 终止符) 。

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
<td>78字节</td>
<td><p>7B 00 38 00 46 00 45 00 36 00 44 00 34 00 44 00 37 00 2D 00 34 00 39 00 00 44 00 2D 00 34 00 31 00 45 00 37 00 2D 00 39 00 34 00 38 00 36 00 2D 00 34 00 39 00 41 00 46 00 43 00 36 00 42 00 46 00 45 00 34 00 37 00 35 00 7D 00 00 00</p></td>
<td>属性值为 {8FE6D4D7-49DD-41E7-9486-49AFC6BFE475}。</td>
</tr>
</tbody>
</table>

 

在设备枚举过程中，USB 驱动程序堆栈会从扩展属性 OS 功能描述符检索 **DeviceInterfaceGUID** 值，并在设备的硬件密钥中注册设备。 应用程序可以使用 **SetupDiXxx** api 检索该值 (参阅 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey)) 。 有关详细信息，请参阅 [如何使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

**启用或禁用 WinUSB 电源管理功能**

在 Windows 8 之前，若要配置 WinUSB 的电源管理功能，必须在 HW 中写入注册表项值 **。** 自定义 INF 的 AddReg 部分。

在 Windows 8 中，您可以在 "设备" 中指定电源设置。 可以通过用于在 WinUSB 中启用或禁用功能的扩展属性 OS 功能描述符来报告值。 可以配置以下两个功能：选择性挂起和系统唤醒。 选择性挂起允许设备进入空闲状态时进入低功耗状态。 系统唤醒是指当系统处于低功耗状态时，设备能够唤醒系统的能力。

有关 WinUSB 电源管理功能的信息，请参阅 [WinUSB 电源管理](winusb-power-management.md)。

| 属性名称            | 说明                                                                                                                                                                                                                                                                                                                               |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DeviceIdleEnabled        | 此值设置为1，表示设备在空闲 (选择性挂起) 时可关闭电源。                                                                                                                                                                                                                                          |
| DefaultIdleState         | 此值设置为1，表示在默认情况下，设备可处于挂起状态。                                                                                                                                                                                                                                                 |
| DefaultIdleTimeout       | 此值设置为5000（以毫秒为单位），以表示确定设备处于空闲状态之前等待的时间（以毫秒为单位）。                                                                                                                                                                                                |
| UserSetDeviceIdleEnabled | 此值设置为1，以允许用户控制设备启用或禁用 USB 选择性挂起的能力。 选中此复选框后 **，计算机可以关闭此设备以节省** 设备 **电源管理** 属性页上的电源，用户可以选中或取消选中该复选框以启用或禁用 USB 选择性挂起。 |
| SystemWakeEnabled        | 此值设置为1，以允许用户控制设备从低功耗状态唤醒系统的能力。 启用后，" **允许此设备唤醒计算机** " 复选框将出现在 "设备电源管理" 属性页中。 用户可以选中或取消选中该复选框，以启用或禁用 USB 系统唤醒。         |

 

例如，若要在设备上启用选择性挂起，请添加自定义属性部分，将 **bPropertyName** 字段设置为 Unicode 字符串 "DeviceIdleEnabled"，将 **wPropertyNameLength** 设置为36字节。 将 **bPropertyData** 字段设置为 "0x00000001"。 属性值存储为小字节序 32 位整数。

在枚举过程中，USB 驱动程序堆栈读取扩展属性功能描述符并在此项下创建注册表项：

**HKEY \_本地 \_ 计算机** \\ **系统** \\ **CurrentControlSet** \\ **枚举** \\ **USB** \\ **_&lt; 设备标识符 &gt;_ *_\\_* _&lt; 实例标识符 &gt;_ *_\\_* 设备参数**

此图像显示 WinUSB 设备的示例设置。

![winusb 设备的注册表设置](images/winusb-device-reg.png)

有关其他示例，请参阅 [MICROSOFT OS 描述符](microsoft-defined-usb-descriptors.md)上的规范。

## <a name="related-topics"></a>相关主题
[Microsoft 定义的 USB 描述符](microsoft-defined-usb-descriptors.md)