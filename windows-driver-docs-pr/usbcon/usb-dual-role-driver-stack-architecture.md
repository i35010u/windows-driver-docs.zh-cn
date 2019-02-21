---
Description: USB Dual Role controllers are now supported in Windows, starting with Windows 10.
title: USB 双角色驱动程序堆栈体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81c90f96a756d3003711c08f3320a1e076990939
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545925"
---
# <a name="usb-dual-role-driver-stack-architecture"></a>USB 双角色驱动程序堆栈体系结构


**上次更新时间**

-   2015 年 11 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

在 Windows 中，从 Windows 10 开始中现在支持 USB 双角色控制器。

## <a name="introduction"></a>简介


USB 双角色功能可以系统不是 USB*设备*或 USB*主机*。 可以位于 USB 双角色的详细的规范[usb.org](http://www.usb.org/developers/wusb/docs/presentations/2006/Taipei06_SA_SBD_DRD_Design_Considerations.pdf)网站。

这里的重要一点是双角色功能，允许移动设备，如手机、 平板手机或平板电脑，可将自身指定为设备或主机。

当移动设备处于*函数*模式下，附加到一台 PC 或某些其他设备，它作为连接的移动设备的主机。

当移动设备处于*主机*模式下，用户可以将其设备，例如鼠标或键盘，附加到它。 在这种情况下在移动设备承载附加的设备。

通过为 Windows 10 中的 USB 双角色提供支持，我们提供以下优势：

-   连接到移动外围设备通过 USB，它提供了更大数据带宽相比无线协议，如蓝牙。
-   电池充电通过 USB 连接到时以及 （只要存在所需的硬件支持是） 与其他 USB 设备通信的选项。
-   启用将很可能拥有其所有工作的智能手机等移动设备的客户。 此功能将允许在有线停靠方案中，移动设备将停靠，因此承载外围设备提高工作效率。

下表显示的列表*主机*类桌面和移动 Windows Sku 可用的驱动程序。

| USB 主机类驱动程序                                             | Windows 10 移动版 | Windows 10 桌面版 |
|--------------------------------------------------------------------|-------------------|---------------------------------|
| USB 集线器 (USBHUB)                                                  | 是               | 是 （自 Windows 2000)        |
| HID-键盘/鼠标 （HidClass、 KBDCLass、 MouClass、 KBDHid、 MouHid） | 是               | 是 （自 Windows 2000)        |
| USB 大容量存储 （大容量和 UASP）                                     | 是               | 是 （自 Windows 2000)        |
| 泛型 USB 主机驱动程序 (WinUSB)                                   | 是               | 是 （自 Windows Vista)       |
| USB 音频输入 / 输出 (USBAUDIO)                                      | 是               | 是 （自 Windows XP)          |
| 串行设备 (USBSER)                                            | 是               | 是 （自 Windows 10)          |
| 蓝牙 (BTHUSB)                                                 | 是               | 是 （自 Windows XP)          |
| 打印 (usbprint)                                                   | 否                | 是 （自 Windows XP)          |
| 扫描 (USBSCAN)                                                 | 否                | 是 （自 Windows 2000)        |
| 网络摄像头 (USBVIDEO)                                                  | 否                | 是 （自 Windows Vista)       |
| 媒体传输协议 （MTP 发起程序）                            | 否                | 是 （自 Windows Vista)       |
| 远程 NDIS (RNDIS)                                                | 否                | 是 （自 Windows XP)          |
| 通过 USB (IPoverUSB) 的 IP                                            | 否                | 是 （新于 Windows 10）        |



根据设备类遥测数据，并根据选择适用于 Windows 10 的关键方案选择表中的类驱动程序。 我们计划提供有限的数量的收件箱，第三方主机驱动程序，以支持 Windows 10 移动版上的主要设备。 将适用于桌面版本的 Windows 10，这些驱动程序提供的 OEM 网站上或通过 Windows Update (WU)。

适用于 Windows 10 移动设备，不包括收件箱的第三方驱动程序将不可用 WU 上。 而保留的 USB 主堆栈 + hid 标准的磁盘占用空间小。 这是为什么不是所有类驱动程序和很少第三方驱动程序包括针对 Windows 10 移动版收件箱。 想要使第三方驱动程序可用的 OEM 可以使用看板支持包 (BSP) 将它们添加到其移动设备的操作系统映像。 有关此策略的详细信息，请参阅[驱动程序开发的 Windows Phone](https://go.microsoft.com/fwlink/p/?LinkId=761246)，并向下的滚动到节*驱动程序开发的 Windows Phone 和 Windows 之间的差异*。

下表显示*函数*类 Windows 移动 Sku 可用的驱动程序。

**请注意**函数的驱动程序*不*可在 Windows 10 的桌面版本中。



| USB 函数类驱动程序                 | Windows 10 移动版 | Windows 10 桌面版 | 注释                                                                                                                                  |
|--------------------------------------------|-------------------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 媒体传输协议 （MTP 响应方）    | 是               | 否                              | 没有在桌面上 MTP 响应程序方案。 P2P 桌面系统之间的情况下已启用通过 Easy MigCable WinUSB 转移。 |
| Out (vidstream) 的视频显示              | 是               | 否                              |                                                                                                                                        |
| 泛型 USB 功能驱动程序 (GenericUSBFn) | 是               | 否                              | 这将需要通过 IPoverUSB 和其他桌面闪烁的方案。                                                                 |



我们将监视设备附件的数据，让我们知道是否我们需要提供其他类驱动程序支持，并为设备类受欢迎程度列表发生变化时。

## <a name="driver-implementation"></a>驱动程序实现


Microsoft USB 角色切换 (URS) 驱动程序允许系统实施者可以利用其平台的双角色 USB 功能。

URS 驱动程序旨在为使用可以在主机和外围角色在单个端口上运行的单个 USB 控制器的平台提供双角色功能。 *外围角色*也称为*函数角色*。 URS 驱动程序管理当前角色的端口，并加载和卸载的适当的软件堆栈，基于硬件的平台的事件。

在系统上具有 USB 微 AB 连接器，驱动程序，可以使用的硬件中断指示状态的连接器上的 ID pin。 此 pin 用于检测是否在控制器需要假设主机角色，或者在连接中的函数角色。 有关详细信息，请参阅[USB 在外出时随时规范](https://go.microsoft.com/fwlink/p/?LinkId=698414)。 在系统上使用 USB 类型 C 连接器，OEM 实施者应使用提供的连接器客户端驱动程序[USB 类型 C 连接器驱动程序的编程接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)。 客户端驱动程序如 CC 检测、 PD 消息传递，以及其他与 Microsoft 提供的 USB 连接器管理器类扩展 (UcmCx) 来管理的 USB 类型 C 连接器的所有方面进行通信。 对于角色切换，客户端驱动程序通信的 USB 类型 C 连接器向 URS 驱动程序的状态。

下图显示了使用 URS 驱动程序的双角色控制器 USB 软件驱动程序堆栈。

![usb 角色切换驱动程序堆栈体系结构。 ](images/dual-role-arch.png)

请注意，URS 驱动程序将永远不会加载同时在上图中所示的函数和主机堆栈。 URS 驱动程序将加载*任一*函数堆栈*或*主机 stack-具体取决于 USB 控制器的角色。

## <a name="hardware-requirements"></a>硬件要求


如果你正在开发一个平台，它将利用 URS 驱动程序，以提供双角色 USB 功能，以下硬件要求必须满足：

-   USB 控制器

    作为现成驱动程序，由 Microsoft 提供这些驱动程序。

    Synopsys DesignWare 核心 USB 3.0 控制器。 收件箱 INF:UrsSynopsys.inf。

    Chipidea 高速 USB OTG 控制器。 收件箱 INF:UrsChipidea.inf。

-   ID pin 中断

    非 USB 类型-C 系统 ID pin interrupt(s) 可能在两种方式之一实现：

    两个边缘触发中断： 接地连接器上的 ID pin 时, 激发的一个，浮点 ID pin 时激发的另一个。

    单个同时处于活动状态的中断时在活动级别 ID 插针接地。

-   USB 控制器枚举

    USB 双角色控制器必须是 ACPI 枚举。

-   软件的支持

    URS 驱动程序需要允许 VBus 控制连接器软件界面。 此接口是特定于 SoC 的。 有关详细信息，请与 SoC 供应商联系。

在 Windows 中不支持这些 USB OTG 功能：

-   附件充电器适配器检测 (ACA)。
-   会话请求协议 (SRP)。
-   主机协商协议 (HNP)。
-   将附加检测协议 (ADP)。

## <a href="" id="acpi"></a>系统配置


若要使用 URS 驱动程序，必须为您的系统中创建的 ACPI 定义文件。 此外，还有一些必须考虑到帐户的驱动程序相关注意事项。

下面是 USB 双角色控制器的示例 ACPI 定义。

```Text
//
// You may name the device whatever you want; we don&#39;t depend on it being called &#39;URS0&#39;.
//
Device(URS0)
{
    //
    // Replace with your own hardware ID. Microsoft will add it to the inbox INF,
    // or you may choose to author a custom INF that uses Needs & Includes directives
    // to include sections from the inbox INF.
    //
    Name(_HID, "ABCD1234")

    Name(_CRS, ResourceTemplate() {
        //
        // The register space for the controller must be defined here.
        //
        Memory32Fixed(ReadWrite, 0xf1000000, 0xfffff)


        //
        // The ID pin interrupts, if you are using two edge-triggered interrupts.
        //
        GpioInt(Edge, ActiveHigh, Exclusive, PullUp, 0, "\\_SB.GPI0", 0, ResourceConsumer, , ){0x1001}
        GpioInt(Edge, ActiveHigh, Exclusive, PullUp, 0, "\\_SB.GPI0", 0, ResourceConsumer, , ){0x1002}

        //
        // Following is an example of a single active-both interrupt.
        //
        // GpioInt(Edge, ActiveBoth, Exclusive, PullUp, 0, "\\_SB.GPI0", 0, ResourceConsumer, , ){0x12}
        //

        //
        // For a Type-C platform, you do not need to specify any interrupts here.
        //
    })

    //
    // This child device represents the USB host controller. This device node is in effect
    // when the controller is in host mode.
    // You may name the device whatever you want; we don&#39;t depend on it being called &#39;USB0&#39;.
    //
    Device(USB0)
    {
        //
        // The host controller device node needs to have an address of &#39;0&#39;
        //
        Name(_ADR, 0)
        Name(_CRS, ResourceTemplate() {

            //
            // The controller interrupt.
            //
            Interrupt(ResourceConsumer, Level, ActiveHigh, Exclusive, , , ){0x10}
        })
    }

    //
    // This child device represents the USB function controller. This device node is in effect
    // when the controller is in device/function/peripheral mode.
    // You may name the device whatever you want; we don&#39;t depend on it being called &#39;UFN0&#39;.
    //
    Device(UFN0)
    {
        //
        // The function controller device node needs to have an address of &#39;1&#39;
        //
        Name(_ADR, 1)
        Name(_CRS, ResourceTemplate() {

            //
            // The controller interrupt (this could be the same as the one defined in
            // the host controller).
            //
            Interrupt(ResourceConsumer, Level, ActiveHigh, Exclusive, , , ){0x11}
        })
    }
}
```

下面是一些了 ACPI 文件的主要部分的说明：

-   URS0 是 USB 双角色控制器的 ACPI 定义。 这是 URS 驱动程序将加载在其的 ACPI 设备。

-   USB0 和 UFN0 URS0 的范围内的子设备。 USB0 和 UFN0 分别表示将枚举由 URS 驱动程序的两个子堆栈和主机和函数堆栈。 请注意， \_ADR 是 ACPI 与 URS 驱动程序创建的设备对象与这些设备定义相匹配的方法。

-   如果控制器使用两个角色相同的中断，可以在这两个子设备中所述相同的控制器中断。 甚至在这种情况下，中断可以仍描述为"独占"。

-   可以根据需要将此 ACPI 定义文件的新增功能。 例如，您可以设置任何其他必需的方法或属性的任何设备上的 ACPI 定义文件中。 这种添加不会干扰 URS 驱动程序的操作。 也可以在描述中堆栈的任何所需的任何其他资源\_CRS 的适当的设备。

URS 驱动程序将硬件 Id 分配给主机和函数堆栈。 这些硬件 Id 派生自 URS 设备的硬件 ID。 例如，如果 URS 设备硬件 ID 是 ACPI\\ABCD1234，然后 URS 驱动程序硬件 Id 为创建的主机和函数的堆栈，如下所示：

-   主机堆栈：URS\\ABCD1234&HOST

-   函数堆栈：URS\\ABCD1234 &AMP; 函数

## <a href="" id="inf"></a>驱动程序安装包


第三方驱动程序包可以依赖于此方案中，如有必要。

如果你是 IHV 或 OEM 并提供你自己的驱动程序包正在考虑，以下是一些要考虑的事项：

- URS 驱动程序包

  预计每个平台上的双角色控制器则硬件 ID 将收件箱 INF 添加为 URS。 但是，如果出于某种原因无法添加 ID，IHV/OEM 可能会提供一个驱动程序包使用 INF 需要 / 包括收件箱 INF 并匹配其硬件 id。

  这是在其中 IHV/OEM 需要筛选器驱动程序位于驱动程序堆栈的情况下必需的。

- 主机驱动程序包。

  IHV/OEM 提供的驱动程序包需要 / 包括收件箱*usbxhci.inf*和主机设备硬件 ID 是必需的匹配项。 硬件 ID 匹配项将基于在上一部分中所述的方案。

  这是在其中 IHV/OEM 需要筛选器驱动程序位于驱动程序堆栈的情况下必需的。

  没有正在进行的工作，使 URS 驱动程序分配主机设备 XHCI 兼容 ID。

- 函数驱动程序包

  IHV/OEM 提供的驱动程序包需要 / 包括收件箱*Ufxsynopsys.inf*和外围设备硬件 ID 是必需的匹配项。 硬件 ID 匹配项将基于在上一部分中所述的方案。

  IHV/OEM 还可以在驱动程序包中包含的筛选器驱动程序。
  ## <a name="see-also"></a>另请参阅

[双角色控制器驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#dual-role-controller-driver-reference)






