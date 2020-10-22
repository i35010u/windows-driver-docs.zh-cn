---
title: 创建 INF 文件
description: 创建 INF 文件
ms.assetid: c45fb42c-f0d6-4ab8-9a19-4bbf98c4cf8c
keywords:
- 游戏杆 WDK HID、INF 文件
- 虚拟游戏杆驱动程序 WDK HID、INF 文件
- VJoyD WDK HID，INF 文件
- INF 文件 WDK 操纵杆
- INF 文件 WDK 操纵杆，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 833e83e7fb036fc60940a0622a34dbdcd32dc65e
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92356031"
---
# <a name="creating-an-inf-file"></a>创建 INF 文件

所有微型驱动程序和 OEM 定义的游戏杆都应该使用 INF 文件进行安装，以向系统提供所有必需的信息。 INF 文件描述设备安装的设备、需要复制的文件、任何兼容的设备、设备所需的任何系统资源以及对注册表进行更改的方面。 用于自定义标准模拟驱动程序的 INF 文件不需要复制任何文件和状态兼容设备，也不需要指定系统资源。 INF 文件可以指定其他操作，例如修改 Autoexec.bat 文件，但这对于操纵杆微型驱动程序通常是不必要的。

INF 文件包含下面描述的元素：

## <a name="setting-the-device-class"></a>设置设备类

游戏杆落在 "添加新硬件" 控制面板下的 "声音、视频和游戏控制器" 这一介质类下。 应从示例或操纵杆文件复制与类相关的部分。

## <a name="selecting-source-files"></a>选择源文件

INF 文件的 "SourceDisksFiles" 部分指定要复制的文件。 这包括所有必要的驱动程序以及任何其他文件，如文档和安装应用程序。 由于这可能是要安装在用户系统上的第一个操纵杆驱动程序，因此除了此设备的特定驱动程序外，还应复制系统游戏杆驱动程序 Vjoyd 和 Msjstrick。 应通过引用 Layout 来建立这两个驱动程序的源， (会导致系统提示用户输入 Windows 95/98/Me 安装光盘) 而不是分发到 OEM 光盘上。应将驱动程序复制到用户的系统目录，该目录是目标代码11。

## <a name="setting-the-manufacturer-specific-data"></a>设置 Manufacturer-Specific 数据

INF 文件所指向的特定于制造商的部分包含可安装的每个设备的一个条目。 每个条目都包含设备名称，后跟安装部分的名称、设备 ID 和任何兼容的设备。 如果设备已注册为即插即用兼容，则应将即插即用 ID (以星号) 开头。 如果设备尚未注册，则不即插即用兼容的设备 ID (即，不能使用星号) 的设备 ID。 注册这种类型的设备时，请避免选择与其他设备 Id 冲突 ( "操纵杆" 的 ID，例如，不是) 好的 ID。

## <a name="setting-up-logconfig-entries"></a>设置 LogConfig 条目

需要系统资源（如输入/输出 (i/o) 端口）的设备使用 "安装" 部分中的 "LogConfig" 条目来指定可以使用的配置。 某些设备不使用其自己的资源。 相反，它们使用其他驱动程序（例如串行端口驱动程序）与设备通信。 DirectX 3.0 VJoyD 与先前版本的不同之处在于其处理模拟游戏端口 i/o 端口要求。 仅当至少有一个设备已配置为具有标准游戏端口范围0x200 到0x20f 端口的一个或两个 i/o 端口分配时，较旧版本才会起作用。  (此外，第二个 i/o 范围必须是单个端口。如果没有任何游戏端口配置为允许没有游戏端口的系统使用通过微型驱动程序运行的设备，则新的 VJoyD 将正常运行 ) 。  (第二个 i/o 范围现在可以是多个端口。 ) 

使用0x200 到0x20f 范围内的端口的设备被 VJoyD 解释为模拟游戏端口，因此，它可能被配置管理器视为发生了冲突的设备。 将忽略任何其他游戏端口 i/o 端口集;如果计算机上有两个卡上的游戏端口，则只轮询一个卡上的端口。 如果设备需要以非标准方式使用标准游戏端口，事情会变得更加有趣。 在 LogConfig 的安装部分中请求标准端口可以正常工作，但这通常会导致更多的重新配置和重新启动来交换游戏杆。 一种替代方法是通过使用通过符合游戏端口标准的 configuration manager 回调传递的任何一组 i/o 范围来与 VJoyD 共享资源。 只要用户没有将游戏杆配置为标准模拟驱动程序和 OEM 驱动程序，就运行一个尝试同时轮询它们的应用程序，这就足够了。

在 DirectX 3.0 中，通过设置 "欢乐 HWS ISGAMEPORTDRIVER" 标志，实现了更改，以允许通过调用 OEM VxD 来替代标准模拟轮询 \_ \_ 。 "控制面板" 允许将此类设备设置为全局驱动程序，这意味着，对于没有与之相关联的任何微型驱动程序的任何操纵杆，将调用它（而不是内部模拟轮询）。 这可确保 VJoyD 不会干扰 OEM 设备的轮询。

如果启动过程中的前四个设备均由微型驱动程序处理 (这可能是 OEM 全局驱动程序) 的，则 VJoyD 不会检查--而不能使用任何游戏端口，即使这些设备不再由微型驱动程序处理。 如果 VJoyD 不能 (使用其端口，或者) 不存在游戏端口，则将 " \_ OEMPOLLRC \_ YOUPOLL" 返回到轮询请求不会导致使用标准轮询。 仅在重新分配游戏端口资源之后，使用此轮询重新配置到设备的操作才会生效 (可能不会) 重启。

## <a name="setting-up-addreg-entries"></a>设置 AddReg 条目

INF 文件还需要在 "安装" 部分的 AddReg 条目所选择的部分中设置注册表项。 对于需要微型驱动程序的设备，需要设置以下各项，确保驱动程序与多媒体系统驱动程序正确关联：

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

% OEMJoy; DeviceDesc% string 替换为已调用的设备名称字符串。

描述此操纵杆的值将放入 OEM 定义的密钥，从路径 REGSTR \_ 路径 \_ JOYOEM (在 HKEY \_ LOCAL \_ MACHINE) 中找到。 在此项下，OEM 可以放置一些静态值，这些值自定义 OEM 操纵杆在游戏杆校准程序中显示的方式，以及适用于 Windows 95/98/Me 的应用程序。 值的名称是在 Regstr 中定义的，因此它是下面讨论的这些常量的名称，而不是注册表中显示的名称。 每个 OEM 定义的设备至少必须定义其基本属性和用户可以在 "控制面板" 下的 "游戏杆" 选择框中看到的名称。 对于要加载的微型驱动程序，值必须包含微型驱动程序 VxD 的名称 (包括 .vxd 扩展名) 。 OEM name 值 (REGSTR \_ val \_ JOYOEMNAME) ，微型驱动程序文件名 (REGSTR \_ val \_ JOYOEMCALLOUT) 值为简单字符串。 基本属性 REGSTR \_ VAL \_ JOYOEMDATA 值为二进制数据，其含义在以下章节中详细说明。

有两个双字;第一个包含一组标志，第二个是设备的按钮数。

标志指定设备的类型、哪些轴存在以及如何解释它们。

大多数标志是在 Mmddk 中定义的。 在 DirectX 3.0 中添加的两个新标志是在 Dinput 中定义的。 以下标志仅用于重新映射由 VJoyD 直接轮询的 OEM 定义的模拟操纵杆的轴。 执行模拟轮询时，它们会更改 VJoyD 的默认行为，但不会影响微型驱动程序返回的数据。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_HWS_XISJ1Y</p></td>
<td><p>X 位于 J1 Y 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_XISJ2X</p></td>
<td><p>X 位于 J2 X 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_XISJ2Y</p></td>
<td><p>X 位于 J2 Y 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_YISJ1X</p></td>
<td><p>Y 位于 J1 X 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_YISJ2X</p></td>
<td><p>Y 位于 J2 X 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_YISJ2Y</p></td>
<td><p>Y 位于 J2 Y 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_RISJ1X</p></td>
<td><p>R 位于 J1 X 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_RISJ1Y</p></td>
<td><p>R 位于 J1 Y 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_RISJ2Y</p></td>
<td><p>R 位于 J2 Y 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ZISJ1X</p></td>
<td><p>Z 位于 J1 X 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_ZISJ1Y</p></td>
<td><p>Z 位于 J1 Y 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ZISJ2X</p></td>
<td><p>Z 位于 J2 X 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_POVISJ1X</p></td>
<td><p>轮询的 POV 在 J1 X 轴上。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_POVISJ1Y</p></td>
<td><p>轮询的 POV 在 J1 Y 轴上。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_POVISJ2X</p></td>
<td><p>轮询的 POV 在 J2 X 轴上。</p></td>
</tr>
</tbody>
</table>

默认行为是：

- X 默认为 J1 X 轴。

- Y 默认值为 J1 Y 轴。

- R (方向舵) 默认为 J2 X 轴。

- Z 默认为 J2 Y 轴。

- 如果以轮询形式实现，则 (POV hat) 默认为 J2 Y 轴。

还定义了标志来确定 POV 数据是来自坐标轴还是来自按钮组合。 如果 VJoyD 对所述设备进行轮询，有趣的工作 \_ 流服务 \_ POVISBUTTONCOMBOS 会导致 VJoyD 解释按钮组合以生成 POV，否则，将使用一个轴来查找它。 如果通过微型驱动程序对所述设备进行轮询，则未定义的 **dwPOV** 中的值将 \_ 导致覆盖任何其他 pov 计算。 但是，如果 \_ \_ 设置了 "有趣的工作流服务 POVISBUTTONCOMBOS"，则 VJoyD 会将其解释为模拟游戏杆的按钮。 否则 \_ ，如果未设置 "HASZ 工作流服务"，则从 Z 轴值获取 POV \_ ，否则为。 如果可能，微型驱动程序应避免使用一般 VJoyD 解释 POV 信息，因为微型驱动程序通常包含有关硬件实现的详细信息。

以下标志用于说明设备具有哪些功能：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_HWS_HASZ</p></td>
<td><p>操纵杆 (第三个轴) 信息。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_HASR</p></td>
<td><p>操纵杆有 R (第四个轴) 信息。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_HASU</p></td>
<td><p>操纵杆有 R (第四个轴) 信息。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_HASV</p></td>
<td><p>操纵杆有 R (第四个轴) 信息。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_HASPOV</p></td>
<td><p>游戏杆包含一个 POV hat。</p></td>
</tr>
</tbody>
</table>

以下标志用于说明设备类型：

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
<td><p>设备是 (DirectX 3.0) 中定义的头跟踪器。</p></td>
</tr>
</tbody>
</table>

最后， \_ \_ 在 DirectX 3.0 中添加的 "娱乐 HWS ISGAMEPORTDRIVER" 标志指示此微型驱动程序替换游戏端口的标准轮询。

例如，如果有8个按钮并为 X、Y、Z、R 和 POV 返回值的数字操纵杆，则需要设置位 "乐趣 \_ hws \_ HASZ"、"乐趣 \_ hws \_ HASPOV" 和 "游戏工作流服务 \_ \_ HASR"。 这为你提供了以下内容：

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
<td><p>01、00、00、00</p></td>
</tr>
<tr class="even">
<td><p>|</p></td>
<td><p>0x00000002</p></td>
<td><p>JOY_HWS_HASPOV</p></td>
<td><p>02、00、00、00</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>0x00080000</p></td>
<td><p>JOY_HWS_HASR</p></td>
<td><p>00，00，08，00</p></td>
</tr>
<tr class="even">
<td><p>=</p></td>
<td><p>0x00080003</p></td>
<td><p>组合</p></td>
<td><p>03、00、08、00</p></td>
</tr>
</tbody>
</table>

将此 **DWORD** 设置为小字节序格式，后跟一个 **dword** 值作为按钮数量，为您提供03，00，08，00，08，00，00，00，即 INF 文件中所需的一系列字节。

INF 文件中提供的所有其他注册表设置自定义标准控制面板给定的校准说明，如下所示：

<a href="" id="regstr-val-joyoemxylabel-"></a>REGSTR \_ VAL \_ JOYOEMXYLABEL 此字符串显示在操纵杆 CPL 的 "测试" 和 "校准" 对话框中的 "XY 位置" 控件下。

<a href="" id="regstr-val-joyoemzlabel-"></a>REGSTR \_ VAL \_ JOYOEMZLABEL 此字符串显示在操纵杆 CPL 的 "测试" 和 "校准" 对话框中的 Z 位置控件下。

<a href="" id="regstr-val-joyoemrlabel-"></a>REGSTR \_ VAL \_ JOYOEMRLABEL 此字符串显示在操纵杆 CPL 的 "测试" 和 "校准" 对话框中的 "R 位置" 控件下。

<a href="" id="regstr-val-joyoempovlabel-"></a>REGSTR \_ VAL \_ JOYOEMPOVLABEL 此字符串显示在操纵杆 CPL 的 "测试" 和 "校准" 对话框中的 "POV hat" 控件下。

<a href="" id="regstr-val-joyoemulabel-"></a>REGSTR \_ VAL \_ JOYOEMULABEL 此字符串显示在操纵杆 CPL 的 "测试" 和 "校准" 对话框中的 U 位置控件下。

<a href="" id="regstr-val-joyoemvlabel-"></a>REGSTR \_ VAL \_ JOYOEMVLABEL 此字符串显示在操纵杆 CPL 的 "测试" 和 "校准" 对话框中的 "V 位置" 控件下。

<a href="" id="regstr-val-joyoemtestmovedesc-"></a>REGSTR \_ VAL \_ JOYOEMTESTMOVEDESC 此字符串显示在 "测试" 对话框的 "移动" 部分中。 它介绍了如何测试操纵杆的用户。

<a href="" id="regstr-val-joyoemtestbuttondesc-"></a>REGSTR \_ VAL \_ JOYOEMTESTBUTTONDESC 此字符串显示在 "测试" 对话框的 "按钮" 部分中。 它向用户介绍如何测试按钮。

<a href="" id="regstr-val-joyoemtestmovecap-"></a>REGSTR \_ VAL \_ JOYOEMTESTMOVECAP 此字符串显示为 "测试" 对话框的 "移动" 部分周围的分组框的标题。

<a href="" id="regstr-val-joyoemtestbuttoncap-"></a>REGSTR \_ VAL \_ JOYOEMTESTBUTTONCAP 此字符串显示为 "测试" 对话框的 "按钮" 部分周围的分组框的标题。

<a href="" id="regstr-val-joyoemtestwincap-"></a>REGSTR \_ VAL \_ JOYOEMTESTWINCAP 此字符串显示为 "测试" 对话框的标题。

<a href="" id="regstr-val-joyoemcalcap-"></a>REGSTR \_ VAL \_ JOYOEMCALCAP 此字符串将显示为校准对话框的标题。

<a href="" id="regstr-val-joyoemcalwincap-"></a>REGSTR \_ VAL \_ JOYOEMCALWINCAP 此字符串显示为校准对话框的标题。

<a href="" id="regstr-val-joyoemcal1-"></a>REGSTR \_ VAL \_ JOYOEMCAL1 此字符串指示用户如何使操纵杆的 XY 部分居中以便进行校准。

<a href="" id="regstr-val-joyoemcal2-"></a>REGSTR \_ VAL \_ JOYOEMCAL2 此字符串指示用户如何移动操纵杆的 XY 部分以进行校准。

<a href="" id="regstr-val-joyoemcal3-"></a>REGSTR \_ VAL \_ JOYOEMCAL3 此字符串指示用户如何 recenter 操纵杆的 XY 部分进行校准。

<a href="" id="regstr-val-joyoemcal4-"></a>REGSTR \_ VAL \_ JOYOEMCAL4 此字符串指示用户如何移动操纵杆的 Z 部分以进行校准。

<a href="" id="regstr-val-joyoemcal5-"></a>REGSTR \_ VAL \_ JOYOEMCAL5 此字符串指示用户如何移动操纵杆的 R 部分进行校准。

<a href="" id="regstr-val-joyoemcal6-"></a>REGSTR \_ VAL \_ JOYOEMCAL6 此字符串指示用户如何移动操纵杆的 U 部分进行校准。

<a href="" id="regstr-val-joyoemcal7-"></a>REGSTR \_ VAL \_ JOYOEMCAL7 此字符串指示用户如何移动操纵杆的 V 部分进行校准。

<a href="" id="regstr-val-joyoemcal8-"></a>REGSTR \_ VAL \_ JOYOEMCAL8 此字符串指示用户如何移动 POV 头盔以便进行校准。

<a href="" id="regstr-val-joyoemcal9-"></a>REGSTR \_ VAL \_ JOYOEMCAL9 此字符串指示用户如何移动 POV hat 权限以便进行校准。

<a href="" id="regstr-val-joyoemcal10-"></a>REGSTR \_ VAL \_ JOYOEMCAL10 此字符串指示用户如何移动 POV hat 以便进行校准。

<a href="" id="regstr-val-joyoemcal11-"></a>REGSTR \_ VAL \_ JOYOEMCAL11 此字符串指示用户如何移动 POV hat 以便进行校准。

<a href="" id="regstr-val-joyoemcal12-"></a>REGSTR \_ VAL \_ JOYOEMCAL12 此字符串包含一条消息，通知用户校准过程已完成。
