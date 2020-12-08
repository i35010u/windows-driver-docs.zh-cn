---
title: 原始接口
description: 原始接口
keywords:
- 操纵杆 WDK HID，接口
- 虚拟游戏杆驱动程序 WDK HID，接口
- VJoyD WDK HID，接口
- 接口 WDK 操纵杆
- 操纵杆 WDK HID，回调
- 虚拟游戏杆驱动程序 WDK HID，回调
- VJoyD WDK HID，回调
- 回调 WDK 操纵杆
- 轮询 WDK 操纵杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee5185b8d3d0526c59e5ec5270d446fde9f3781f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831847"
---
# <a name="original-interface"></a>原始接口

以下操纵杆微型驱动程序回调特定于原始接口。 在 \_ \_ \_ 从处理 SYS \_ 动态 \_ 设备 \_ 初始消息返回之前，必须向 VJoyD VJoyD 注册设备驱动程序服务注册四个操纵杆特定的回调。 EAX 必须指向轮询例程，EBX (配置处理程序) ，ECX (功能回调) ，并 (标识例程) 。 游戏杆微型驱动程序注册序列的示例如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Mov</p></td>
<td><p>eax，offset32 _PollRoutine@8</p></td>
</tr>
<tr class="even">
<td><p>Mov</p></td>
<td><p>ebx、offset32 _CfgRoutine</p></td>
</tr>
<tr class="odd">
<td><p>Mov</p></td>
<td><p>ecx、offset32 _HWCapsRoutine@8</p></td>
</tr>
<tr class="even">
<td><p>Mov</p></td>
<td><p>edx、offset32 _JoyIdRoutine@8</p></td>
</tr>
<tr class="odd">
<td><p>VxDcall</p></td>
<td><p>VJOYD_Register_Device_Driver</p></td>
</tr>
</tbody>
</table>

 除了注册以外，微型驱动程序还可以在此时执行任何其他初始化。 操纵杆微型驱动程序模型不需要执行任何特定操作来响应 SYS \_ 动态 \_ 设备 \_ 退出，但 VxD 仍可将其用于最终内部清理。

## <a name="configuration-manager-callback"></a>Configuration Manager 回调

```cpp
CONFIGRET CM_HANDLER CfgRoutine( CONFIGFUNC cfFuncName,
    SUBCONFIGFUNC scfSubFuncName, DEVNODE dnToDevNode,
    ULONG dwRefData, ULONG ulFlags );
```

有关如何为 configuration manager 提供支持的常规信息，请访问 Windows 驱动程序开发工具包 (DDK) 的 Windows Me 部分的即插即用环境部分。  (在 Windows 驱动程序工具包 WDK 之前的 DDK \[ \] 。 ) 

仅当 VJoyD 接收回拨时加载微型驱动程序时，才会将 Configuration manager 回叫传递到微型驱动程序。 因此，此回调的当前实现存在重要问题。 当系统启动期间，当配置管理器在运行时为设备重新配置以及当系统关闭时，在运行时为其关联的设备节点，VJoyD 将收到回调。 因此，只有在以前的启动上选择的设备会按时加载，以接收这些消息。 这会限制在调用此回调时执行的潜在函数数量，因为用户可以启动系统、配置游戏杆、玩游戏、取消配置操纵杆，并在不调用此回调的情况下关闭。

对于不需要任何硬件资源的设备，这不是问题。 使用此类资源的设备具有几个选项：它们只能在启动时进行配置，可以从配置管理器中动态分配资源，也可以在注册表中为其设备节点搜索其分配，并请求信息。

对于上述信息，驱动程序会在第一次加载驱动程序时正确初始化，并会接收到系统 \_ 动态 \_ 设备 \_ 初始化，或首次通过轮询例程。 同样， \_ \_ 接收到 SYS 动态设备退出消息时，资源应是免费的 \_ 。

另一个问题是当前提供服务的游戏杆设备的所有 configuration manager 回叫都发送到所有加载的微型驱动程序。 但是，可以使用 *dnToDevNode* 参数查找设备标识符，并且可以对此驱动程序可以处理的设备进行检查。

## <a name="polling-callback"></a>轮询回调

```cpp
int stdcall PollRoutine( int type, LPJOYOEMPOLLDATA pojd );
```

对于调用 joyGetPos 或 joyGetPosEx 的应用程序，或者当 Windows 95/98/Me 定期为已调用 joySetCapture 的应用程序调用 joyGetPos 时，会调用轮询例程。 仅当微型驱动程序第一次在其轮询回调上收到调用时，可以确定应用程序是否需要数据。 对于当前位于16个可用游戏杆列表中的所有设备，都将调用所有其他回调，无论是否有任何应用程序请求数据。

可能的返回值为 \_ "OEMPOLLRC \_ YOUPOLL，乐趣 \_ OEMPOLLRC \_ \_ " 和 \_ "OEMPOLLRC"。 除了仅限按钮的轮询，返回值被解释为 JOYERR \_ NOERROR 或 JOYERR，然后再将其 \_ 返回给应用程序。 始终假定按钮轮询成功。

\_ \_ 如果轮询的设备未响应，或 VJoyD 请求微型驱动程序无法处理的轮询，则会返回 OEMPOLLRC。 在前一种情况下，应确保不会对设备进行故障转移，除非它确实出现故障，因为应用程序可能会停止所有操作，并请求用户检查与设备的连接。 例如，如果第一个轮询失败，则对 joySetCapture 的调用将失败。 在需要用户干预或检测到无法恢复的设备错误之前，次要设备故障不会导致报告失败。 例如，使用基于数据包的协议进行通信的设备应在一个数据包无效的情况下尝试在轮询失败之前重试。

务必识别正版设备故障并最终返回错误;否则，应用程序无法确定是否需要用户干预。 如果在执行错误恢复时返回了 "陈旧" 或 "假" 数据，则返回的数据的含义、允许的轮询数或从初始错误允许的时间应受到限制，以便驱动程序不会延迟一段时间。 当请求微型驱动程序对其不控制的设备执行轮询时，或者如果要执行它无法服务的轮询类型或子类型，则失败始终是正确的响应。

\_ \_ 如果标准模拟轮询产生正确的结果，则可以使用 "OEMPOLLRC" YOUPOLL。

\_ \_ 如果使用请求的数据填充 JOYINFOEX 结构，则应在常规情况下返回 "OEMPOLLRC"。

如果使用轮询在设备上执行初始化，则必须小心谨慎。 应用程序可以通过检查返回代码执行初始轮询以检查设备的可用性。 然后，他们可以进行后续轮询，无需错误检查。 这实质上是 joySetCapture 的作用。 理想情况下，应执行所有初始化和第一次轮询。 如果在这种情况下，设置设备所需的时间最多可达到一秒钟，就足以验证设备是否存在并正常工作，并返回静态的数据以进行第一次轮询。

API 和系统驱动程序对应用程序发出的请求执行验证，并在完成后将所需数据复制到应用程序结构中。 微型驱动程序不应复制此功能。 但是，任何一个进程都不会阻止一个进程轮询设备，而另一个进程仍处于轮询过程中。 此事件的后果并不比报告两个轴的不同示例更糟。 如有必要，微型驱动程序可以执行其自身的进程同步。

返回值取决于 "type" 参数及其支持的设备。 应始终返回按钮和按钮号。 由于无法指定微型驱动程序是否需要使用 POV 投票，因此，如果请求了任何轴，则应返回此值。 如果设备不支持此 POV，请将其设置为 \_ 未定义。 对于单轴轮询，该值将在 JOYPOLLDATA 结构的 **dwX** 成员中返回， (DirectX 5.0 和更高版本中的 [**VJPOLLDATA**](/previous-versions/windows/hardware/drivers/ff543573(v=vs.85)) 结构) 。 对于多轴请求（其中请求的轴数为奇数）， [**JOYOEMPOLLDATA**](/previous-versions/windows/hardware/drivers/ff542251(v=vs.85))结构 **的 \_ 其他** 成员指定是就地返回最后一个轴还是为以下轴返回上一个轴。 例如，在三轴轮询中，成员指定返回的轴是 X、Y、Z 还是 X、Y、R。

下面是其他可能的返回值的列表，这些值按类型分类 (您可以填写额外数据，但是请注意，奇数个轴的所有轮询都必须对 " **执行 \_ 其他** 成员" 进行解码，以决定返回的内容) ：

- 有趣 \_ \_ 的 OEMPOLL GETBUTTONS：没有任何额外内容。

- 有趣 \_ \_ 的 OEMPOLL POLL1：在 **dwX** 成员中返回在 **Do \_ 其他** 成员中指定的轴。

- 有趣 \_ \_ 的 OEMPOLL POLL2：在 **dwX** 和 **dwY** 成员中返回 X 和 Y 轴。

- 有趣 \_ \_ 的 OEMPOLL POLL3：在 **dwX** 和 **dwY** 成员中返回 X 和 Y 轴。

    如果 " **\_ 其他** 成员" 为非零值，则会在 **DwR** 成员中返回 R 轴。 否则，Z 轴将在 **dwZ** 成员中返回。

- 有趣 \_ \_ 的 OEMPOLL POLL4：分别在 **dwX**、 **dwY**、 **dwZ** 和 **dwR** 成员中返回 X、Y、Z 和 R 轴。

- 有趣 \_ \_ 的 OEMPOLL POLL5：分别在 **dwX**、 **dwY**、 **dwZ** 和 **dwR** 成员中返回 X、Y、Z 和 R 轴。

    如果 " **\_ 其他** 成员" 为非零值，则会在 **DwR** 成员中返回 V 轴。 否则，在 **dwZ** 成员中返回 U 轴。

- 有趣 \_ \_ 的 OEMPOLL POLL6：分别在 **dwX**、 **dwY**、 **dwZ**、 **dwR**、 **dwU** 和 **dwV** 成员中返回 X、Y、Z、R 和 V 轴。

DirectX 3.0 添加了 "无轮询" 类型的 " \_ OEMPASSDRIVERDATA"，其中，" **\_ 其他** 成员" 包含应用程序通过的 DWORD。 可以将此 DWORD 用于任何微型驱动程序定义的函数，但它仅用于启用已完全标识微型驱动程序的自定义安装应用程序，以发送设备特定的命令和配置信息。

对于不支持的所有类型，微型驱动程序应返回乐趣 \_ OEMPOLLRC \_ 失败。

尽管轴数据以双引号返回，但如果标准游戏杆控制面板配置用作唯一的配置机制，则轴值的范围应限制为大约10位值。 由于用户无法轻松地了解发生的情况，因此这有助于避免混淆。 为了帮助与现有应用程序的兼容性，微型驱动程序返回的轴应与模拟操纵杆 (所返回的轴相同，适用) 。 例如，X 将是最小化左侧的从左到右移动，依此类推。

对于激活的 POV hat，方向应表示为角度（以度为单位）乘以100，0表示向前9000、向右、向后18000、向左27000。

由于轮询例程调用是设备仍在使用中的唯一指示，因此使用共享资源（如通信端口）的微型驱动程序应跟踪上次使用的时间。 如果使用时间变得很重要，则微型驱动程序应停止采样设备并释放资源，以防用户已完成设备使用，现在尝试将资源用于其他目的。 如果出现通信错误，这一点特别重要，因为这可能表明设备已拔出。

## <a name="hardware-capabilities-callback"></a>硬件功能回调

```cpp
int __stdcall HWCapsRoutine( int joyid, LPJOYOEMHWCAPS pjhwc );
```

每次请求设备的硬件功能时，都将调用 HWCapsRoutine。 特别是，VJoyD 在从 VJOYD \_ Register \_ 设备驱动程序返回之前调用 HWCapsRoutine \_ 。 因此，在注册设备之前，驱动程序必须完成此调用所依赖的任何初始化，这一点很重要。 这些值通常为常量。 对于具有四个按钮和三个轴的设备，其中第三个按钮可以返回一个限制或方向舵值，以下内容适用：

```cpp
pjhwc->dwMaxButtons = 4;    /* This should always be the number of buttons */
pjhwc->dwMaxAxes = 4;       /* The largest axis number which may be requested */
pjhwc->dwNumAxes = 3;       /* The number of axes the device has */
```

## <a name="joystick-identification-callback"></a>游戏杆标识回调


```cpp
int __stdcall JoyIdRoutine( int joyid, BOOL used );
```

当用户配置或取消配置操纵杆作为16个操纵杆中的一个时，VJoyD 会调用 JoyIDRoutine。 如果微型驱动程序可以支持在 *joyid* 中请求的 ID，则 JoyIdRoutine 将返回一个非零值。 如果微型驱动程序不支持 ID，则例程返回零值。

只要进行了任何更改，就会调用 joyConfigChanged 来更新驱动程序，VJoyD 会循环遍历所有16个设备，从 JOYSTICKID1 开始。 它会将所有设备重置为未使用，然后再次循环遍历它们以设置系统需要使用的所有设备。 在 "控制面板" 操作过程中，此过程可能需要大量调用，这会导致此回调使用中的初始化问题。 如果在系统启动完成之前进行调用（即，其他服务不可用），则更是如此。

微型驱动程序，对于多个设备的服务回叫，应尽可能将操纵杆标识符与单个物理设备相关联，以避免用户混淆。 在单个会话期间，可以相对轻松地实现这一点，但重新启动后可能不需要这样做。

在 \_ \_ \_ 从处理 SYS \_ 动态 \_ 设备 \_ 初始消息返回之前，必须向 VJoyD VJoyD 注册设备驱动程序服务注册四个操纵杆特定的回调。 EAX 必须指向轮询例程，EBX (配置处理程序) ，ECX (功能回调) ，并 (标识例程) 。 游戏杆微型驱动程序注册序列的示例如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Mov</p></td>
<td><p>eax，offset32 _PollRoutine@8</p></td>
</tr>
<tr class="even">
<td><p>Mov</p></td>
<td><p>ebx、offset32 _CfgRoutine</p></td>
</tr>
<tr class="odd">
<td><p>Mov</p></td>
<td><p>ecx、offset32 _HWCapsRoutine@8</p></td>
</tr>
<tr class="even">
<td><p>Mov</p></td>
<td><p>edx、offset32 _JoyIdRoutine@8</p></td>
</tr>
<tr class="odd">
<td><p>VxDcall</p></td>
<td><p>VJOYD_Register_Device_Driver</p></td>
</tr>
</tbody>
</table>

 除了注册以外，微型驱动程序还可以在此时执行任何其他初始化。 操纵杆微型驱动程序模型不需要执行任何特定操作来响应 SYS \_ 动态 \_ 设备 \_ 退出，但 VxD 仍可将其用于最终内部清理。
