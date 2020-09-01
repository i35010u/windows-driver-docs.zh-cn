---
title: D3cold 固件要求
description: 从 Windows 8 开始，设备可以输入 D3cold 电源子状态，即使系统处于 S0 电源状态也是如此。
ms.assetid: 4BADC310-CC53-4084-A592-66197C348279
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77bf52439de3dd43d16829aa93e74ab7638568a0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187661"
---
# <a name="firmware-requirements-for-d3cold"></a>D3cold 固件要求


从 Windows 8 开始，设备可以输入 D3cold 电源子状态，即使系统处于 S0 电源状态也是如此。 本主题介绍为嵌入式设备实现 D3cold 支持的固件要求。 以下讨论旨在帮助固件开发人员使其嵌入式设备能够可靠地进入和退出 D3cold。

此外，还将简要介绍支持 D3cold 的设备驱动程序要求。 有关设备驱动程序对 D3cold 的支持的详细信息，请参阅 [在驱动程序中支持 D3cold](../kernel/supporting-d3cold-in-a-driver.md)。

## <a name="introduction"></a>简介


[设备电源状态](../kernel/device-power-states.md) 在 ACPI 规范和各种总线规范中定义。 PCI 总线规范具有，因为它引入了 PCI 电源管理，将 D3 (关闭) 设备电源状态分成两个子状态，即 D3hot 和 D3cold。 此区别已添加到 ACPI 3.0 的 ACPI 规范中，并已在 ACPI 4.0 中扩展。 Windows 始终支持两种 D3 子状态，但 Windows 7 和更早版本的 Windows 仅在整个计算机退出 S0 时才支持 D3cold 子状态， () 系统电源状态进入睡眠或休眠状态，通常为 S3 或 S4。 从 Windows 8 开始，设备驱动程序可以使其设备进入 D3cold 状态，即使系统处于 S0 状态也是如此。

D3hot （通常简称为 "D3"）是设备的 "软关闭" 状态。 在此状态下，可通过总线扫描检测到设备，发送到设备的命令可能会导致设备再次开机。 在 D3cold 中，将删除所有电源，并可能出现少量电源的异常，从而驱动设备的唤醒逻辑。 例如，对于 PCI Express (PCIe) 设备，在转换为 D3cold 时，主要设备电源源 Vcc 会经常关闭。 关闭 Vcc 可降低能耗，并延长移动硬件平台可以在电池电量上运行的时间。 如果设备处于 D3cold 中，则总线扫描无法检测到它，并且无法接收命令。 还原 Vcc 电源会将设备移到未初始化状态，这通常与 D0 状态相同。 然后，软件必须重新初始化设备，使其进入工作状态。

在 D3cold 中放置设备并不一定意味着已删除设备的所有电源源，这意味着只会删除主电源，Vcc。 如果唤醒逻辑不需要辅助电源源 Vaux，则还可能会将其删除。 但是，可能需要用来向处理器发出唤醒事件的设备必须能够为操作唤醒逻辑提供足够的功率。 例如，以太网网络接口卡 (NIC) ，其主电源被删除可能会从以太网电缆中消耗足够的功率。 或者，可以从 PCIe 接口之外的源提供 Wi-fi NIC 的备用电源，在这种情况下，可以完全关闭 PCIe 接口。

以下讨论介绍了一组要求，用于启用设备电源状态到 D3cold 的转换。 这些要求分为以下两个类别：

-   固件和平台要求
-   设备驱动程序要求

这两个类别中的第一种是讨论的主要焦点。 将显示第二个类别的简要概述。 有关设备驱动程序要求的详细信息，请参阅 [支持驱动程序中的 D3cold](../kernel/supporting-d3cold-in-a-driver.md)。

## <a name="firmware-and-platform-requirements"></a>固件和平台要求


在下面的讨论中，为这两种情况提供了启用 D3cold 的固件和平台要求：

-   在 ACPI 中枚举设备时。
-   当设备由其父总线枚举时。

以下大多数讨论特定于 PCIe。 但是，此处所述的一般原则也适用于其他总线。

提取一些详细信息，从 D3cold 到 D0 的转换是通过对嵌入的设备重新应用 Vcc 电源来触发的。 重新应用电源可以有效地还原设备与总线的连接。 Windows 读取设备的标识符，以便区分以下两种情况：

-   设备已被删除并被另一设备替换。
-   已删除相同的设备，然后重新插入。

如果标识符匹配，则设备驱动程序将重新初始化设备。 如果标识符不匹配，Windows 将卸载设备驱动程序并为新设备生成新的驱动程序堆栈。 例如，在某些版本的规范) 中，对供应商 ID、设备 ID 和子系统 Id 的查询将 (分解为子设备和子供应商 Id。 重新应用电源后，这些标识符必须与之前连接的设备的标识符匹配， (且总线指定的等待期已过) ;否则，Windows 会将新设备视为不同于上一设备。

### <a name="case-1-an-embedded-device-is-enumerated-in-acpi"></a>情况1：在 ACPI 中枚举嵌入式设备

如果嵌入式设备无法通过总线规范（如 PCIe 或 USB）定义的机制发现，但设备永久连接 (或者至少连接专用于已知设备) ，则可以通过 ACPI \_ HID 和/或 CID 对象在平台固件中描述此设备 \_ 。 通过这些对象，OSPM 可以枚举设备。  ( "OSPM" 是在 ACPI 规范中定义的术语。 这意味着，松散的 "不固件的软件"。仅当没有总线枚举器可以检测到设备 ID 时，) OSPM 才会枚举设备。 例如，OSPM 将枚举 ISA 总线上的设备。 此外， (SoC) 芯片上的系统上的设备通常由 ACPI 枚举，因为它们位于不可枚举的结构上。 此类设备的示例包括 USB 和 SD 主机控制器。

**平台固件**

OSPM 使用 \\ \_ SB。 \_.OSC 将平台范围内的 OSPM 功能传递到平台固件。 平台固件必须在 SB 中设置第2位 \\ \_ 。 \_.OSC 返回值，指示 OSPM 设备支持 \_ PR3。 有关详细信息，请参阅 ACPI 5.0 规范中的 6.2.10.2 "平台范围内的 OSPM 功能" 部分。

**嵌入式设备–仅通过 ACPI 发现**

为支持 D3cold，平台固件应为嵌入式设备实现以下 ACPI 电源资源对象：

-   \_PR0：此对象计算) 设备电源状态下的 D0 (中设备的电源要求。 返回值是设备在 D0 状态中所需的电源资源的列表。
-   \_PR2) ：此对象计算为 D2 设备电源状态下设备的电源要求。 返回值是设备在 D2 状态中所需的电源资源的列表。 请注意，由于历史原因， \_ 无论何时存在 PR0，Windows 都需要 pr2) \_ 。 如果在硬件中实现了 D2， \_ pr2) 会列出 d2 所需的电源资源。 如果未实现 D2， \_ pr2) 会列出与 PR0 相同的资源 \_ 。
-   \_PR3：此对象的计算结果为设备在 D3hot 设备电源状态下的电源要求。 返回值是设备在 D3hot 状态中所需的电源资源的列表。
-   对于任何 PRx 对象中标识的每个电源资源 \_ ，必须实现以下控制方法：

    -   \_关闭：将电源资源设置为 *关闭* 状态 (关闭资源) 。
    -   \_打开：将 "电源资源" 设置为 " *开启* " 状态 (资源) 。
    -   \_STA：此对象的计算结果为电源资源的当前 *开启* 或 *关闭* 状态 (0： off，1： on) 。

当 ACPI 在 \_ PR3 中列出的电源资源上运行 OFF 控制方法时，将发生到 D3cold 的转换 \_ 。 请注意，如果设备函数驱动程序指示支持 D3cold，此支持并不意味着所有转换到 D3 都将导致 swift 转换为 D3cold。 设备可能会长时间进入并保持 D3hot 状态，然后返回到 D0，而不会输入 D3cold，也不会在稍后输入 D3cold。

**父设备**

不要求父设备能够进行电源管理。 但是，如果父设备是电源管理的，则 Windows 将无法关闭此设备，前提是它的任何子 (依赖设备) 不在 D3 中。

**示例**

以下块示意图显示了在系统总线上 (标记为 **EMBD**) 的嵌入式设备。 可通过标记为 "**电源逻辑**" 的块单独开启和关闭设备的主电源 (**Vcc**) 和辅助电源 (**Vaux**) 。

![acpi 枚举的嵌入式设备](images/d3cold1.png)

下面的 ASL 代码示例说明了上图中嵌入式设备所使用的电源资源。 此示例从用于 \_ 描述设备驱动程序功能的 .osc 控制方法的声明开始。 接下来，已声明设备的两个电源资源-将资源名称 PVCC 和 PVAX 分配给设备的主要和辅助电源、 **Vcc** 和 **Vaux**。 最后，列出设备支持的每个设备电源状态的电源资源要求，并介绍设备的唤醒功能。

```asl
Scope (\_SB)
{
     Method(_OSC, 4, NotSerialized) // Platform-wide Capabilities Check.
     {  
          ... // This must indicate support for _PR3.
     }

     PowerResource(PVCC,0,0) // Power resource representing the main power for the device.
                             // Required for the device to be fully functional (D0).
     {
          Name(_STA,VAR1)        // Return the state of the power resource.
          Method(_ON,0x0) {...}  // Turn on the power resource and set VAR1 to 1.
          Method(_OFF,0x0) {...} // Turn off the power resource and set VAR1 to 0.
     }

     PowerResource(PVAX,0,0) // Power resource representing the auxiliary power for the device.
                             // Required for low-power, less-functional states (e.g., D3hot).
     {
          Name(_STA,VAR2)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     Device(EMBD) // An ACPI-enumerated device on the processor bus that supports D3Cold
     {
               Name(_HID, ...)
               ... // Other (non-power) objects for this device

          // Indicate support for D0.
               Name(_PR0, Package() {PVCC, PVAX}) // Power resources required for D0

          // Indicate support for D1 (optional)...

          // Indicate support for D2.
               Name(_PR2, Package() {PVCC, PVAX}) // If D2 is implemented in the hardware,
                                                  //  list the power resources needed by D2.
                                                  // If D2 is not implemented, list the same
                                                  //  resources as _PR3.

          // Indicate support for D3Cold.
               Name(_PR3, Package() {PVCC, PVAX}) // Power resource for D3. These will be 
                                                  //  turned off ONLY if drivers opt-in to D3cold.
 
          // Indicate support for wake. Required for entry into D3cold, even if the device doesn't
          // need or have a wake mechanism.
               Name(_S0W, 4) // The existence of this object indicates that the platform is
                             //  capable of handling wake events from this device while in S0. 
                             // The value of this object indicates the lowest D-state this device
                             //  can be in to trigger wake events that can be handled while the
                             //  platform is in S0.

          // Enable wake events (optional) 
          //  If this device actually does generate wake events, there must be a way for OSPM to
          //  enable and disable them. The mechanism for this depends on the platform hardware:
               /*
               Name(_PRW, ...) // If the event is signaled via a GPE bit (SCI) OR
                               //  if there are power resources required only for wake.
               Name(_CRS, ...) // If the event is signaled via a wake-capable interrupt.
                
               Method(_DSW, 3) {...) // Can be used with either of the above, if wake enablement
                                     // varies depending on the target S-state and D-state.
               */
     }  // End of Device EMBD
} End Scope \_SB
```

### <a name="case-2-an-embedded-device-is-bus-enumerated"></a>案例2：嵌入式设备已枚举总线

如果嵌入式设备符合公共总线规范（如 PCIe 或 USB），则可以通过总线定义的机制发现此设备，并且可以通过总线部分或全部提供电源。 如果此设备未通过其他 sideband 电源资源提供支持，则设备的主电源是将设备连接到父总线控制器的链接。 总线枚举设备可由 \_ 嵌入式设备的定义中的 ADR 对象标识。 \_ADR 对象用于向 OSPM 提供嵌入式设备父总线上设备的地址。 此地址用于将总线硬件) 所显示的设备 (的总线表示形式绑定到设备 (的平台表示形式，如 ACPI 固件) 所示。  (\_ ADR address 编码是特定于总线的。 有关详细信息，请参阅 \_ ACPI 5.0 规范中的 "ADR (Address) " 部分 ) 。在采用此机制的情况下，必须与父总线驱动程序协调 D3cold 支持。

如果嵌入式设备的主电源是将此设备连接到其父总线的链接，则将设备放置在 D3cold 中的关键要求是关闭该链接。 有关转换到 D3cold 的详细信息，请参阅处于 [设备电源状态](../kernel/device-power-states.md)的状态图。

**平台固件**

OSPM 使用 \\ \_ SB。 \_.OSC 将平台范围内的 OSPM 功能传递到平台固件。 平台固件必须在 SB 中设置第2位 \\ \_ 。 \_.OSC 返回值，指示 OSPM 设备支持 \_ PR3。 有关详细信息，请参阅 ACPI 5.0 规范中的 6.2.10.2 "平台范围内的 OSPM 功能" 部分。

**嵌入式设备**

不需要 D3cold 特定的 ACPI 更改。 在这种情况下，只要设备驱动程序和平台指示了对 D3cold 的支持，当父总线退出 D0 并进入低功耗状态 Dx 时，就可以关闭向嵌入式设备提供电源的总线链接。 从链接中删除 power 时，会发生从 D3hot 到 D3cold 的嵌入式设备的转换。 父总线输入的 Dx 状态可以是导致链接电源源关闭的任何状态。

**父设备**

父总线的 ACPI 描述符必须执行以下操作：

-   \_ (Dx) 实现 S0W。 此对象将 Dx 指定为在系统处于 S0 状态时，子 (嵌入) 设备可以唤醒的最小电源 D 状态。

-   定义电源资源以表示将 (嵌入) 设备的子节点连接到父总线的链接。 此外， \_ \_ \_ 应为此电源资源定义 ON、OFF 和 STA 对象。 此列表后面的 ASL 代码示例介绍了 PVC1 和 PVX1 这两个资源的链接能力。 每个资源、 \_ ON、 \_ OFF 和 \_ STA 对象均已定义。

-   如果 "Dx" (最小电源 D 状态，则为;请参阅) 为 D3cold 的第一个列表项，提供 \_ PR3 对象，该对象包括子 (embedded) 设备需要用于 D3hot (例如，Vcc 和 Vaux) 的电源资源。 如果 D0、D2 和 D3hot 需要相同的电源，则 \_ PR0、 \_ pr2) 和 \_ PR3 都指定相同的电源资源。 仅当子设备进入 D3cold 时，才会关闭这些资源。

    由于历史原因， \_ 无论何时存在 PR0，Windows 都需要 pr2) \_ 。 如果在硬件中实现了 D2， \_ pr2) 会列出 d2 所需的电源资源。 如果未实现 D2， \_ pr2) 会列出与 PR0 相同的资源 \_ 。

-   实现 \_ PR0。 \_父总线的 PR0 对象中的资源列表应包括用于将父总线连接到子 (嵌入) 设备的链接的资源。

**示例**

以下块图中的示例硬件配置显示了可为 PCIe 设备启用 D3cold 的两种不同方式。 首先，标记为 " **ENDP** " 的终结点 () 连接到 pcie 根端口 (**为 rp01**) 并通过 **PCIe 链接**从其父设备接收辅助电源。 其次，关系图中的 **HD 音频** 设备没有到其父设备的标准链接 (标记为 " **PCI0** " 的 PCI 控制器) ，因此建模方式类似于 ACPI 枚举的事例。

![总线枚举的嵌入式设备](images/d3cold2.png)

此图中的 **为 rp01** 设备有一个主电源、 **Vcc1**和一个辅助电源源 **Vaux1**。 同样， **HD 音频** 设备具有主电源、 **Vcc2**和辅助电源 **Vaux2**。

以下 ASL 代码描述了父总线控制器 (**PCI0**) ，以及上图中显示的 **ENDP** 和 **HD 音频** 设备所需的电源资源。

```asl
Scope (\_SB)
{
     Method(_OSC, 4, NotSerialized) // Platform-wide Capabilities Check.
     {  
          ... // This must indicate support for _PR3.
     }

     PowerResource(PVC1,0,0) // Power resource representing Vcc1 for the RP01 device.
                             // Required for the device(s) to be fully functional (D0).
     {
          Name(_STA,VAR0)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     PowerResource(PVX1,0,0) // Power resource representing Vaux1 for the RP01 device.
                             // Required for low-power, less-functional states (e.g., D3hot).
     {
          Name(_STA,VAR1)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     PowerResource(PVC2,0,0) // Power resource representing Vcc2 for the HD device.
                             // Required for the device(s) to be fully functional (D0).
     {
          Name(_STA,VAR2)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     PowerResource(PVX2,0,0) // Power resource representing Vaux2 for the HD device.
                             // Required for low-power, less-functional states (e.g., D3hot).
     {
          Name(_STA,VAR3)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     ... // Power resources for other child devices

     Device(PCI0) // The PCI root complex
     {
          Name(_HID, EISAID("PNP0A08"))  // ACPI enumerated
          Method(_OSC, 4, NotSerialized) // PCIe-specific Capabilities Check.
          {     
               ... // This must support hand-off of PCIe control to the OS.
          }
          ... // Other (non-power) objects for this device

          Device(RP01) // PCIe Root Port 1
          {
                    Name(_ADR, "...") // Bus enumerated
                    ... // Other (non-power) objects for this device
    
               // Indicate support for D0.
                    Name(_PR0, Package() {PVC1, PVX1}) // Power resources required for D0.
                                                       // Includes the Link Power for ENDP.

               // Indicate support for D1 (optional)...

               // Indicate support for D2.
                    Name(_PR2, Package(){PVC1, PVX1}) 

               // Indicate support for wake. Required for entry into D3cold, even if the
               // device doesn't need or have a wake mechanism.
                    Name(_S0W, 4) // The existence of this object indicates the platform
                                  //  is capable of handling wake events from this device
                                  //  while the platform is in S0. 
                                  // The value of this object indicates the lowest D-state
                                  //  this device can be in to trigger wake events that 
                                  //  can be handled while the platform is in S0.

               // Enable wake events (optional) 
               //  If this device actually does generate wake events, there must be a way
               //  for OSPM to enable and disable them. The mechanism for this depends on
               //  the platform hardware:

                    /*
                    Name(_PRW, ...) // If the event is signaled via a GPE bit (SCI) OR
                                    //  if there are power resources required only for wake.
                    Name(_CRS, ...) // If the event is signaled via a wake-capable interrupt.

                    Method(_DSW, 3) {...) // Can be used with both of the above, if wake
                                          //  enablement varies depending on the target 
                                          //  S-state and D-state.
                    */

                    Device(ENDP) // This device supports D3cold. No power-related objects
                                 // are required.
                    {
                         Name(_ADR, "...")  // Bus enumerated
                         ... // Other (non-power) objects
                    }  // End of Device ENDP
          }  // End of Device RP01

          Device(HD) // A PCIe Bus0 device (HD Audio) that supports D3cold. Note that
                     //  this case is modeled similar to the ACPI-enumerated case
                     //  because device HD has no standard link to its parent.
          {
                    Name(_ADR, "...") // Bus enumerated
                    ... // Other (non-power) objects for this device
    
               // Indicate support for D0.
                    Name(_PR0, Package() {PVC2, PVX2}) // Power resources required for D0
                            
               // Indicate support for D1 (optional)...

               // Indicate support for D2.
                    Name(_PR2, Package(){PVC2, PVX2})

               // Indicate support for D3Cold.
                    Name(_PR3, Package() {PVC2, PVX2}) // Power resource for D3; These will
                                                       //  be turned off ONLY if drivers
                                                       //  opt-in to D3cold.
 
               // Indicate support for wake. Required for entry into D3cold, even if the
               // device doesn't need or have a wake mechanism.
                    Name(_S0W, 4) // The existence of this object indicates that the platform
                                  //  is capable of handling wake events from this device 
                                  //  while the platform is in S0. 
                                  // The value of this object indicates the lowest D-state
                                  //  this device can be in to trigger wake events that can
                                  //  be handled while the platform is in S0.

               // Enable wake events (optional). 
               //  If this device actually does generate wake events, there must be a way for
               //  OSPM to enable and disable them. The mechanism for this depends on the HW:
                    /*
                    Name(_PRW, ...) // If the event is signaled via a GPE bit (SCI) OR
                                    //  if there are power resources required only for wake.
                    Name(_CRS, ...) // If the event is signaled via a wake-capable interrupt.

                    Method(_DSW, 3) {...) // Can be used with both of the above, if wake
                                          //  enablement varies depending on the target
                                          //  S-state and D-state.
                    */
          }  // End Device HD

          ... // Device objects for other child devices

     }  // End Device PCI0
}  // End Scope \_SB
```

### <a name="other-possibilities"></a>其他可能性

可以结合使用上述两个示例中所示的方法来支持同时使用总线电源和 sideband 功能的配置。

## <a name="device-driver-requirements"></a>设备驱动程序要求


设备的电源策略所有者通常 (功能驱动程序) 通知操作系统是否允许设备从 D3hot 转换为 D3cold。 驱动程序可在安装设备的 INF 文件中提供此信息。 或者，驱动程序可以在运行时调用 [*SetD3ColdSupport*](/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support) 例程，以动态地启用或禁用设备到 D3cold 的转换。 通过使设备进入 D3cold，驱动程序可保证以下行为：

-   当计算机停留在 S0 中时，设备可以容忍从 D3hot 到 D3cold 的转换。
-   当设备从 D3cold 返回到 D0 时，它将正常工作。

输入 D3cold 后，无法满足任一要求的设备可能会在计算机重新启动或进入睡眠状态之后才可用。 如果设备必须能够从其输入的任何低功耗 Dx 状态向唤醒事件发出信号，则除非驱动程序确定设备的唤醒信号在 D3cold 中起作用，否则不能启用条目进入 D3cold。

有关详细信息，请参阅 [支持驱动程序中的 D3cold](../kernel/supporting-d3cold-in-a-driver.md)。

 

