---
title: 特殊大小写映射
description: 特殊大小写映射
ms.assetid: 1691e0e5-7b05-40e1-8747-40926f2eba9c
keywords:
- 游戏杆 WDK HID，轴
- 虚拟游戏杆驱动程序 WDK HID，轴
- VJoyD WDK HID 轴
- 轴 WDK 游戏杆
- 特殊大小写映射 WDK 游戏杆
- 大小写映射 WDK 游戏杆
- Z 轴大小写映射 WDK 游戏杆
- 汽车控制器大小写映射 WDK 游戏杆
- 映射轴
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: efa2a676b2a220e56de1dc74c013060b6dea8e8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384366"
---
# <a name="special-case-mappings"></a>特殊大小写映射





由于复杂性和各种输入设备立即可用，可以为所有类型的设备不使用任何单个组映射。 DirectInput 支持本节中介绍的两种特殊情况。

### <a name="special-case-mapping-for-z-axes"></a>Z 轴的特殊大小写映射

在极少数的情况下，z 轴所述 HID 是所需的 WinMM 映射，有两个可用的重写。 如果设备是六度自由设备，则将设置类型和子类型重写 (的参考资料中所述**DIJOYTYPEINFO**) 到 DI8DEVTYPE\_1STPERSON 和 DI8DEVTYPE1STPERSON\_SIXDOF分别将调用以下替代映射：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WinMM Axis</th>
<th>DirectInput 分配</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>Y</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>Z</p></td>
<td><p>GUID_ZAxis</p></td>
</tr>
<tr class="even">
<td><p>R</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="odd">
<td><p>U</p></td>
<td><p>GUID_RyAxis</p></td>
</tr>
<tr class="even">
<td><p>V</p></td>
<td><p>GUID_RxAxis</p></td>
</tr>
</tbody>
</table>



如果设备不是六度自由设备，但仍需要 z 轴来描述通过 DirectInput，应该设置类型重写为包括 JOYTYPE\_INFOZISZ。 此类型重写导致 DirectInput，若要还原到 DirectX 7.0 映射。

默认映射，设备将通过 HID 不具有更改除该 GUID\_滑块轴不再替换为 GUID\_ZAxis SetDataFormat 方法匹配。 因为 HID 轴在更完全比 WinMM 轴所述的本质上是，默认值应在大多数情况下工作。 在极少数情况下，滑块轴 （通常被限制为使用） 已被描述为 HID\_使用情况\_页面\_泛型、 HID\_用法\_Z 因为轴将使用 WinMM z 轴的方式相同。 若要确保此类设备可以一致地使用该设备，重写标志 JOYTYPE\_INFOZISSLIDER 可用。

### <a name="special-case-mappings-for-car-controllers"></a>汽车控制器特殊大小写映射

所需的声明两个以上轴的汽车控制器特殊大小写映射的另一组。 遗憾的是，是此区域中行业内的一些一致性。 目前有三种常见方式来表示单独加速器和刹车踏板。 DirectInput 尝试检测汽车控制器使用与逻辑类似于下面的伪代码中所示的方法：

```cpp
    if( has_r and has_Z )
        use mappings:
        X => GUID_XAxis
        Z => GUID_YAxis
        R => GUID_RzAxis
    else if( has_r )
        use mappings:
        X => GUID_XAxis
        Y => GUID_YAxis
        R => GUID_RzAxis
    else if( has_z )
        use mappings:
        X => GUID_XAxis
        Y => GUID_RzAxis
        Z => GUID_YAxis
    else
        use default mappings.

   // If the device declares any other axes, they are mapped to sliders.
```

前面的踏板映射相同的方式报告给应用程序的所有三种已知类型中的逻辑结果。 如果默认映射会失败，则可以设置用于选择应使用哪种类型的映射的替代标志。 重写标志 JOYTYPE\_INFOYYPEDALS、 JOYTYPE\_INFOZYPEDALS、 JOYTYPE\_INFOYRPEDALS 和 JOYTYPE\_INFOZRPEDALS 其他位置在本文档中所述。

如同 WinMM，汽车控制器需要特殊处理映射正在使用通过 HID 数据路径时。 在此情况下，如下所示 WinMM 的情况下，但具有额外的变体，由于报告设备固件中的正确模拟页使用情况有可能相同的方式进行映射。

设备报告泛型轴接收相同的映射，并可以使用相同的重写的 HID 和 WinMM 数据路径中的机制。 但是，这些重写会影响仅泛型的轴;它们不会更改设备上的所有轴使用映射表。

### <a name="axis-overrides-under-windows-9598me"></a>在 Windows 95/98/我的轴替代

轴重写会影响以下接口：

-   WinMM JoyGetPos()
-   WinMM JoyGetPosEx()
-   **IDirectInput2**
-   **IDirectInput7**
-   **IDirectInput8**

### <a name="to-perform-an-axis-override"></a>若要执行的轴替代：

1.  插入重写其轴的设备。 运行 joy.cpl 或任何其他 DirectInput 应用来初始化此设备的注册表项。 拔出该设备。

2.  打开注册表，并查找 HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\控制\\MediaProperties\\PrivateProperties\\游戏杆\\OEM

3.  找到重写其轴的设备的密钥。 键应位于此密钥，其 VID 和 PID 组合来指定。

4.  创建以下子项：

    -   轴
    -   "轴"项下指定一个密钥用于你想要重写 （轴密钥） 每个轴。 从 0 到 7 的描述了 GUID 和轴信息的一位数字指定的键：

        <table>
        <colgroup>
        <col width="33%" />
        <col width="33%" />
        <col width="33%" />
        </colgroup>
        <thead>
        <tr class="header">
        <th>项名称</th>
        <th>DirectX GUID</th>
        <th>WinMM Axis</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td><p>0</p></td>
        <td><p>GUID_XAxis</p></td>
        <td><p>X</p></td>
        </tr>
        <tr class="even">
        <td><p>1</p></td>
        <td><p>GUID_YAxis</p></td>
        <td><p>Y</p></td>
        </tr>
        <tr class="odd">
        <td><p>2</p></td>
        <td><p>GUID_ZAxis</p></td>
        <td><p>Z</p></td>
        </tr>
        <tr class="even">
        <td><p>3</p></td>
        <td><p>GUID_RxAxis</p></td>
        <td><p>-</p></td>
        </tr>
        <tr class="odd">
        <td><p>4</p></td>
        <td><p>GUID_RyAxis</p></td>
        <td><p>-</p></td>
        </tr>
        <tr class="even">
        <td><p>5</p></td>
        <td><p>GUID_RzAxis</p></td>
        <td><p>R</p></td>
        </tr>
        <tr class="odd">
        <td><p>6</p></td>
        <td><p>GUID_Slider</p></td>
        <td><p>U</p></td>
        </tr>
        <tr class="even">
        <td><p>7</p></td>
        <td><p>GUID_Slider</p></td>
        <td><p>V</p></td>
        </tr>
        </tbody>
        </table>




-   每个轴项下指定你想要替代的轴。 创建一个名为的二进制值**属性**并将其设置为：00 00 00 00 00 HUP HU 00。 HUP 是指定您想要覆盖的设备对象 （轴） 的 HID 使用页面的两位十六进制数。 HU 是指定的设备对象的 HID 用法的两位十六进制数。 使用 DIQuick 以确定这些值，或参阅 HID 规范。
-   设备回并使用任何程序来检查是否替代共同发挥作用，即插即用。


### <a name="meaning-of-the-registry-keys"></a>注册表项的含义

首先需要 DirectX 接口的轴映射和 WinMM 接口之间进行区分。

DirectX 接口将解释 Axiskeys 以匹配用于标识对象的 Guid。 Guid 是用于从设备读取数据和中指定的对象**IDirectInputDevice8::SetDataFormat()**。 如果程序读取的对象的数据，此对象中重写，则 DirectInput 返回中重写的对象的数据。

正如您所看到的滑块 0 与滑块 DirectInput 接口中的 1 之间没有差异。 这意味着，当重写轴 6 或 7，您始终重写第一个可用滑块。 如果滑块 0 尚未定义的轴，并将轴映射到 7，滑块 0 中重写。

与此相反，WinMM 接口执行区分 u 和 V 轴，因此 V 轴轴 7 中重写，如果收到的重写的对象; 中的数据如果轴 6 重写时，数据被转换为发送的 U 轴。

### <a name="rules-to-keep-in-mind"></a>要记住的规则

若要确保相等的接口的行为，必须遵循严格的规则。 这些规则提供了 WinMM 接口的行为。

不符合这些规则的映射可能会导致失败的 WinMM 接口会报告此设备的任何数据。

这些规则不适用于滑块映射; 之间的差异这种差异是可接受的。

不支持不在以下规则内任何映射。

-   没有漏洞。

    轴映射后将替代应用必须是连续的。 只有一个轴可以位于未映射的状态，也就是说，"2"= GUID\_ZAxis = Z。 不能跳过轴项。 对于示例、 X、 Y、 Z、 R、 U、 V 是有效的序列，但 X、 Z、 R、 U、 V 是不是因为有一个"hole"之间 X 和 Z。

-   存在所有轴。

    在设备上必须存在用于执行替代操作 （由属性值指定） 的所有轴。

-   不移动轴"向上"而不映射到它们。

    不能将轴的映射到轴而无需映射轴 C 轴 A 与 B 中，如果轴 A 将上表中具有较低的密钥名称中。

    将轴而不映射向上移到它会导致一个三角形孔。

### <a name="if-the-mapping-is-not-reflected-by-the-interfaces"></a>如果映射不反映通过接口

-   在更改映射之前，始终拔出该设备。 即插即用设备后才能重新初始化 DirectInput 编辑映射回。

-   DirectInput 可以拒绝特殊重写。 检查的项：HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\控制\\MediaProperties\\PrivateProperties\\DirectInput\\VID 和 PID，其中 VID 和 PID 是设备 VID PID 组合。 如果没有设置值 Flags2，DirectInput 在内部映射到轴的轴，并且不能重写这些映射。 例如，您可能不能移动滑块离开 DInput7/2 和 WinMM 接口中的 z 轴的映射。

-   如果用户安装并校准游戏杆，生成的校准信息存储在注册表中。 如果驱动程序现已安装，用于设置轴将不同于以前存储在注册表中重写，DirectInput 应用存储在注册表中的重写。 在注册表中的校准信息不会反映轴映射更改，因为数据可能会错误地报告，或可能不会报告所有被重写的轴上。

    有两种方法来防止这种情况：

    -   用户可以重新校准设备。
    -   驱动程序供应商的安装可以删除注册表中的校准信息。

如果设备不使用 joyhid.vxd 作为其驱动程序、 wUsage 和 wUsagePage 值仅用于描述哪些使用情况和使用情况页面对象应被视为，而不是任何形式的重写。 设备使用 joyhid.vxd 才的注册表项 HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\控制\\MediaProperties\\PrivateProperties\\游戏杆\\OEM\\VID 和 PID\\OEMCallout 等于 joyhid.vxd。








