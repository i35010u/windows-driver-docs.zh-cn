---
description: Oem 必须设置多个注册表值，以确保在连接到计算机时，其设备使用正确的元数据进行枚举。
title: 适用于功能控制器驱动程序的 USB 注册表设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f0cbf20d7f72c49582dcf7101969d5b2e2de515
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968604"
---
# <a name="usb-registry-settings-for-a-function-controller-driver"></a>适用于功能控制器驱动程序的 USB 注册表设置


**摘要**

-   要定义 USB 描述符，Oem 必须设置的注册表项。

**适用于：**

-   Windows 10

**上次更新时间：**

-   2015 年 11 月

Oem 必须设置多个注册表值，以确保在连接到计算机时，其设备使用正确的元数据进行枚举。 这些值指定 [Windows 中 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)的设备和配置描述符。 创建并包含其自己的接口的 Oem 必须设置其他注册表值，以便加载和使用其接口。

与设备端 USB 驱动程序相关的注册表项如下：

**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ USBFN**

本主题介绍用于定义设备、配置和设备接口描述符的前面的密钥和子项的设置。

## <a name="usbfn-registry-key"></a>USBFN 注册表项


USB 设备的配置信息如下所示：

**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ USBFN**

下表描述了其子项。 Oem 可以修改其中的某些部分。 以下各节提供了有关每个子项支持的值的详细信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>子项</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>备用项</strong></td>
<td>此子项包含其他子项，用于描述具有一个或多个备用设置的接口。</td>
</tr>
<tr class="even">
<td><strong>相关性</strong></td>
<td>此子项定义 (IADs) 的接口关联描述符。 每个 IAD 允许将多个接口分组为一个函数。 每个子项表示不同的 IAD，Oem 可以修改这些子项的值。</td>
</tr>
<tr class="odd">
<td><strong>默认</strong></td>
<td>此子项包含用于描述设备特定设置（如 VID 和 PID）的默认值。 这是一个 Microsoft 拥有的子项，其值被父键中的值覆盖。</td>
</tr>
<tr class="even">
<td><strong>配置</strong></td>
<td>此子项包含其他子项，其中包含在 USB 枚举期间使用的配置描述符值。 例如， <strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\configurations\testconfig</strong>下可能存在标准测试配置。</td>
</tr>
<tr class="odd">
<td><strong>Configurations\Default</strong></td>
<td>这是一个 Microsoft 拥有的子项。 它包含默认配置的值。 当在 HKEY_LOCAL_MACHINE \System\CurrentControlSet\Control\USBFN 键下将 <strong>IncludeDefaultCfg</strong> 值设置为1时，将在当前配置出现之前添加默认配置中的接口 <strong> 。</td>
</tr>
<tr class="even">
<td><strong>接口</strong></td>
<td>此子项包含其他描述特定接口描述符的子项。 例如，IP over USB 接口可能驻留在 <strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\interfaces\ipoverusb</strong>下。 接口子项的名称还用作加载 USBFn 类驱动程序的 USBFN 子设备的硬件 ID。 在 IP over USB 示例中，USBFN 子设备的硬件 ID 将为 <strong>USBFN\IpOverUsb</strong>。</td>
</tr>
</tbody>
</table>

 

下表描述了 Oem 可在 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Control \\ USBFN** 项中定义的值。 未在此项中定义的值假设 Microsoft 在 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ 默认**值下定义的默认值。

所有 Oem 必须设置 **idVendor**、 **idProduct**、 **ManufacturerString**和 **ProductString** 值。 创建和添加自己的接口的 Oem 还必须将 **CurrentConfiguration** 设置为 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ 配置** 中的子项的名称，这些配置包含其在 **InterfaceList**中的接口。

| “值” | 类型 | 所有者 | 说明|
|--|--|--|--|
| **IncludeDefaultCfg** | REG \_ DWORD | OEM | 如果 Oem 要包括默认配置的接口（如 IpOverUsb 或 MTP），则设置为1。 |
| **idVendor** | REG \_ DWORD | OEM | 枚举过程中发送到主机的设备描述符的供应商标识符。 |
| **idProduct** | REG \_ DWORD | OEM | 枚举过程中发送到主机的设备描述符的产品标识符。 |
| **ManufacturerString** | REG\_SZ| OEM | 发送到主机以标识设备制造商的制造商字符串。 |
| **ProductString** | REG\_SZ| OEM | 将设备描述为产品的字符串。 默认值为 Windows 10 移动版设备。 此值用作连接计算机的用户界面中设备的显示名称。 Oem 应确保此值与 DeviceTargetingInfo 子项下的 PhoneModelName 值的值匹配。 |
| **iSerialNumber**| REG \_ DWORD | OEM | 如果此值设置为0，则设备不具有序列号。 如果此值不是零或不存在，则每个设备的序列号都是唯一的。 |
| **CurrentConfiguration** | REG\_SZ | OEM | 此字符串必须与配置子项的名称相对应。 此字符串确定要使用哪个配置来为 USB 设备枚举构建配置描述符。 |

 

## <a name="usbfnconfigurations-registry-key"></a>USBFN \\ 配置注册表项


下表描述了 Oem 可为 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ 配置**下的子项定义的值。 每个子项表示不同的 USB 配置。 如果 OEM 要创建自己的接口，则 OEM 必须定义一个新配置，其中包含要使用的接口。 为此，请在 " **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ ** " 下创建一个子键，其中使用配置的名称，并使用此表中的值填充该子项。 此外，若要使 USB 驱动程序使用新配置，) 必须将 **CurrentConfiguration** (值设置为配置子项的名称。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>类型</th>
<th>所有者</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>InterfaceList</strong></td>
<td>REG_MULTI_SZ</td>
<td>OEM 或 Microsoft</td>
<td><p>包含与 <strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\interfaces</strong>下的接口子项、在 <strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\associations</strong>下定义的 IAD 关联以及在 <strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\alternates</strong>下定义的备用接口相对应的接口名称列表。 这些键确定用于描述复合配置描述符的接口。</p>
<p>如果<strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn</strong>键下的<strong>IncludeDefaultCfg</strong>值设置为1，则会将此列表追加到 Microsoft 拥有的默认接口列表，以创建设备将用于枚举的完整接口列表。</p></td>
</tr>
<tr class="even">
<td><strong>MSOSCompatIdDescriptor</strong></td>
<td>REG_BINARY</td>
<td>OEM 或 Microsoft</td>
<td><p>可选。 为配置定义扩展的兼容 ID OS 功能描述符。 如果<strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn</strong>键下的<strong>IncludeDefaultCfg</strong>值设置为1，则此描述符中的函数将追加到默认配置中的函数和接口。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usbfninterfaces-registry-key"></a>USBFN \\ 接口注册表项


下表描述了 Oem 可为 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ 接口**下的子项修改的值。

每个子项表示不同的 USB 接口。 若要定义接口，请在 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ ** interface 下使用接口的名称创建一个子键，并使用下表中的值填充该接口。 此外，如果接口是**CurrentConfiguration**的**InterfaceList**的一部分，则仅包含接口。

| “值”                              | 类型        | 所有者            | 说明                                                                                                                                                                                                                                                                                                  |
|------------------------------------|-------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceDescriptor**            | 注册表 \_ 二进制 | OEM 或 Microsoft | 要在 USB 枚举过程中发送到主机的接口描述符的二进制表示形式。 **BInterfaceNumber**和**iInterface**值将在编译完整配置描述符后由 USB 函数堆栈自动填充，以避免与其他接口描述符冲突。 |
| **InterfaceGUID**                  | REG\_SZ     | OEM 或 Microsoft | 一个 GUID，用于唯一标识总线上的接口。                                                                                                                                                                                                                                                     |
| **InterfaceNumber**                | REG \_ DWORD  | OEM 或 Microsoft | 可选。 此值用于将固定的接口号分配给函数。 接口号 0-1F 是为传统函数保留的，20-3F 是为 Microsoft 保留的，40-5F 保留供 Oem 使用。                                                                                           |
| **MSOSExtendedPropertyDescriptor** | 注册表 \_ 二进制 | OEM 或 Microsoft | 可选。 定义接口的扩展属性 OS 功能描述符。                                                                                                                                                                                                                              |

 

## <a name="usbfnalternates-registry-key"></a>USBFN \\ 备用注册表项


替代子项用于定义具有一个或多个备用接口的单个接口。 下表描述了 Oem 可为 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ 备用**项下的子项修改的值。

每个子项表示不同的接口。 若要使用备用设置定义接口，请在 " **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ ** " 下使用接口的名称创建一个子键，并使用下表中的值对其进行填充。

| “值”                              | 类型           | 所有者            | 说明                                                                                                                                                                                                                                                                                                                                                        |
|------------------------------------|----------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceList**                  | REG \_ 多 \_ SZ | OEM 或 Microsoft | 与 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ interface**下定义的接口对应的两个接口名称的列表。 该密钥共同定义具有替代设置的接口。 第一个接口对应于备用设置0，第二个接口对应于替代设置1，依此类推。 |
| **InterfaceNumber**                | REG \_ DWORD     | OEM 或 Microsoft | 可选。 此值用于将固定的接口号分配给函数。 接口号 0-1F 是为传统函数保留的，20-3F 是为 Microsoft 保留的，40-5F 保留供 Oem 使用。                                                                                                                                                 |
| **MSOSExtendedPropertyDescriptor** | 注册表 \_ 二进制    | OEM 或 Microsoft | 可选。 定义接口的扩展属性 OS 功能描述符。                                                                                                                                                                                                                                                                                    |

 

## <a name="usbfnassociations-registry-key"></a>USBFN \\ 关联注册表项


Oem 可以通过定义 (IADs) 的接口关联描述符来指定关联。 每个 IAD 允许将多个接口分组为一个函数。 下表描述了 Oem 可为 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ association**下的子项修改的值。

每个子项表示不同的 IAD。 若要定义关联，请使用 IAD 的名称在 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ USBFN \\ association** 下创建一个子项，并使用下表中的值填充该关联。

| “值”                              | 类型           | 所有者            | 说明                                                                                                                                                                                                                 |
|------------------------------------|----------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceList**                  | REG \_ 多 \_ SZ | OEM 或 Microsoft | 与 USB 函数关联的接口或备用接口的列表。 如果列表的大小小于2，则函数驱动程序堆栈无法加载。 其他函数或接口将继续加载。 |
| **bFunctionClass**                 | REG \_ DWORD     | OEM 或 Microsoft | 函数的类代码，设置为02。                                                                                                                                                                                  |
| **bFunctionSubClass**              | REG \_ DWORD     | OEM 或 Microsoft | 函数的子类代码，设置为0d。                                                                                                                                                                               |
| **bFunctionProtocol**              | REG \_ DWORD     |                  | 函数的协议代码，设置为01。                                                                                                                                                                               |
| **MSOSExtendedPropertyDescriptor** | 注册表 \_ 二进制    | OEM 或 Microsoft | 可选。 定义接口的扩展属性 OS 功能描述符。                                                                                                                                             |

 

**用例：启用 MirrorLink**

MirrorLink 是一种互操作性标准，允许在移动设备和汽车 infotainment 系统之间集成。 设备必须向 MirrorLink 客户端公开一个 USB CDC NCM 接口。 作为通信设备类 (CDC) 设备，需要使用接口关联描述符 (IAD) 和/或 CDC 函数联合描述符来描述数据接口。

若要在 Windows 10 移动设备上启用 MirrorLink 连接，OEM 必须进行这些更改才能公开 IAD。

-   通过设置上表中显示的注册表值，通过使用接口关联描述符 (IAD) 为通信和数据接口创建关联。
-   除了注册表设置，将此注册表值设置为非零值。

    | “值”          | 类型       | 所有者            | 说明                                                                                                                     |
    |----------------|------------|------------------|---------------------------------------------------------------------------------------------------------------------------------|
    | **MirrorLink** | REG \_ DWORD | OEM 或 Microsoft | 非零值指示接口支持 MirrorLink。 USB 函数堆栈不会延迟 MirrorLink USB 命令。 |

     

-   类特定的描述符可以包含在注册表中定义的接口描述符集中。 必须在这些描述符中设置大小字段，以使 USB 函数驱动程序堆栈能够准确分析它们。

此外，也可以将 CDC 函数联合描述符定义为类特定的接口描述符;但是，由联合描述符指定的接口号是静态的，不会由 USB 函数驱动程序堆栈指定，并且联合描述符不会导致其所描述的接口与单个子 PDO 关联。 该关联需要 IAD。

## <a name="related-topics"></a>相关主题
[Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)  
[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)  



