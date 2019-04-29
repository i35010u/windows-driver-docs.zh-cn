---
Description: Oem 必须设置几个注册表值，以确保其设备枚举与正确的元数据时连接到计算机。
title: 适用于功能控制器驱动程序的 USB 注册表设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18bf5bde14e3a9fc21d2ae1842ec19281e81a099
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377207"
---
# <a name="usb-registry-settings-for-a-function-controller-driver"></a>适用于功能控制器驱动程序的 USB 注册表设置


**摘要**

-   Oem 必须设置为定义 USB 描述符的注册表项。

**适用于：**

-   Windows 10

**上次更新时间：**

-   2015 年 11 月

Oem 必须设置几个注册表值，以确保其设备枚举与正确的元数据时连接到计算机。 这些值指定为设备和配置描述符[USB 设备端驱动程序在 Windows 中的](usb-device-side-drivers-in-windows.md)。 创建并将包含其自己的接口的 Oem 必须及其接口来加载和使用的顺序中设置其他注册表值。

设备端 USB 驱动程序相关的注册表项下是：

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control**\\**USBFN**

本主题介绍设置上述的密钥和定义设备、 配置和设备的接口描述符的子项。

## <a name="usbfn-registry-key"></a>USBFN 注册表项


下面是 USB 设备的配置信息：

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control**\\**USBFN**

下表介绍 Oem 可以修改在此项下的子项。 在以下各节提供有关支持的每个子项值的详细信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>子项</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>备用项</strong></td>
<td>此子项包含其他描述具有一个或多个替代设置的接口：
<p><strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;strong&gt;USBFN</strong>&lt;strong&gt;Alternates</strong></p></td>
</tr>
<tr class="even">
<td><strong>关联</strong></td>
<td>此子项定义接口关联描述符 (Iad)。 每个 IAD 允许多个接口分组到单个函数。 每个子项表示不同 IAD 和 Oem 可以修改这些子项的值。
<p><strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;strong&gt;USBFN</strong>&lt;strong&gt;Associations</strong></p></td>
</tr>
<tr class="odd">
<td><strong>默认</strong></td>
<td>此子项包含用于描述特定于设备的设置，例如 VID 和 PID 的默认值。 这是其值被重写父项中的一个 Microsoft 拥有的子项：
<p><strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;strong&gt;USBFN</strong></p></td>
</tr>
<tr class="even">
<td><strong>配置</strong></td>
<td>此子项包含其他包含 USB 枚举过程中使用的配置描述符值。 例如，标准测试配置可能存在下<strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;强&gt;USBFN</strong>&lt;强&gt;配置</strong>&lt;强&gt;TestConfigClassic</strong>。</td>
</tr>
<tr class="odd">
<td><strong>Configurations\Default</strong></td>
<td>此子项包含默认配置的值。 默认配置中的接口添加之前的当前配置存在何时<strong>IncludeDefaultCfg</strong>下设置值<strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;强&gt;USBFN</strong>密钥。</td>
</tr>
<tr class="even">
<td><strong>Interfaces</strong></td>
<td>此子项包含其他描述特定接口描述符。 例如，IP over USB 配置可能驻留在名为一个子项下<strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;强&gt;USBFN</strong>&lt;强&gt;接口</strong>&lt;强&gt;IpOverUsb</strong>。 此接口的名称是子项的由什么决定类驱动程序的硬件 ID。 在 IP over USB 示例，是加载 PDO _HID <strong>USBFN\IpOverUsb</strong>。</td>
</tr>
</tbody>
</table>

 

下表介绍在中，Oem 可以修改的值**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\ **USBFN**密钥。 此表中未列出的值假定由 Microsoft 根据定义的默认值**HKEY\_本地\_机\\系统\\CurrentControlSet\\控件** \\ **USBFN**\\**默认**。

必须设置所有 Oem **idVendor**， **idProduct**， **ManufacturerString**，以及**ProductString**值。 创建并添加其自身接口还必须设置的 Oem **CurrentConfiguration**下的子项的名称**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\**USBFN**\\**配置**中包括其接口中**InterfaceList**。

| ReplTest1                    | 在任务栏的搜索框中键入       | 所有者 | 描述                                                                                                                                                                                                                                                                                                                |
|--------------------------|------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **idVendor**             | REG\_DWORD | OEM   | 在枚举期间发送到主机的设备描述符供应商标识符。                                                                                                                                                                                                                               |
| **idProduct**            | REG\_DWORD | OEM   | 在枚举期间发送到主机的设备描述符产品标识符。                                                                                                                                                                                                                              |
| **ManufacturerString**   | REG\_SZ    | OEM   | 发送到主机来标识设备的制造商制造商字符串。                                                                                                                                                                                                                               |
| **ProductString**        | REG\_SZ    | OEM   | 一个字符串，描述作为产品的设备。 默认值为 Windows 10 移动版设备。 此值用作连接的计算机的用户界面中的设备的显示名称。 Oem 应确保此值与 DeviceTargetingInfo 子项下的 PhoneModelName 值的值相匹配。 |
| **iSerialNumber**        | REG\_DWORD | OEM   | 此值设置为 0，如果设备没有序列号。 如果此值为非零，或者不存在，则序列号会生成唯一每台设备。                                                                                                                                            |
| **CurrentConfiguration** | REG\_SZ    | OEM   | 此字符串必须对应于配置子项的名称。 此字符串确定要用于生成 USB 设备枚举配置描述符的配置。                                                                                                                                       |

 

## <a name="usbfnconfigurations-registry-key"></a>USBFN\\配置注册表项


下表介绍 Oem 可以修改的子项下的值**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\ **USBFN**\\**配置**。 每个子项表示不同的 USB 配置。 如果 OEM 想要创建自己的界面，OEM 必须定义新的配置，其中包含要使用的接口。 若要执行此操作，创建下的子项**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\**USBFN**\\**配置**，它使用配置的名称，并填充此表中的值的子项。 此外，对于 USB 驱动程序，以使用新的配置中， **CurrentConfiguration** （前面的表中所述） 的值必须设置为在配置的子项的名称。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>在任务栏的搜索框中键入</th>
<th>所有者</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>InterfaceList</strong></td>
<td>REG_MULTI_SZ</td>
<td>OEM 或 Microsoft</td>
<td><p>包含对应于接口子项下的接口名称的列表<strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;强&gt;USBFN</strong>&lt;强&gt;接口</strong>，在所定义的 IAD 关联<strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;强&gt;USBFN</strong>&lt;强&gt;关联</strong>，以及下定义的备用接口<strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;强&gt;USBFN</strong>&lt;强&gt;交替</strong>。 这些密钥确定用于描述复合配置描述符的接口。</p>
<p>如果<strong>IncludeDefaultCfg</strong>值下<strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;强&gt;USBFN</strong>键设置为 1，此列表追加到 Microsoft 拥有默认接口列表创建的设备将使用要枚举的完整接口列表。</p></td>
</tr>
<tr class="even">
<td><strong>MSOSCompatIdDescriptor</strong></td>
<td>REG_BINARY</td>
<td>OEM 或 Microsoft</td>
<td><p>可选。 定义扩展兼容 ID 操作系统功能描述符的配置。 如果<strong>IncludeDefaultCfg</strong>值下<strong>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control</strong>&lt;强&gt;USBFN</strong>键设置为 1，函数在此描述符将追加到函数和默认配置中的接口。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usbfninterfaces-registry-key"></a>USBFN\\接口注册表项


下表介绍 Oem 可以修改的子项下的值**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\ **USBFN**\\**接口**。

每个子项表示不同的 USB 接口。 若要定义一个接口，创建下的子项**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\ **USBFN**\\**接口**使用接口的名称，并使用下表中的值填充它。 此外，接口才会包含如果接口的一部分**InterfaceList**的**CurrentConfiguration**。

| ReplTest1                              | 在任务栏的搜索框中键入        | 所有者            | 描述                                                                                                                                                                                                                                                                                                  |
|------------------------------------|-------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceDescriptor**            | REG\_二进制 | OEM 或 Microsoft | 将 USB 枚举过程中发送到主机接口描述符的二进制表示形式。 **BInterfaceNumber**并**iInterface**值自动填充通过 USB 函数堆栈编译一个完整的配置描述符，以避免与其他接口冲突后描述符。 |
| **InterfaceGUID**                  | REG\_SZ     | OEM 或 Microsoft | 用于唯一标识总线上的接口的 GUID。                                                                                                                                                                                                                                                     |
| **InterfaceNumber**                | REG\_DWORD  | OEM 或 Microsoft | 可选。 此值用于将固定的接口分配到一个函数。 接口数字 0 1f 之间保留的旧版功能、 20 3F 仅供 Microsoft 和 40 5F 保留供 Oem。                                                                                           |
| **MSOSExtendedPropertyDescriptor** | REG\_二进制 | OEM 或 Microsoft | 可选。 定义接口的扩展属性操作系统功能描述符。                                                                                                                                                                                                                              |

 

## <a name="usbfnalternates-registry-key"></a>USBFN\\备用项注册表项


在备用项的子项用于定义有一个或多个备用接口的单一界面。 下表介绍 Oem 可以修改的子项下的值**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\ **USBFN**\\**交替**。

每个子项表示不同的接口。 若要使用备用设置定义一个接口，创建下的子项**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\ **USBFN**\\**交替**通过使用接口的名称，并使用下表中的值填充它。

| ReplTest1                              | 在任务栏的搜索框中键入           | 所有者            | 描述                                                                                                                                                                                                                                                                                                                                                        |
|------------------------------------|----------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceList**                  | REG\_MULTI\_SZ | OEM 或 Microsoft | 两个对应于在定义的接口的多个接口名称的列表**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\**USBFN**\\**接口**。 该注册表项共同定义替代设置的接口。 第一个接口对应于第二个接口对应替代设置的备用设置 0，1，依此类推。 |
| **InterfaceNumber**                | REG\_DWORD     | OEM 或 Microsoft | 可选。 此值用于将固定的接口分配到一个函数。 接口数字 0 1f 之间保留的旧版功能、 20 3F 仅供 Microsoft 和 40 5F 保留供 Oem。                                                                                                                                                 |
| **MSOSExtendedPropertyDescriptor** | REG\_二进制    | OEM 或 Microsoft | 可选。 定义接口的扩展属性操作系统功能描述符。                                                                                                                                                                                                                                                                                    |

 

## <a name="usbfnassociations-registry-key"></a>USBFN\\关联注册表项


Oem 可以通过定义接口关联描述符 (Iad) 指定的关联。 每个 IAD 允许多个接口分组到单个函数。 下表介绍 Oem 可以修改的子项下的值**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\ **USBFN**\\**关联**。

每个子项表示不同 IAD。 若要定义的关联，创建下的子项**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制**\\ **USBFN**\\**关联**通过使用 IAD，名称并使用下表中的值填充它。

| ReplTest1                              | 在任务栏的搜索框中键入           | 所有者            | 描述                                                                                                                                                                                                                 |
|------------------------------------|----------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceList**                  | REG\_MULTI\_SZ | OEM 或 Microsoft | 接口或与 USB 函数相关联的备用接口的列表。 如果列表的大小，小于 2 函数驱动程序堆栈将无法加载。 其他函数或接口继续进行加载。 |
| **bFunctionClass**                 | REG\_DWORD     | OEM 或 Microsoft | 该函数的类代码设置为 02。                                                                                                                                                                                  |
| **bFunctionSubClass**              | REG\_DWORD     | OEM 或 Microsoft | 该函数，则设置为 0 d 子类代码。                                                                                                                                                                               |
| **bFunctionProtocol**              | REG\_DWORD     |                  | 该函数，将设置为 01 协议代码。                                                                                                                                                                               |
| **MSOSExtendedPropertyDescriptor** | REG\_二进制    | OEM 或 Microsoft | 可选。 定义接口的扩展属性操作系统功能描述符。                                                                                                                                             |

 

**用例：启用 MirrorLink**

MirrorLink 是一种互操作性标准，允许移动设备和汽车位系统之间的集成。 设备必须公开到 MirrorLink 客户端的 USB CDC NCM 界面。 为通信设备类 (CDC) 的设备，它需要通过使用接口关联描述符 (IAD) 和/或 CDC 函数联合描述符来描述数据接口。

若要启用 MirrorLink 连接，可以在 Windows 10 移动版设备，OEM 必须进行这些更改，以公开 IAD。

-   通过设置注册表值在上表中所示使用接口关联描述符 (IAD) 创建的通信和数据接口的关联。
-   除了注册表设置中，将此注册表值设置为非零值。

    | ReplTest1          | 在任务栏的搜索框中键入       | 所有者            | 描述                                                                                                                     |
    |----------------|------------|------------------|---------------------------------------------------------------------------------------------------------------------------------|
    | **MirrorLink** | REG\_DWORD | OEM 或 Microsoft | 一个非零值指示该接口支持 MirrorLink。 USB 函数堆栈不会不会出现延迟 MirrorLink USB 命令。 |

     

-   特定于类的描述符可以包含在注册表中定义的接口描述符集合。 大小字段必须在这些描述符设置，以便该 USB 函数驱动程序堆栈可以准确地分析它们。

或者，CDC 函数联合描述符可以也定义为类特定的接口描述符;但是，联合描述符指定的接口数是静态的是不是通过 USB 函数驱动程序堆栈，分配和 Union 描述符是否存在不会导致它将与单个子 PDO 关联所描述的接口。 需要为该关联 IAD。

## <a name="related-topics"></a>相关主题
[在 Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)  
[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)  



