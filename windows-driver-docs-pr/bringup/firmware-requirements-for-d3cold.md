---
title: D3cold 固件要求
description: 从 Windows 8 开始，设备可以输入 D3cold 电源子状态甚至时系统将保留在 S0 电源状态。
ms.assetid: 4BADC310-CC53-4084-A592-66197C348279
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff10d3af3c23cf857e2e68f772bfeacc59683d03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338675"
---
# <a name="firmware-requirements-for-d3cold"></a>D3cold 固件要求


从 Windows 8 开始，设备可以输入 D3cold 电源子状态甚至时系统将保留在 S0 电源状态。 本主题介绍实现 D3cold 要求支持嵌入式设备的固件。 下面的讨论旨在帮助固件开发人员，使其嵌入的设备能够可靠地进入和退出 D3cold。

此外，设备驱动程序要求，以支持 D3cold 简要讨论了。 D3cold 的设备驱动程序支持的详细信息，请参阅[驱动程序中支持 D3cold](https://msdn.microsoft.com/library/windows/hardware/hh967717)。

## <a name="introduction"></a>简介


[设备的电源状态](https://msdn.microsoft.com/library/windows/hardware/ff543162)在 ACPI 规范中，并在各种总线规范中定义。 PCI 总线规范，因为它引入了 PCI 电源管理，拆分为两种子状态，D3hot 和 D3cold D3 (off) 设备电源状态。 这一区别是添加到 ACPI 3.0 中的 ACPI 规范，并在 ACPI 4.0 中扩展。 Windows 始终支持两种 D3 子状态，但 Windows 7 和更早版本的 Windows 支持 D3cold 子状态仅当整个计算机退出 S0 （工作） 系统电源状态进入睡眠或休眠状态 — 通常 S3 和 S4。 从 Windows 8 开始，设备驱动程序可以启用其设备，以便即使系统处于 S0 输入 D3cold 状态。

D3hot，通常只需调用"D3"，是设备的"软关闭"状态。 在此状态下，总线扫描速度，可以检测到该设备并发送到设备的命令可能会导致它幂上再次。 在 D3cold，所有电源都删除，使用少量的能力，能够促成设备的唤醒逻辑的可能异常。 例如，对于 PCI Express (PCIe) 的设备，主要设备电源，Vcc，经常已关闭到 D3cold 转换中。 关闭 Vcc 可以降低功率消耗和扩展移动硬件平台可以在电池电量运行的时间。 D3cold 设备时，它不能检测到的总线扫描并不能接收命令。 还原 Vcc power 将设备移到通常等效于 D0 状态未初始化状态。 软件必须重新初始化该设备以将其放入工作状态。

将设备放入 D3cold 不一定意味着，已删除的电源与设备的所有源 — 它只意味着主要的电源，Vcc，已都移除。 如果不需要唤醒逻辑，辅助的电源，Vaux，也可能会被删除。 但是，可能需要发出信号将唤醒事件发送到处理器的设备必须能够绘制能力不足以运行唤醒逻辑。 例如，删除其主电源源以太网网络接口卡 (NIC) 可能会从以太网电缆获得足够的电力。 或者，可能会在其中用例 PCIe 接口可以完全关闭的 PCIe 接口之外的源提供 Wi-fi NIC 的备用电源。

在下面的讨论，一组要求启用设备电源状态转换为 D3cold 的描述。 这些要求划分为以下两个类别：

-   固件和平台要求
-   设备驱动程序要求

这两个类别的第一个是在本文的重点。 显示第二个类别的简要概述。 有关设备驱动程序要求的详细信息，请参阅[驱动程序中支持 D3cold](https://msdn.microsoft.com/library/windows/hardware/hh967717)。

## <a name="firmware-and-platform-requirements"></a>固件和平台要求


在下面的讨论，启用 D3cold 的固件和平台要求仅供这两种情况：

-   当在 ACPI 枚举设备。
-   当枚举设备时由其父总线。

以下讨论的大多数是特定于 PCIe。 但是，很大程度上此处所述的一般原则适用于其他总线还。

提取某些详细信息，通过重新将 Vcc power 应用于嵌入式设备触发从 D3cold 到 D0 的转换。 重新应用电源有效地将设备的连接还原到总线。 Windows 读取设备的标识符，以便区分以下两种情况：

-   删除并替换为另一台设备的设备。
-   在同一设备已删除并随后重新插入。

如果标识符匹配，将设备驱动程序重新初始化该设备。 如果标识符不匹配，Windows 将卸载设备驱动程序，并生成一个新的驱动程序堆栈的新设备。 PCIe，例如，供应商 ID、 设备 ID 和子系统 Id （它被拆分为子设备和子供应商的 Id，在某些版本的规范） 的查询。 这些标识符必须与匹配以前连接的设备的后 power 是重新应用 （以及的总线指定等待时间到期）;否则，Windows 将考虑新的设备，使其不同于上一个。

### <a name="case-1-an-embedded-device-is-enumerated-in-acpi"></a>案例 1：嵌入式的设备会在 ACPI 枚举

如果嵌入式的设备不是通过如 PCIe 或 USB、 总线规范所定义的机制可发现，但设备永久连接 (或至少连接专用于已知的设备)，此设备可以通过在平台固件中所述ACPI \_HID 和/或\_CID 对象。 这些对象使设备能够通过 OSPM 枚举。 （"OSPM"是 ACPI 规范中定义的术语。 这意味着，松散，"不是固件的软件。"）OSPM 枚举设备，仅当没有总线枚举器可以检测设备 id。 例如，通过 OSPM 枚举 ISA 总线上的设备。 此外，通过 ACPI 因为它们位于非可枚举 fabric 通常枚举芯片 (SoC) 上的系统上的设备。 此类设备的示例包括 USB 和 SD 主机控制器。

**平台固件**

使用 OSPM \\ \_SB.\_OSC 来传达对平台固件平台范围 OSPM 功能。 平台固件必须设置中的 2 位\\ \_SB.\_OSC 返回值以指示设备是否支持在 OSPM \_PR3。 有关详细信息，请参阅 ACPI 5.0 规范的第 6.2.10.2，"平台范围 OSPM 功能"部分。

**嵌入式的设备 – 仅通过 ACPI 发现**

若要支持 D3cold，平台固件应实现嵌入式设备的下列 ACPI power 资源对象：

-   \_PR0:此对象的计算结果为 D0 （完全启用） 设备电源状态的设备的电源需求。 返回值为 D0 状态所需设备的 power 资源的列表。
-   \_PR2:此对象的计算结果为 D2 设备电源状态的设备的电源需求。 返回值为设备 D2 状态所需的电源资源的列表。 请注意，出于历史原因，Windows 应\_PR2 时必须存在\_PR0 是否存在。 如果在硬件中实现 D2 \_PR2 列出了所需的 D2 power 资源。 如果未实现 D2， \_PR2 列出了与相同的资源\_PR0。
-   \_PR3:此对象的计算结果为 D3hot 设备电源状态的设备的电源需求。 返回值为 D3hot 状态所需设备的 power 资源的列表。
-   每个 power 资源中任何标识\_PRx 对象时，必须实现以下控制方法：

    -   \_关闭：设置为 power 资源*关闭*状态 （电源禁用了资源）。
    -   \_打开：设置为 power 资源*上*状态 （在资源上的电源）。
    -   \_STA:此对象的计算结果为当前*上*或*关闭*power 资源的状态 (0： 关闭，1： 上)。

ACPI 运行时，会发生转换到 D3cold\_中列出的电源资源 OFF 控件方法\_PR3。 请注意，是否设备功能驱动程序指示对 D3cold 的支持，这种支持并不意味着所有转换到 D3 都导致 swift 将转换为 D3cold。 可能的设备进入和长时间处于 D3hot，然后返回到 D0 而无需不断输入 D3cold，或在更高版本时将进入 D3cold 它。

**父设备**

没有父设备，才能成为电源管理的要求。 但是，如果父设备电源管理，Windows 永远不会为提供支持向下此设备如果任何子项 （依赖于设备） 不在 D3。

**示例**

以下块图显示了嵌入式的设备 (标有**EMBD**) 系统总线上。 主电源 (**Vcc**) 和辅助电源 (**Vaux**) 到设备都可以独立打开和关闭块标记为通过**Power 逻辑**。

![acpi 枚举的嵌入式的设备](images/d3cold1.png)

下面的 ASL 代码示例介绍了使用的嵌入式设备上图中的 power 资源。 此示例开头的声明\_OSC 控件方法描述的设备驱动程序的功能。 接下来，声明此设备的两个电源资源 — PVCC 和 PVAX 分配给设备的主要和辅助电源，资源名称**Vcc**并**Vaux**。 最后，对设备支持，每个设备电源状态列出的电源资源要求和设备的唤醒功能进行了介绍。

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

### <a name="case-2-an-embedded-device-is-bus-enumerated"></a>情况 2：嵌入式的设备是总线枚举

如果嵌入式的设备符合公共总线规范，如 PCIe 或 USB，此设备是通过总线定义的机制，可发现并 power 可以提供部分或全部通过总线。 如果此设备不由其他旁带 power 资源提供支持，设备的主电源源是将设备连接到父总线控制器的链接。 总线枚举设备可以通过标识\_ADR 嵌入式的设备的定义中的对象。 \_ADR 对象用于 OSPM 提供嵌入式的设备的父总线上设备的地址。 此地址用于为设备 （如所示的 ACPI 固件） 的平台的表示形式将关联的设备 （如所示的总线硬件） 总线的表示形式。 ( \_ADR 地址编码是特定于总线的。 有关详细信息，请参阅 6.1.1 节"\_ADR （地址）"，在 ACPI 5.0 规范中。)采用这种机制时, D3cold 支持必须与父总线驱动程序相协调。

如果嵌入式设备的主电源是将此设备连接到其父总线的链接，将设备放入 D3cold 的关键要求是能耗更低的链接。 有关过渡到 D3cold 的详细信息，请参阅中的状态关系图[设备的电源状态](https://msdn.microsoft.com/library/windows/hardware/ff543162)。

**平台固件**

使用 OSPM \\ \_SB.\_OSC 来传达对平台固件平台范围 OSPM 功能。 平台固件必须设置中的 2 位\\ \_SB.\_OSC 返回值以指示设备是否支持在 OSPM \_PR3。 有关详细信息，请参阅 ACPI 5.0 规范的第 6.2.10.2，"平台范围 OSPM 功能"部分。

**嵌入式的设备**

不不需要任何特定于 D3cold 的 ACPI 更改。 在这种情况下，只要设备驱动程序和平台已表明对 D3cold 的支持，提供到嵌入式设备的电源的总线链接可以关闭时父总线退出 D0 并进入低功耗状态 Dx。 Power 删除从链接时发生转换到 D3cold D3hot 从嵌入式设备。 父总线进入的 Dx 状态可以是任何会导致链接电源关闭的状态。

**父设备**

父总线的 ACPI 描述符必须执行以下操作：

-   实现\_S0W(Dx)。 此对象指定 Dx 作为子 （嵌入） 设备可以从其唤醒系统处于 S0 状态时的最低功率 D 状态。

-   定义 power 资源来表示将子 （嵌入） 设备连接到父总线的链接。 此外， \_ON， \_OFF，和\_STA 对象应为此电源资源定义。 此列表后面的 ASL 代码示例描述为两个资源，PVC1 和 PVX1 链接电源。 这些资源的每个\_ON， \_OFF，和\_STA 对象定义的。

-   如果"Dx"（最低电源 D 状态，请参见第一个列表项），D3cold 提供\_PR3 对象包含子 （嵌入） 设备 （例如，Vcc 和 Vaux） 需要 D3hot power 资源。 如果同一个电源和所需 D0，D2，D3hot，然后\_PR0， \_PR2，和\_PR3 所有指定的同一 power 资源。 仅当子设备进入 D3cold 关闭这些资源。

    由于历史原因，Windows 应\_PR2 时必须存在\_PR0 是否存在。 如果在硬件中实现 D2 \_PR2 列出了所需的 D2 power 资源。 如果未实现 D2， \_PR2 列出了与相同的资源\_PR0。

-   实现\_PR0。 中的资源的列表\_父总线 PR0 对象应包含 power 父总线连接到子 （嵌入） 设备的链接的资源。

**示例**

以下块图中的示例硬件配置显示了可以为 PCIe 设备启用 D3cold 的两种不同方式。 首先，终结点 (标有**ENDP**) 连接到 PCIe 根端口 (**为 RP01**)，并从通过其父设备接收辅助电源**PCIe 链接**。 第二个， **HD Audio**关系图中的设备有没有标准链接到其父设备 (标记为 PCI 控制器**PCI0**)，在因此模型到 ACPI 枚举用例中与此类似。

![总线枚举的嵌入式的设备](images/d3cold2.png)

**为 RP01**在此图中的设备已在主电源**Vcc1**，和辅助电源源**Vaux1**。 同样， **HD Audio**设备具有在主电源**Vcc2**，和辅助电源源**Vaux2**。

下面的 ASL 代码描述父总线控制器 (**PCI0**) 和所需的电源资源**ENDP**并**HD Audio**设备上图中所示。

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

### <a name="other-possibilities"></a>其他可能的情况

可以组合两个前面的示例中所示的技术来支持使用总线能源和旁带能源的配置。

## <a name="device-driver-requirements"></a>设备驱动程序要求


设备 （通常是功能驱动程序） 的电源策略所有者告知操作系统是否启用从 D3hot D3cold 到的设备的转换。 该驱动程序可以提供此信息在安装设备的 INF 文件中。 或者，驱动程序可以调用[ *SetD3ColdSupport* ](https://msdn.microsoft.com/library/windows/hardware/hh967716)在运行时动态地启用或禁用设备的转换为 D3cold 例程。 通过启用设备输入 D3cold，驱动程序可保证以下行为：

-   在计算机保留在 S0 中时，设备可以容忍 D3hot 从转换到 D3cold。
-   从 D3cold 恢复 D0 时，设备将正常工作。

设备不能满足任一要求，输入 D3cold 后, 可能不可用之前在计算机重新启动或进入休眠状态。 如果设备必须能够从进入任何低功耗 Dx 状态信号发生唤醒事件，进入 D3cold 必须未启用除非驱动程序为特定设备的唤醒信号，将在 D3cold 中正常工作。

有关详细信息，请参阅[驱动程序中支持 D3cold](https://msdn.microsoft.com/library/windows/hardware/hh967717)。

 

 




