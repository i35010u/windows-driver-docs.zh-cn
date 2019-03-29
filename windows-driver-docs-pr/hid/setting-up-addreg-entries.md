---
title: 设置 AddReg 条目
description: 设置 AddReg 条目
ms.assetid: 6b3e3eea-96d6-4f39-907a-80ef64ba61a9
keywords:
- INF 文件 WDK 游戏杆，AddReg 条目
- AddReg 条目 WDK 游戏杆
- 注册表 WDK 游戏杆
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da0fadb5af3a7fdc0b0f386e90e15179845b9961
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577566"
---
# <a name="setting-up-addreg-entries"></a>设置 AddReg 条目





INF 文件还需要在选择安装部分的 AddReg 条目的部分中设置注册表项。 对于需要微型驱动程序的设备，下面需要设置以确保该驱动程序正确地与多媒体系统驱动程序相关联：

```cpp
HKR,,DevLoader,,mmdevldr.vxd
HKR,Drivers,,,
HKR,Drivers,MIGRATED,,0
HKR,Drivers\joystick,,,
HKR,,Driver,,vjoyd.vxd
HKR,Drivers\joystick\msjstick.drv,,,
HKR,Drivers\joystick\msjstick.drv,Description,,%OEMJoy.DeviceDesc%
HKR,Drivers\joystick\msjstick.drv,Driver,,msjstick.drv
```

%OEMJoy.DeviceDesc%字符串被替换为任何调用的设备名称字符串。

描述此游戏杆的值将放入注册表项下的 OEM 定义的密钥，开头的路径 REGSTR\_路径\_JOYOEM (HKEY 下找到\_本地\_机)。 在此项下，OEM 可以放置多个自定义在游戏杆校准程序和应用程序的 Windows 95/98/me OEM 游戏杆的显示的方式的静态值 因此，下面，而不是出现在注册表中的名称将讨论这些常量的名称中 Regstr.h，定义的值的名称。 OEM 定义的每个设备至少必须具有定义其基本属性和用户可以看到游戏杆选择框在控制面板中的名称。 对于要加载微型驱动程序，值必须包含微型驱动程序 （包括.vxd 扩展名） 的 VxD 的名称。 OEM 名称值 (REGSTR\_VAL\_JOYOEMNAME)，和的微型驱动程序文件的名称 (REGSTR\_VAL\_JOYOEMCALLOUT) 的值为简单的字符串。 基本属性 REGSTR\_VAL\_JOYOEMDATA 值是二进制数据，其含义将因以下段落中详细介绍。

有两个双字数组;第一个包含一组标志，第二个按钮的设备数。

标志指定何种设备，哪个轴都存在，并解释如何。

Mmddk.h 中定义了大多数的标志。 DirectX 3.0 中新增的两个新标志 Dinput.h 中定义。 以下标志仅用于重新映射 OEM 定义模拟游戏杆，直接通过 VJoyD 轮询一次的轴。 它们执行模拟轮询时更改 VJoyD 的默认行为，但对微型驱动程序返回的数据没有影响。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_HWS_XISJ1Y</p></td>
<td><p>X 是 J1 Y 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_XISJ2X</p></td>
<td><p>X 是 J2 X 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_XISJ2Y</p></td>
<td><p>X 是 J2 Y 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_YISJ1X</p></td>
<td><p>Y 是 J1 X 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_YISJ2X</p></td>
<td><p>Y 是 J2 X 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_YISJ2Y</p></td>
<td><p>Y 是 J2 Y 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_RISJ1X</p></td>
<td><p>R 是 J1 X 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_RISJ1Y</p></td>
<td><p>R 是 J1 Y 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_RISJ2Y</p></td>
<td><p>R 是 J2 Y 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ZISJ1X</p></td>
<td><p>Z 是 J1 X 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_ZISJ1Y</p></td>
<td><p>Z 是 J1 Y 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ZISJ2X</p></td>
<td><p>Z 是 J2 X 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_POVISJ1X</p></td>
<td><p>轮询的 POV 是 J1 X 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_POVISJ1Y</p></td>
<td><p>轮询的 POV 是 J1 Y 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_POVISJ2X</p></td>
<td><p>轮询的 POV 是 J2 X 轴上。</p></td>
</tr>
</tbody>
</table>

 

默认行为是：

-   X 将默认为 J1 X 轴。

-   Y 默认值为 J1 Y 轴。

-   R （方向舵） 默认值为 J2 X 轴。

-   Z 默认值为 J2 Y 轴。

-   POV hat （如果作为轮询实现） 默认为 J2 Y 轴。

标志还定义来确定 POV 数据来自从轴或按钮组合。 如果所述的设备轮询的 VJoyD，乐趣\_工作流服务\_POVISBUTTONCOMBOS 导致 VJoyD 来解释按钮组合以生成 POV，否则使用轴来找到它。 如果通过微型驱动程序，则中的值轮询一次所述的设备**dwPOV** POV 以外\_UNDEFINED 导致的任何其他 POV 计算重写。 但是，如果 JOY\_工作流服务\_设置 POVISBUTTONCOMBOS，VJoyD 会按钮将解释为就像模拟游戏杆。 否则 POV 不会执行的 Z 轴值从 JOY\_工作流服务\_HASZ 未设置，请从 R 否则为。 如果可能，微型驱动程序应避免泛型 VJoyD 解释 POV 信息，如微型驱动程序通常具有硬件实现详细信息。

以下标志用于描述设备有哪些功能：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_HWS_HASZ</p></td>
<td><p>游戏杆包含 Z （第三个轴） 的信息。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_HASR</p></td>
<td><p>游戏杆了 R （第四个轴） 的信息。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_HASU</p></td>
<td><p>游戏杆了 R （第四个轴） 的信息。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_HASV</p></td>
<td><p>游戏杆了 R （第四个轴） 的信息。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_HASPOV</p></td>
<td><p>游戏杆具有 POV hat。</p></td>
</tr>
</tbody>
</table>

 

以下标志用于描述设备类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_HWS_ISYOKE</p></td>
<td><p>设备是飞行控制器。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ISGAMEPAD</p></td>
<td><p>设备是游戏板。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_ISCARCTRL</p></td>
<td><p>设备是赛车控制器。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ISHEADTRACKER</p></td>
<td><p>设备是一个头跟踪器 （在 DirectX 3.0 中定义）。</p></td>
</tr>
</tbody>
</table>

 

最后，乐趣\_工作流服务\_DirectX 3.0 中新增了 ISGAMEPORTDRIVER 标志指示此微型驱动程序将替换游戏端口的标准轮询。

例如，如果您有数字游戏杆，具有八个按钮，并返回 x 值，Y，Z，R、 和 POV，然后您需要设置位乐趣\_工作流服务\_HASZ，乐趣\_工作流服务\_HASPOV 和乐趣\_工作流服务\_HASR。 这提供了以下：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td></td>
<td><p>0x00000001</p></td>
<td><p>JOY_HWS_HASZ</p></td>
<td><p>01,00,00,00</p></td>
</tr>
<tr class="even">
<td><p>|</p></td>
<td><p>0x00000002</p></td>
<td><p>JOY_HWS_HASPOV</p></td>
<td><p>02,00,00,00</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>0x00080000</p></td>
<td><p>JOY_HWS_HASR</p></td>
<td><p>00,00,08,00</p></td>
</tr>
<tr class="even">
<td><p>=</p></td>
<td><p>0x00080003</p></td>
<td><p>组合</p></td>
<td><p>03,00,08,00</p></td>
</tr>
</tbody>
</table>

 

避免争用**DWORD**在 little-endian 格式，跟**DWORD**的按钮，使您 03,00,08,00,08,00,00,00，是一系列字节的 INF 文件中所需的数目。

所有剩余的注册表设置 INF 文件中提供自定义标准控件面板中，通过给定的校准的说明和如下所示：

<a href="" id="regstr-val-joyoemxylabel-"></a>REGSTR\_VAL\_JOYOEMXYLABEL   
此字符串显示在测试中找到 XY 位置控件下方，并校准游戏杆 CPL 的对话框。

<a href="" id="regstr-val-joyoemzlabel-"></a>REGSTR\_VAL\_JOYOEMZLABEL   
此字符串显示在测试中找到的 Z 位置控件的下方，并校准游戏杆 CPL 的对话框。

<a href="" id="regstr-val-joyoemrlabel-"></a>REGSTR\_VAL\_JOYOEMRLABEL   
此字符串显示在测试中找到 R 位置控件下方，并校准游戏杆 CPL 的对话框。

<a href="" id="regstr-val-joyoempovlabel-"></a>REGSTR\_VAL\_JOYOEMPOVLABEL   
此字符串显示在测试中找到 POV hat 控件下方，并校准游戏杆 CPL 的对话框。

<a href="" id="regstr-val-joyoemulabel-"></a>REGSTR\_VAL\_JOYOEMULABEL   
此字符串显示在测试中找到 U 位置控件下方，并校准游戏杆 CPL 的对话框。

<a href="" id="regstr-val-joyoemvlabel-"></a>REGSTR\_VAL\_JOYOEMVLABEL   
此字符串显示在测试中找到 V 位置控件下方，并校准游戏杆 CPL 的对话框。

<a href="" id="regstr-val-joyoemtestmovedesc-"></a>REGSTR\_VAL\_JOYOEMTESTMOVEDESC   
在测试对话框的移动部分中显示此字符串。 它介绍了向用户如何测试游戏杆。

<a href="" id="regstr-val-joyoemtestbuttondesc-"></a>REGSTR\_VAL\_JOYOEMTESTBUTTONDESC   
此字符串显示在测试对话框的按钮部分。 它介绍了向用户如何测试按钮。

<a href="" id="regstr-val-joyoemtestmovecap-"></a>REGSTR\_VAL\_JOYOEMTESTMOVECAP   
此字符串显示为组框周围移动部分中的测试对话框的标题。

<a href="" id="regstr-val-joyoemtestbuttoncap-"></a>REGSTR\_VAL\_JOYOEMTESTBUTTONCAP   
此字符串显示为组框周围的测试对话框的按钮部分的标题。

<a href="" id="regstr-val-joyoemtestwincap-"></a>REGSTR\_VAL\_JOYOEMTESTWINCAP   
此字符串显示为测试对话框的标题。

<a href="" id="regstr-val-joyoemcalcap-"></a>REGSTR\_VAL\_JOYOEMCALCAP   
此字符串将显示为校准对话框的标题。

<a href="" id="regstr-val-joyoemcalwincap-"></a>REGSTR\_VAL\_JOYOEMCALWINCAP   
此字符串显示为校准对话框的标题。

<a href="" id="regstr-val-joyoemcal1-"></a>REGSTR\_VAL\_JOYOEMCAL1   
此字符串指示用户如何 center 的校准游戏杆的 XY 部分。

<a href="" id="regstr-val-joyoemcal2-"></a>REGSTR\_VAL\_JOYOEMCAL2   
此字符串指示用户如何继续的校准游戏杆的 XY 部分。

<a href="" id="regstr-val-joyoemcal3-"></a>REGSTR\_VAL\_JOYOEMCAL3   
此字符串指示用户如何为自动的校准游戏杆的 XY 部分。

<a href="" id="regstr-val-joyoemcal4-"></a>REGSTR\_VAL\_JOYOEMCAL4   
此字符串指示用户如何继续的校准游戏杆的 Z 部分。

<a href="" id="regstr-val-joyoemcal5-"></a>REGSTR\_VAL\_JOYOEMCAL5   
此字符串指示用户如何继续的校准游戏杆的 R 部分。

<a href="" id="regstr-val-joyoemcal6-"></a>REGSTR\_VAL\_JOYOEMCAL6   
此字符串指示用户如何继续的校准游戏杆的 U 部分。

<a href="" id="regstr-val-joyoemcal7-"></a>REGSTR\_VAL\_JOYOEMCAL7   
此字符串指示用户如何继续的校准游戏杆的 V 部分。

<a href="" id="regstr-val-joyoemcal8-"></a>REGSTR\_VAL\_JOYOEMCAL8   
此字符串指示用户如何继续进行校准 POV 乘幂号。

<a href="" id="regstr-val-joyoemcal9-"></a>REGSTR\_VAL\_JOYOEMCAL9   
此字符串指示用户如何移动适合校准 POV 乘幂号。

<a href="" id="regstr-val-joyoemcal10-"></a>REGSTR\_VAL\_JOYOEMCAL10   
此字符串指示如何校准的向下移动 POV hat 用户。

<a href="" id="regstr-val-joyoemcal11-"></a>REGSTR\_VAL\_JOYOEMCAL11   
此字符串指示用户如何移动留给校准 POV hat。

<a href="" id="regstr-val-joyoemcal12-"></a>REGSTR\_VAL\_JOYOEMCAL12   
此字符串包含一条消息，通知用户，完成校正过程。

 

 




