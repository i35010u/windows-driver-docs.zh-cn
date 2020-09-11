---
description: 从 Windows 10 开始，Windows 现在支持 USB 双重角色控制器。
title: USB 双角色驱动程序堆栈体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2748df15bf673901b0520158bc187c7855b6d34
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010063"
---
# <a name="usb-dual-role-driver-stack-architecture"></a>USB 双角色驱动程序堆栈体系结构


**上次更新时间**

-   2015 年 11 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

从 Windows 10 开始，Windows 现在支持 USB 双重角色控制器。

## <a name="introduction"></a>简介


USB 双重角色功能使系统成为 USB *设备* 或 usb *主机*成为可能。 可在 [usb.org](https://www.usb.org/developers/wusb/docs/presentations/2006/Taipei06_SA_SBD_DRD_Design_Considerations.pdf) 网站上找到适用于 USB 双重角色的详细规范。

这里的重要一点是，双重角色功能允许移动设备（如手机、phablet 或 tablet）将自身指定为设备或主机。

当移动设备处于 *功能* 模式时，它会附加到作为连接移动设备的主机的 PC 或其他设备。

当移动设备处于 *主机* 模式时，用户可以将其设备（如鼠标或键盘）连接到该设备。 在这种情况下，移动设备承载附加设备。

通过在 Windows 10 中为 USB 双重角色提供支持，我们提供了以下优势：

-   通过 USB 连接到移动外围设备，与蓝牙等无线协议相比，它提供更大的数据带宽。
-   如果已连接到其他 USB 设备并与之通信，则可以选择 "电池通过 USB 充电" (，只要) 提供所需的硬件支持。
-   使最有可能拥有移动设备的客户（如智能手机）能够满足所有工作的需要。 此功能将允许在有线插接方案中提高工作效率，移动设备在该环境中进行停靠，因而承载外围设备。

下表显示了在 Windows 的 desktop 和 mobile Sku 上可用的 *主机* 类驱动程序的列表。

| USB 主机类驱动程序                                             | Windows 10 移动版 | Windows 10 桌面版 |
|--------------------------------------------------------------------|-------------------|---------------------------------|
| USB 集线器 (USBHUB)                                                   | 是               | 由于 Windows 2000) ，是 (        |
| HID-键盘/鼠标 (HidClass，KBDCLass，MouClass，KBDHid，MouHid)  | 是               | 由于 Windows 2000) ，是 (        |
| USB 大容量存储 (批量 & UASP)                                      | 是               | 由于 Windows 2000) ，是 (        |
|  (WinUSB 的通用 USB 主机驱动程序)                                    | 是               | 由于 Windows Vista) ，是 (       |
| USB Audio in/out (USBAUDIO)                                       | 是               |  (是的，因为 Windows XP)           |
| 串行设备 (USBSER)                                             | 是               | 由于 Windows 10) ，是 (          |
| 蓝牙 (BTHUSB)                                                  | 是               |  (是的，因为 Windows XP)           |
| 打印 (usbprint)                                                    | 否                |  (是的，因为 Windows XP)           |
| 正在扫描 (USBSCAN)                                                  | 否                | 由于 Windows 2000) ，是 (        |
| 网络摄像机 (USBVIDEO)                                                   | 否                | 由于 Windows Vista) ，是 (       |
|  (MTP 发起程序的媒体传输协议)                             | 否                | 由于 Windows Vista) ，是 (       |
| 远程 NDIS (RNDIS)                                                | 否                |  (是的，因为 Windows XP)           |
| 通过 USB (的 IP) IPoverUSB                                            | 否                | 是 (新的 Windows 10)         |



表中的类驱动程序是基于设备类遥测选择的，并且基于为 Windows 10 选择的关键方案。 我们计划包括有限数量的收件箱、第三方主机驱动程序，以支持 Windows 10 移动版上的密钥设备。 对于桌面版的 Windows 10，这些驱动程序将在 OEM 网站上或通过 Windows 更新 (WU) 提供。

对于 Windows 10 移动版，不包含收件箱的第三方驱动程序在 WU 上将不可用。 USB 主机堆栈 + HID 的磁盘占用量已经很小。 这就是为什么不是所有类驱动程序，而是 Windows 10 移动版的收件箱中包含的第三方驱动程序的原因。 希望使用第三方驱动程序的 OEM 可以使用 (BSP) 的板支持包，将它们添加到其移动设备的操作系统映像中。 有关此策略的详细信息，请参阅 [Windows Phone 的驱动程序开发](https://go.microsoft.com/fwlink/p/?LinkId=761246)，并向下滚动到 " *Windows Phone 和 Windows 的驱动程序开发之间的差异*" 一节。

下表显示了 Windows 移动 Sku 上可用的 *函数* 类驱动程序。

**注意** 对于桌面版，函数驱动程序在 Windows 10 上*不可用。*



| USB 函数类驱动程序                 | Windows 10 移动版 | Windows 10 桌面版 | 说明                                                                                                                                  |
|--------------------------------------------|-------------------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
|  (MTP 响应方的媒体传输协议)     | 是               | 否                              | 桌面上没有适用于 MTP 响应程序的方案。 桌面系统之间的 P2P 方案通过 WinUSB 上的 MigCable 启用。 |
| 视频显示 (vidstream)               | 是               | 否                              |                                                                                                                                        |
| 泛型 USB 函数驱动程序 (GenericUSBFn)  | 是               | 否                              | IPoverUSB 和其他桌面闪烁方案需要此方法。                                                                 |



我们将监视设备附件数据，如果需要提供额外的类驱动程序支持，请告知我们，因为设备类的受欢迎列表随时间推移而变化。

## <a name="driver-implementation"></a>驱动程序实现


Microsoft USB 角色切换 (URS) 驱动程序允许系统实施者充分利用其平台的双重角色 USB 功能。

URS 驱动程序旨在为使用单个 USB 控制器的平台提供双重角色功能，该控制器可以在一个端口上同时操作主机和外围角色。 *外围角色*也称为*函数角色*。 URS 驱动程序根据平台上的硬件事件，管理端口的当前角色以及适当软件堆栈的加载和卸载。

在具有 USB 微 AB 连接器的系统上，驱动程序使用硬件中断来指示连接器上 ID pin 的状态。 此 pin 用于检测控制器是否需要在连接中采用主机角色或函数角色。 有关详细信息，请参阅 [USB 点播规范](https://go.microsoft.com/fwlink/p/?LinkId=698414)。 在使用 USB 类型 C 连接器的系统上，OEM 实施者应该使用 [USB 类型 c 连接器驱动程序编程接口](/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)提供连接器客户端驱动程序。 客户端驱动程序与 Microsoft 提供的 USB 连接器管理器类扩展通信， (UcmCx) 来管理 USB 类型 C 连接器的所有方面，如 CC 检测、PD 消息传送等。 对于角色切换，客户端驱动程序会将 USB 类型 C 连接器的状态传达给 URS 驱动程序。

下图显示了使用 URS 驱动程序的双角色控制器的 USB 软件驱动程序堆栈。

![usb 角色切换驱动程序堆栈体系结构。 ](images/dual-role-arch.png)

请注意，URS 驱动程序绝不会同时加载上图中显示的函数和主机堆栈。 URS 驱动程序 *将加载函数* 堆栈 *或* 主机堆栈-具体取决于 USB 控制器的角色。

## <a name="hardware-requirements"></a>硬件要求


如果正在开发将利用 URS 驱动程序的平台，若要提供双重角色的 USB 功能，必须满足以下硬件要求：

-   USB 控制器

    这些驱动程序由 Microsoft 作为内置驱动程序提供。

    Synopsys DesignWare Core USB 3.0 控制器。 收件箱 INF： UrsSynopsys。

    Chipidea 高速 USB OTG 控制器。 收件箱 INF： UrsChipidea。

-   ID pin 中断

    可以通过以下两种方式之一来实现非 USB 类型 C 系统 (s) 的 ID pin 中断：

    两个边缘触发的中断：一个是在连接器上的 ID pin 被接地时触发的，另一个是在 ID pin 为浮动时激发的另一个。

    单个主动-两个中断，在 ID pin 被接地时处于活动状态。

-   USB 控制器枚举

    USB 双重角色控制器必须是 ACPI 枚举的。

-   软件支持

    URS 驱动程序需要一个允许通过连接器控制 VBus 的软件接口。 此接口是 SoC 特定的。 有关更多详细信息，请联系 SoC 供应商。

Windows 不支持以下 USB OTG 功能：

-    (ACA) 的附件充电器适配器检测。
-   会话请求协议 (SRP) 。
-   主机协商协议 (HNP) 。
-    (ADP) 附加检测协议。

## <a name="system-configuration"></a><a href="" id="acpi"></a>系统配置


若要使用 URS 驱动程序，必须为系统创建一个 ACPI 定义文件。 此外，还必须考虑一些与驱动程序相关的注意事项。

下面是 USB 双重角色控制器的示例 ACPI 定义。

```Text
//
// You may name the device whatever you want; we don't depend on it being called 'URS0'.
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
    // You may name the device whatever you want; we don't depend on it being called 'USB0'.
    //
    Device(USB0)
    {
        //
        // The host controller device node needs to have an address of '0'
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
    // You may name the device whatever you want; we don't depend on it being called 'UFN0'.
    //
    Device(UFN0)
    {
        //
        // The function controller device node needs to have an address of '1'
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

下面是 ACPI 文件主要部分的一些说明：

-   URS0 是 USB 双重角色控制器的 ACPI 定义。 这是 URS 驱动程序将加载到的 ACPI 设备。

-   USB0 和 UFN0 是 URS0 作用域内的子设备。 USB0 和 UFN0 表示将分别由 URS 驱动程序和主机和函数堆栈枚举的两个子堆栈。 请注意， \_ ADR 是 ACPI 将这些设备定义与 URS 驱动程序创建的设备对象进行匹配的方式。

-   如果控制器对这两个角色都使用相同的中断，则两个子设备中都可以描述相同的控制器中断。 即使在这种情况下，也仍然可以将中断描述为 "独占"。

-   你可以根据需要将其添加到此 ACPI 定义文件。 例如，你可以在 ACPI 定义文件中的任何设备上设置任何其他所需的方法或属性。 此类添加操作不会影响 URS 驱动程序的操作。 任何堆栈中所需的任何其他资源也可以在相应设备的 CRS 中进行描述 \_ 。

URS 驱动程序将硬件 Id 分配给主机和函数堆栈。 这些硬件 Id 派生自 URS 设备的硬件 ID。 例如，如果你的 URS 设备的硬件 ID 为 ACPI \\ ABCD1234，则 URS 驱动程序将为主机和函数堆栈创建硬件 id，如下所示：

-   主机堆栈： URS \\ ABCD1234&主机

-   函数堆栈： URS \\ ABCD1234&函数

## <a name="driver-installation-packages"></a><a href="" id="inf"></a>驱动程序安装包


必要时，第三方驱动程序包可以依赖于此方案。

如果你是 IHV 或 OEM，并且想要提供自己的驱动程序包，以下是一些需要考虑的事项：

- URS 驱动程序包

  应将每个平台上的双重角色控制器的硬件 ID 添加到 URS 的收件箱 INF。 但是，如果出于某种原因无法添加 ID，则 IHV/OEM 可能会提供一个具有 INF 的驱动程序包，该 INF 需要/包含收件箱 INF，并与硬件 ID 匹配。

  如果 IHV/OEM 需要驱动程序堆栈中存在筛选器驱动程序，则这是必需的。

- 主机驱动程序包。

  IHV/OEM 提供的驱动程序包需要/包括收件箱 *usbxhci .inf* ，并需要与主机设备硬件 ID 匹配。 硬件 ID 匹配将基于上一部分中所述的方案。

  如果 IHV/OEM 需要驱动程序堆栈中存在筛选器驱动程序，则这是必需的。

  正在进行的工作使 URS 驱动程序为主机设备分配 XHCI 兼容 ID。

- 函数驱动程序包

  IHV/OEM 提供的需要/包含收件箱 *Ufxsynopsys* 的驱动程序包，并且需要匹配外围设备硬件 ID。 硬件 ID 匹配将基于上一部分中所述的方案。

  IHV/OEM 还可以在驱动程序包中包含筛选器驱动程序。
  ## <a name="see-also"></a>另请参阅

[双重角色控制器驱动程序参考](/windows-hardware/drivers/ddi/_usbref/#dual-role-controller-driver-reference)