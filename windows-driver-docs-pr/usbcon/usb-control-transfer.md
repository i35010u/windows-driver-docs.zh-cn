---
description: 本主题介绍控制传输的结构以及客户端驱动程序应如何将控制请求发送到设备。
title: 如何发送 USB 控制传输
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: a2dbf51cd75543582550ef6dc712255aa1ad8412
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010111"
---
# <a name="how-to-send-a-usb-control-transfer"></a>如何发送 USB 控制传输


本主题介绍控制传输的结构以及客户端驱动程序应如何将控制请求发送到设备。

本主题内容：

-   [关于默认终结点](#about-the-default-endpoint)
-   [控制传输的布局](#layout-of-a-control-transfer)
-   [支持的驱动程序模型](#supported-driver-models)
    -   [相关技术](#related-technologies)
-   [必备条件](#prerequisites)
-   [Microsoft 定义的用于发送控制传输请求的方法](#microsoft-defined-methods-for-sending-control-transfer-requests)
-   [如何发送供应商命令的控制传输 - KMDF](#how-to-send-a-control-transfer-for-vendor-commands---kmdf)
-   [如何发送 GET\_STATUS 的控制传输 - UMDF](#how-to-send-a-control-transfer-for-get_status---umdf)

## <a name="about-the-default-endpoint"></a>关于默认终结点


所有 USB 设备必须支持至少一个名为“默认终结点”的终结点。  任何以默认终结点为目标的传输都称为“控制传输”。  控制传输的目的是使主机能够获取设备信息、配置设备或执行特定于设备的控制操作。

让我们从研究默认终结点的以下特征着手。

-   默认终结点的地址为 0。
-   默认终结点是双向的，也就是说，在一次传输过程中，主机可以向终结点发送数据并从其接收数据。
-   默认终结点在设备级别可用，不在设备的任何接口中定义。
-   一旦在主机和设备之间建立连接，默认终结点就处于活动状态。 甚至在选择配置之前，它就已经处于活动状态。
-   默认终结点的数据包最大大小取决于设备的总线速度。 低速，8 字节；全速和高速，64 字节；超高速，512 字节。

## <a name="layout-of-a-control-transfer"></a>控制传输的布局


由于控制传输是高优先级传输，因此会由主机在总线上保留一定量的带宽。 将为低速和全速设备保留 10% 的带宽；为高速和超高速传输设备保留 20% 的带宽。 现在，让我们看看控制传输的布局。

![USB 控制传输](images/control-transfer.png)

控制传输分为三个事务：设置事务  、数据事务  、状态事务  。 每个事务包含三类数据包：令牌数据包、数据数据包、握手数据包。   

某些字段通用于所有数据包。 这些字段是：

-   “同步”字段，指示数据包的开始。
-   数据包标识符 (PID)，指示数据包的类型、事务的方向、事务是成功还是失败（如果是握手数据包）。
-   EOP 字段，指示数据包的结束。

其他字段取决于数据包的类型。

-   **令牌数据包**

    每个设置事务都以令牌数据包开头。 下面是该数据包的结构。 主机始终发送令牌数据包。

    ![令牌数据包布局](images/token.png)

    PID 值指示令牌数据包的类型。 下面是可能的值：

    -   SETUP：指示控制传输中设置事务的开始。
    -   IN：指示主机在从设备请求数据（读取示例）。
    -   OUT：指示主机在将数据发送到设备（写入示例）。
    -   SOF：指示帧的开始。 此类型的令牌数据包包含一个 11 位的帧号。 主机发送 SOF 数据包。 发送此数据包的频率取决于总线速度。 对于全速总线，主机每隔 1 毫秒发送一次数据包；对于高速总线，则每隔 125 微秒发送一次。

<!-- -->

-   **数据数据包**

    紧跟着令牌数据包的是包含有效负载的数据数据包。 每个数据数据包能够包含的字节数取决于默认终结点的数据包最大大小。 数据数据包可以由主机或设备发送，具体取决于传输的方向。

    ![数据数据包布局](images/data.png)

<!-- -->

-   **握手数据包**

    紧跟着数据数据包的是握手数据包。 此数据包的 PID 指示是主机还是设备接收了数据包。 握手数据包可以由主机或设备发送，具体取决于传输的方向。

    ![握手数据包布局](images/handshake.png)

可以使用任何 USB 分析器（例如 Beagle、Ellisys、LeCroy USB 协议分析器）来查看事务和数据包的结构。 分析器设备显示如何通过线路将数据发送到 USB 设备或从其接收数据。 在此示例中，让我们检查由 LeCroy USB 分析器捕获的某些跟踪。 此示例仅供参考， 不表示 Microsoft 的认可。

-   **设置事务**

    始终由主机启动控制传输。 为此，主机会发送设置事务。 此事务包含名为“设置令牌”的令牌数据包，后跟一个 8 字节的数据数据包。  以下屏幕截图显示了一个示例性的设置事务。

    ![设置事务的跟踪。](images/setup-trans.png)

    在前面的跟踪中，主机启动（以 **H↓** 表示）控制传输的方式是发送设置令牌数据包 \#434。 请注意，PID 指定的 SETUP 表示一个设置令牌。 PID 后跟设备地址和终结点地址。 对于控制传输，该终结点地址始终为 0。

    接下来，主机发送数据数据包 \#435。 PID 为 DATA0，该值用于数据包排序（在后面讨论）。 PID 后跟 8 个字节，其中包含有关此请求的主要信息。 这 8 个字节指示请求的类型和缓冲区（设备将在其中写入响应）的大小。

    所有字节以相反顺序接收。 如 9.3 节所述，我们会看到以下字段和值：

    <table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>字段</th>
    <th>大小</th>
    <th>值</th>
    <th>说明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>bmRequestType</strong>（参见 9.3.1 bmRequestType）</td>
    <td>1</td>
    <td>0x80</td>
    <td><p>数据传输方向为从设备到主机（D7 为 1）</p>
    <p>请求为标准请求（D6…D5 为 0）</p>
    <p>请求的接收者为 DEVICE（D4 为 0）</p></td>
    </tr>
    <tr class="even">
    <td><strong>bRequest</strong>（参见 9.3.2 节和表 9-4）</td>
    <td>1</td>
    <td>0x06</td>
    <td>请求类型为 GET_DESCRIPTOR。</td>
    </tr>
    <tr class="odd">
    <td><strong>wValue</strong>（参见表 9-5）</td>
    <td>2</td>
    <td>0x0100</td>
    <td>请求值指示描述符类型为 DEVICE。</td>
    </tr>
    <tr class="even">
    <td><strong>wIndex</strong>（参见 9.3.4 节）</td>
    <td>2</td>
    <td>0x0000</td>
    <td><p>方向为从主机到设备（D7 为 1）</p>
    <p>终结点编号为 0。</p></td>
    </tr>
    <tr class="odd">
    <td><strong>wLength</strong>（参见 9.3.5 节）</td>
    <td>2</td>
    <td>0x0012</td>
    <td>请求将检索 18 个字节。</td>
    </tr>
    </tbody>
    </table>

    因此，我们可以得出结论：在此控制（读取）传输中，主机发送请求来检索设备描述符，并指定 18 个字节作为保存该描述符所需的传输长度。 设备发送这 18 个字节的方式取决于默认终结点可以在一个事务中发送多少数据。 该信息包含在设备描述符中，由设备在数据事务中返回。

    在响应中，设备发送一个握手数据包（即 \#436，以 **D↓** 表示）。 请注意，PID 值为 ACK（ACK 数据包）。 这表示设备确认了此事务。

-   **数据事务**

    现在，让我们看看设备在响应请求时返回的内容。 实际数据在数据事务中传输。

    下面是数据事务的跟踪。

    ![示例数据事务的跟踪。](images/datra-trans.png)

    在接收到 ACK 数据包后，主机会启动数据事务。 为了启动此事务，主机会发送方向为 IN（称为 IN 令牌）的令牌数据包 (\#450)。

    在响应中，设备发送一个紧随 IN 令牌的数据数据包 (\#451)。 此数据数据包包含实际的设备描述符。 第一个字节指示设备描述符的长度，即 18 个字节 (0x12)。 此数据数据包中的最后一个字节指示默认终结点支持的数据包最大大小。 在此示例中，我们看到设备可以通过其默认终结点一次发送 8 个字节。

    **注意**  默认终结点的数据包最大大小取决于设备的速度。 高速设备的默认终结点为 64 个字节；低速设备为 8 个字节。

    主机确认数据事务的方式是向设备发送 ACK 数据包 (\#452)。

    让我们计算返回的数据量。 在设置事务的数据数据包 (\#435) 的 **wLength** 字段中，主机请求了 18 个字节。 在数据事务中，我们看到从设备收到的只有设备描述符的前 8 个字节。 那么，主机如何接收存储在剩余的 10 个字节中的信息？ 设备分两个事务这样做：先是 8 个字节，然后是最后的 2 个字节。

    主机知道了默认终结点的数据包最大大小以后，就会启动新的数据事务，根据数据包大小请求下一部分。

    下面是下一数据事务：

    ![示例数据事务的跟踪。](images/datra-trans2.png)

    主机启动上面的数据事务的方式是：发送一个 IN 令牌 (\#463)，然后从设备请求随后的 8 个字节。 设备使用数据数据包 (\#464) 进行响应，该数据包中包含设备描述符接下来的 8 个字节。

    在收到这 8 个字节以后，主机向设备发送 ACK 数据包 (\#465)。

    接下来，主机在另一数据事务中请求最后的 2 个字节，如下所示：

    ![示例数据事务的跟踪。](images/datra-trans3.png)

    因此，我们看到，为了将 18 个字节从设备传输到主机，主机会跟踪传输的字节数并启动三个数据事务 (8+8+2)。

    **注意**   请注意数据事务 19、23、26 中数据数据包的 PID。 PID 在 DATA0 和 DATA1 之间交替变换。 该顺序称为数据切换。 在有多个数据事务的情况下，数据切换用于验证数据包顺序。 此方法可确保数据数据包不重复或丢失。

    将合并的数据数据包映射到设备描述符的结构（参见表 9-8）以后，我们看到以下字段和值：

    | 字段                  | 大小 | 值  | 说明                                                                       |
    |------------------------|------|--------|-----------------------------------------------------------------------------------|
    | **bLength**            | 1    | 0x12   | 设备描述符的长度，即 18 个字节。                               |
    | **bDescriptorType**    | 1    | 0x01   | 描述符类型为设备。                                                    |
    | **bcdUSB**             | 2    | 0x0100 | 规范版本号为 1.00。                                         |
    | **bDeviceClass**       | 1    | 0x00   | 设备类为 0。 配置中的每个接口都有类信息。 |
    | **bDeviceSubClass**    | 1    | 0x00   | 子类为 0，因为设备类为 0。                                          |
    | **bProtocol**          | 1    | 0x00   | 协议为 0。 此设备不使用任何特定于类的协议。             |
    | **bMaxPacketSize0**    | 1    | 0x08   | 终结点的数据包最大大小为 8 个字节。                               |
    | **idVendor**           | 2    | 0x0562 | 电传通信。                                                             |
    | **idProduct**          | 2    | 0x0002 | USB 麦克风。                                                                   |
    | **bcdDevice**          | 2    | 0x0100 | 指示设备发行版号。                                              |
    | **iManufacturer**      | 1    | 0x01   | 制造商字符串。                                                              |
    | **iProduct**           | 1    | 0x02   | 产品字符串。                                                                   |
    | **iSerialNumber**      | 1    | 0x03   | 序列号。                                                                    |
    | **bNumConfigurations** | 1    | 0x01   | 配置数。                                                         |



    检查这些值即可获得设备的一些初步信息。 设备是低速 USB 麦克风。 默认终结点的数据包最大大小为 8 个字节。 设备支持一种配置。

-   **状态事务**

    最后，主机会启动最后一个事务：状态事务，从而完成控制传输。

    ![示例数据事务的跟踪。](images/status-trans.png)

    主机使用 OUT 令牌数据包 (\#481) 来启动事务。 此数据包的目的是验证设备是否已发送所有请求的数据。 在此状态事务中，不发送数据数据包。 设备使用 ACK 数据包进行响应。 如果发生错误，PID 可能为 NAK 或 STALL。

## <a name="supported-driver-models"></a>支持的驱动程序模型


### <a name="related-technologies"></a>相关技术

-   [内核模式驱动程序框架](../wdf/index.md)
-   [用户模式驱动程序框架](../wdf/index.md)
-   [WinUSB](winusb.md)

## <a name="prerequisites"></a>必备条件


在客户端驱动程序能够枚举管道之前，请确保满足以下要求：

-   客户端驱动程序必须已创建框架 USB 目标设备对象。

    如果使用 Microsoft Visual Studio Professional 2012 随附的 USB 模板，则模板代码会执行这些任务。 模板代码会获取目标设备对象的句柄并将其存储在设备上下文中。

    **KMDF 客户端驱动程序：**

    KMDF 客户端驱动程序必须调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) 方法来获取 WDFUSBDEVICE 句柄。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md) 中的“设备源代码”。

    **UMDF 客户端驱动程序：**

    UMDF 客户端驱动程序必须通过查询框架目标设备对象获取 [**IWDFUsbTargetDevice**](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) 指针。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构 (UMDF)](understanding-the-umdf-template-code-for-usb.md) 中的“[**IPnpCallbackHardware**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware) 实现和特定于 USB 的任务”。

-   控制传输最重要的方面是正确设置设置令牌的格式。 在发送请求之前，请收集以下信息集：

    -   请求的方向：从主机到设备，或者从设备到主机。
    -   请求的接收者：设备、接口、终结点或其他。
    -   请求的类别：标准、类或供应商。
    -   请求的类型，例如 GET\_DESCRIPTPOR 请求。 有关详细信息，请参阅 USB 规范中的 9.5 节。
    -   **wValue** 和 **wIndex** 值。 这些值取决于请求的类型。

    可以从官方的 USB 规范中获取所有此类信息。

-   如果编写 UMDF 驱动程序，请从 OSR USB Fx2 学习工具包的 UMDF 示例驱动程序中获取头文件 Usb\_hw.h。 此头文件包含的宏和结构用于设置控制传输的设置数据包的格式。

    所有 UMDF 驱动程序必须与内核模式驱动程序通信才能通过设备发送和接收数据。 对于 USB UMDF 驱动程序，内核模式驱动程序始终是 Microsoft 提供的驱动程序 [WinUSB](winusb.md) (Winusb.sys)。

    每当 UMDF 启动程序针对 USB 驱动程序堆栈发出请求时，Windows I/O 管理器就会将该请求发送给 WinUSB。 收到请求后，WinUSB 会处理请求，或者将其转发给 USB 驱动程序堆栈。

## <a name="microsoft-defined-methods-for-sending-control-transfer-requests"></a>Microsoft 定义的用于发送控制传输请求的方法


主机上的 USB 客户端驱动程序启动的大多数控制请求是用于获取有关设备的信息、配置设备或发送供应商控制命令。 所有这些请求可以分为以下类别：

-   标准请求 — 标准请求在 USB 规范中定义。 发送此类请求的目的是获取有关设备及其配置、接口和终结点的信息。 每个请求的接收者取决于请求的类型。 接收者可以是设备、接口、终结点。

    **注意**  任何控制传输的目标都始终是默认终结点。 接收者是设备的实体，其信息（描述符、状态等）是主机感兴趣的。

    这些请求可以进一步分类为配置请求、功能请求和状态请求。

    -   发送配置请求是为了从设备获取信息，这样主机就能够配置设备，例如 GET\_DESCRIPTOR 请求就是配置请求。 这些请求也可能是主机发送的写入请求，目的是在设备中设置特定的配置或备用设置。
    -   功能请求由客户端驱动程序发送，目的是启用或禁用设备、接口或终结点支持的特定布尔设备设置。
    -   USB 设备支持状态请求，目的是使主机能够获取或设置 USB 定义的设备、终结点或接口的状态位。

    有关详细信息，请参阅 USB 规范版本 2.0 中的 9.4 节。 标准请求类型在头文件 Usbspec.h 中定义。

-   类请求 — 通过特定的设备类规范进行定义。
-   供应商请求 — 由供应商提供，取决于设备支持的请求。

Microsoft 提供的 USB 堆栈处理与设备进行的所有协议通信，如前面的跟踪所示。 此驱动程序会公开设备驱动程序接口 (DDI)，后者允许客户端驱动程序以多种方式发送控制传输。 如果客户端驱动程序是 Windows Driver Foundation (WDF) 驱动程序，则它可以直接调用例程来发送常见类型的控制请求。 WDF 本质上支持 KMDF 和 UMDF 的控制传输。

某些类型的控制请求不通过 WDF 公开。 对于这些请求，客户端驱动程序可以使用 WDF 混合模型。 此模型允许客户端驱动程序构建 WDM URB 样式的请求并设置其格式，然后使用 WDF 框架对象发送这些请求。 混合模型仅适用于内核模式驱动程序。

**对于 UMDF 驱动程序：**

请使用在 usb\_hw.h 中定义的帮助器宏和结构。 此头文件随附在 OSR USB Fx2 学习工具包的 UMDF 示例驱动程序中。

请使用下表来确定向 USB 驱动程序堆栈发送控制请求的最佳方式。 如果无法查看此表，请查看[此主题](/windows-hardware/drivers/ddi/index)中的表。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>如果要发送控制请求...</th>
<th>如果是 KMDF 驱动程序，请使用这些 KMDF DDI...</th>
<th>如果是 UMDF 驱动程序，请使用这些 UMDF 方法...</th>
<th>如果是 WDM 驱动程序，请构建 USB 结构（帮助器例程）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>CLEAR_FEATURE：禁用设备及其配置、接口和终结点中的特定功能设置。 请参阅 USB 规范中的 9.4.1 节。</td>
<td><ol>
<li>声明设置数据包。 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> 结构。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a> 初始化设置数据包。</li>
<li>指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a> 中定义的接收者值。</li>
<li>指定功能选择器 (<strong>wValue</strong>)。 请参阅 Usbspec.h 中的 USB_FEATURE_XXX 常量。 另请参阅 USB 规范中的表 9-6。</li>
<li>将 <em>SetFeature</em> 设置为 <strong>FALSE</strong>。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> 来发送请求。</li>
</ol></td>
<td><ol>
<li>声明设置数据包。 请参阅在 usb_hw.h 中声明的 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> 结构。</li>
<li>通过调用在 usb_hw.h 中定义的帮助器宏 <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong> 来初始化设置数据包。</li>
<li>指定在 <strong>WINUSB_BMREQUEST_RECIPIENT</strong> 中定义的接收者值。</li>
<li>指定功能选择器 (<strong>wValue</strong>)。 请参阅 Usbspec.h 中的 <strong>USB_FEATURE_XXX</strong> 常量。 另请参阅 USB 规范中的表 9-6。</li>
<li>将 <em>SetFeature</em> 设置为 <strong>FALSE</strong>。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> 方法将初始化的设置数据包与框架请求对象和传输缓冲区相关联，以这种方式构建请求。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> 方法来发送请求。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>GET_CONFIGURATION：获取当前的 USB 配置。 请参阅 USB 规范中的 9.4.2 节。</td>
<td><p>KMDF 默认选择第一个配置。 若要检索设备定义的配置编号，请执行以下操作：</p>
<ol>
<li>格式化 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>，将其 <strong>bRequest</strong> 成员设置为 <strong>USB_REQUEST_GET_CONFIGURATION</strong>。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> 来发送请求。</li>
</ol></td>
<td><p>UMDF 默认选择第一个配置。 若要检索设备定义的配置编号，请执行以下操作：</p>
<ol>
<li>声明设置数据包。 请参阅在 usb_hw.h 中声明的 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> 结构。</li>
<li>通过调用在 usb_hw.h 中定义的帮助器宏 <strong>WINUSB_CONTROL_SETUP_PACKET_INIT</strong> 来初始化设置数据包。</li>
<li>将 <strong>BmRequestToDevice</strong> 指定为方向、<strong>BmRequestToDevice</strong> 指定为接收者、<strong>USB_REQUEST_GET_CONFIGURATION</strong> 指定为请求。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> 方法将初始化的设置数据包与框架请求对象和传输缓冲区相关联，以这种方式构建请求。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> 方法来发送请求。</li>
<li>在传输缓冲区中接收配置编号。 通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a> 方法访问该缓冲区。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_CONFIGURATION</p></td>
</tr>
<tr class="odd">
<td>GET_DESCRIPTOR：获取设备、配置、接口和终结点描述符。 请参阅 USB 规范中的 9.4.3 节。
<p>有关详细信息，请参阅 <a href="usb-descriptors.md" data-raw-source="[USB Descriptors](usb-descriptors.md)">USB 描述符</a>。</p></td>
<td><p>调用以下方法：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetEndpointInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation)"><strong>WdfUsbInterfaceGetEndpointInformation</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)"><strong>WdfUsbTargetPipeGetInformation</strong></a>。 此方法返回 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information" data-raw-source="[&lt;strong&gt;WDF_USB_PIPE_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)"><strong>WDF_USB_PIPE_INFORMATION</strong></a> 结构中的终结点描述符字段。</li>
</ul></td>
<td><p>调用以下方法：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)"><strong>IWDFUsbInterface::GetInterfaceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe::GetInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)"><strong>IWDFUsbTargetPipe::GetInformation</strong></a>。 此方法返回 <a href="https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information" data-raw-source="[&lt;strong&gt;WINUSB_PIPE_INFORMATION&lt;/strong&gt;](/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)"><strong>WINUSB_PIPE_INFORMATION</strong></a> 结构中的终结点描述符字段。</li>
</ul></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](/previous-versions/ff538943(v=vs.85))"><strong>UsbBuildGetDescriptorRequest</strong></a>)</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_INTERFACE</p></td>
</tr>
<tr class="even">
<td>GET_INTERFACE：获取接口的当前备用设置。 请参阅 USB 规范中的 9.4.4 节。</td>
<td><p></p>
<ol>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetInterface&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)"><strong>WdfUsbTargetDeviceGetInterface</strong></a> 方法获取目标接口对象的 WDFUSBINTERFACE 句柄。</li>
<li>调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetConfiguredSettingIndex&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex)"><strong>WdfUsbInterfaceGetConfiguredSettingIndex</strong></a> 方法。</li>
</ol></td>
<td><ol>
<li>获取目标接口对象的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)"><strong>IWDFUsbInterface</strong></a> 指针。</li>
<li>调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetConfiguredSettingIndex&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)"><strong>IWDFUsbInterface::GetConfiguredSettingIndex</strong></a> 方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_interface_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_INTERFACE_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_interface_request)"><strong>_URB_CONTROL_GET_INTERFACE_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>GET_STATUS：获取设备、终结点或接口的状态位。 请参阅 USB 规范中 的 9.4.5 节。</td>
<td><ol>
<li>声明设置数据包。 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> 结构。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong></a> 初始化设置数据包。</li>
<li>指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a> 中定义的接收者值。</li>
<li>指定要获取设备、接口或终结点的哪个状态 (<strong>wIndex</strong>)。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> 来发送请求。</li>
</ol></td>
<td><ol>
<li>声明设置数据包。 请参阅在 usb_hw.h 中声明的 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> 结构。</li>
<li>通过调用在 usb_hw.h 中定义的帮助器宏 <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong> 来初始化设置数据包。</li>
<li>指定在 <strong>WINUSB_BMREQUEST_RECIPIENT</strong> 中定义的接收者值。</li>
<li>指定要获取设备、接口或终结点的哪个状态 (<strong>wIndex</strong>)。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> 方法将初始化的设置数据包与框架请求对象和传输缓冲区相关联，以这种方式构建请求。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> 方法来发送请求。</li>
<li>在传输缓冲区中接收状态值。 通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a> 方法访问该缓冲区。</li>
<li>若要确定状态指示自驱动还是远程唤醒，请使用 <strong>WINUSB_DEVICE_TRAITS</strong> 枚举中定义的值：</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_status_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_STATUS_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_status_request)"><strong>_URB_CONTROL_GET_STATUS_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildgetstatusrequest" data-raw-source="[&lt;strong&gt;UsbBuildGetStatusRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildgetstatusrequest)"><strong>UsbBuildGetStatusRequest</strong></a>)</p>
<p>URB_FUNCTION_GET_STATUS_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_INTERFACE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_STATUS_FROM_OTHER。</p></td>
</tr>
<tr class="even">
<td>SET_ADDRESS：请参阅 USB 规范中的 9.4.6 节。</td>
<td>此请求由 USB 驱动程序堆栈处理；客户端驱动程序不能执行此操作。</td>
<td>此请求由 USB 驱动程序堆栈处理；客户端驱动程序不能执行此操作。</td>
<td>此请求由 USB 驱动程序堆栈处理；客户端驱动程序不能执行此操作。</td>
</tr>
<tr class="odd">
<td>SET_CONFIGURATION：设置一个配置。 请参阅 USB 规范中的 9.4.7 节。
<p>有关详细信息，请参阅<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何选择 USB 设备的配置</a>。</p></td>
<td>默认情况下，KMDF 选择默认配置以及每个接口中的第一个备用设置。 客户端驱动程序可以调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfigType&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype)"><strong>WdfUsbTargetDeviceSelectConfigType</strong></a> 方法并将 <strong>WdfUsbTargetDeviceSelectConfigTypeUrb</strong> 指定为请求选项，以这种方式更改默认配置。 然后，你必须格式化此请求的 URB 并将其提交到 USB 驱动程序堆栈。</td>
<td>默认情况下，UMDF 选择默认配置以及每个接口中的第一个备用设置。 客户端驱动程序无法更改此配置。</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_configuration" data-raw-source="[&lt;strong&gt;_URB_SELECT_CONFIGURATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_configuration)"><strong>_URB_SELECT_CONFIGURATION</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_CONFIGURATION</p></td>
</tr>
<tr class="even">
<td>SET_DESCRIPTOR：更新现有设备、配置或字符串描述符。 请参阅 USB 规范中的 9.4.8 节。
<p>此请求不常用。 但是，USB 驱动程序堆栈会接受来自客户端驱动程序的此类请求。</p></td>
<td><ol>
<li>分配并构建请求的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>。</li>
<li>指定 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a> 结构中的传输信息。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForUrb&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)"><strong>WdfUsbTargetDeviceFormatRequestForUrb</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendUrbSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)"><strong>WdfUsbTargetDeviceSendUrbSynchronously</strong></a> 来发送请求。</li>
</ol></td>
<td><ol>
<li>声明设置数据包。 请参阅在 usb_hw.h 中声明的 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> 结构。</li>
<li>按 USG 规范指定传输信息。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> 方法将初始化的设置数据包与框架请求对象和传输缓冲区相关联，以这种方式构建请求。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> 方法来发送请求。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_DEVICE</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SET_FEATURE：启用设备及其配置、接口和终结点中的特定功能设置。 请参阅 USB 规范中的 9.4.9 节。</td>
<td><ol>
<li>声明设置数据包。 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> 结构。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a> 初始化设置数据包。</li>
<li>指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a> 中定义的接收者值（设备、接口、终结点）。</li>
<li>指定功能选择器 (<strong>wValue</strong>)。 请参阅 Usbspec.h 中的 USB_FEATURE_XXX 常量。 另请参阅 USB 规范中的表 9-6。</li>
<li>将 <em>SetFeature</em> 设置为 <strong>TRUE</strong></li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> 来发送请求。</li>
</ol></td>
<td><ol>
<li>声明设置数据包。 请参阅在 usb_hw.h 中声明的 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> 结构。</li>
<li>通过调用在 usb_hw.h 中定义的帮助器宏 <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong> 来初始化设置数据包。</li>
<li>指定在 <strong>WINUSB_BMREQUEST_RECIPIENT</strong> 中定义的接收者值。</li>
<li>指定功能选择器 (<strong>wValue</strong>)。 请参阅 Usbspec.h 中的 <strong>USB_FEATURE_XXX</strong> 常量。 另请参阅 USB 规范中的表 9-6。</li>
<li>将 <em>SetFeature</em> 设置为 <strong>TRUE</strong>。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> 方法将初始化的设置数据包与框架请求对象和传输缓冲区相关联，以这种方式构建请求。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> 方法来发送请求。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_SET_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>SET_INTERFACE：更改接口中的备用设置。 请参阅 USB 规范中的 9.4.9 节。
<p>有关详细信息，请参阅<a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">如何在 USB 接口中选择备用设置</a>。</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a>
<p></p>
<ol>
<li>获取目标接口对象的 WDFUSBINTERFACE 句柄。</li>
<li>调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)"><strong>WdfUsbInterfaceSelectSetting</strong></a> 方法。</li>
</ol></td>
<td><ol>
<li>获取目标接口对象的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)"><strong>IWDFUsbInterface</strong></a> 指针。</li>
<li>调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)"><strong>IWDFUsbInterface::SelectSetting</strong></a> 方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_interface" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_interface)"><strong>_URB_SELECT_INTERFACE</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)"><strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SYNC_FRAME：设置并获取终结点的同步帧号。 请参阅 USB 规范中的 9.4.10 节。</td>
<td>此请求由 USB 驱动程序堆栈处理；客户端驱动程序不能执行此操作。</td>
<td>此请求由 USB 驱动程序堆栈处理；客户端驱动程序不能执行此操作。</td>
<td>此请求由 USB 驱动程序堆栈处理；客户端驱动程序不能执行此操作。</td>
</tr>
<tr class="even">
<td>针对特定于设备类的请求和供应商命令。</td>
<td><ol>
<li>声明设置数据包。 请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> 结构。</li>
<li>通过调用特定于 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS</strong></a> 的请求或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong></a>（针对供应商命令），初始化设置数据包。</li>
<li>指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a> 中定义的接收者值（设备、接口、终结点）。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> 来发送请求。</li>
</ol></td>
<td><ol>
<li>声明设置数据包。 请参阅在 usb_hw.h 中声明的 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> 结构。</li>
<li>通过调用在 usb_hw.h 中定义的帮助器宏 <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_CLASS</strong> 或 <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong>，初始化设置数据包。</li>
<li>指定方向（请参阅 <strong>WINUSB_BMREQUEST_DIRECTION</strong> 枚举）、接收者（请参阅 <strong>WINUSB_BMREQUEST_RECIPIENT</strong> 枚举）和请求，详见类或硬件规范。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> 方法将初始化的设置数据包与框架请求对象和传输缓冲区相关联，以这种方式构建请求。</li>
<li>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> 方法来发送请求。</li>
<li>在传输缓冲区中接收来自设备的信息。 通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a> 方法访问该缓冲区。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_vendor_or_class_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_VENDOR_OR_CLASS_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_vendor_or_class_request)"><strong>_URB_CONTROL_VENDOR_OR_CLASS_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538986(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildVendorRequest&lt;/strong&gt;](/previous-versions/ff538986(v=vs.85))"><strong>UsbBuildVendorRequest</strong></a>)</p>
<p>URB_FUNCTION_VENDOR_DEVICE</p>
<p>URB_FUNCTION_VENDOR_INTERFACE</p>
<p>URB_FUNCTION_VENDOR_ENDPOINT</p>
<p>URB_FUNCTION_VENDOR_OTHER</p>
<p>URB_FUNCTION_CLASS_DEVICE</p>
<p>URB_FUNCTION_CLASS_INTERFACE</p>
<p>URB_FUNCTION_CLASS_ENDPOINT</p>
<p>URB_FUNCTION_CLASS_OTHER</p></td>
</tr>
</tbody>
</table>



## <a name="how-to-send-a-control-transfer-for-vendor-commands---kmdf"></a>如何发送供应商命令的控制传输 - KMDF


以下过程演示了客户端驱动程序如何发送控制传输。 在此示例中，客户端驱动程序发送一个从设备检索固件版本的供应商命令。

1.  声明一个用于供应商命令的常量。 研究硬件规范，确定要使用的供应商命令。
2.  通过调用 [**WDF\_MEMORY\_DESCRIPTOR\_INIT\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff552392_init_buffer) 宏来声明 [**WDF\_MEMORY\_DESCRIPTOR**](/windows-hardware/drivers/ddi/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor) 结构并将其初始化。 此结构会在 USB 驱动程序完成请求后从设备接收响应。
3.  指定发送选项，具体取决于你是以同步方式还是异步方式发送请求：
    -   如果通过调用 [**WdfUsbTargetDeviceSendControlTransferSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously) 以同步方式发送请求，请指定超时值。 该值很重要，因为如果没有超时值，则可能无限期阻止线程。

        为此，请通过调用 [**WDF\_REQUEST\_SEND\_OPTIONS\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552491_init) 宏声明 [**WDF\_REQUEST\_SEND\_OPTIONS**](/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options) 结构并将其初始化。 将此选项指定为 **WDF\_REQUEST\_SEND\_OPTION\_TIMEOUT**。

        接下来，通过调用 [**WDF\_REQUEST\_SEND\_OPTIONS\_SET\_TIMEOUT**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdf_request_send_options_set_timeout) 宏设置超时值。

    -   如果以异步方式发送请求，请实施一个完成例程。 释放完成例程中所有分配的资源。

4.  声明一个 [**WDF\_USB\_CONTROL\_SETUP\_PACKET**](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet) 结构，使之包含设置令牌，然后将结构格式化。 为此，请调用 [**WDF\_USB\_CONTROL\_SETUP\_PACKET\_INIT\_VENDOR**](https://msdn.microsoft.com/library/windows/hardware/ff552568_init_vendor) 宏来格式化设置数据包。 在调用中指定请求的方向、接收者、发送-请求选项（已在步骤 3 中初始化）以及供应商命令的常量。
5.  通过调用 [**WdfUsbTargetDeviceSendControlTransferSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously) 或 [**WdfUsbTargetDeviceFormatRequestForControlTransfer**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer) 来发送请求。
6.  检查框架返回的 NTSTATUS 值，并检查接收的值。

以下代码示例将控制传输请求发送到 USB 设备，以便检索其固件版本。 请求以异步方式发送，客户端驱动程序指定一个 5 秒的相对超时值（以 100 纳秒为单位）。 驱动程序将接收的响应存储在驱动程序定义的设备上下文中。

```cpp
enum {   
    USBFX2_GET_FIRMWARE_VERSION = 0x1,  
....

} USBFX2_VENDOR_COMMANDS; 

#define WDF_TIMEOUT_TO_SEC              ((LONGLONG) 1 * 10 * 1000 * 1000)  // defined in wdfcore.h

const __declspec(selectany) LONGLONG   
            DEFAULT_CONTROL_TRANSFER_TIMEOUT = 5 * -1 * WDF_TIMEOUT_TO_SEC; 


typedef struct _DEVICE_CONTEXT
{

    ...
       union {  
        USHORT      VersionAsUshort;  
        struct {  
            BYTE Minor;  
            BYTE Major;  
        } Version;  
    } Firmware; // Firmware version.

} DEVICE_CONTEXT, *PDEVICE_CONTEXT;


__drv_requiresIRQL(PASSIVE_LEVEL)  
VOID  GetFirmwareVersion(  
    __in PDEVICE_CONTEXT DeviceContext  
)  
{  
    NTSTATUS                        status;  
    WDF_USB_CONTROL_SETUP_PACKET    controlSetupPacket;  
    WDF_REQUEST_SEND_OPTIONS        sendOptions;  
    USHORT                          firmwareVersion;  
    WDF_MEMORY_DESCRIPTOR           memoryDescriptor;  

    PAGED_CODE();  

    firmwareVersion = 0;  

    WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&memoryDescriptor, (PVOID) &firmwareVersion, sizeof(firmwareVersion));  

    WDF_REQUEST_SEND_OPTIONS_INIT(  
                                  &sendOptions,  
                                  WDF_REQUEST_SEND_OPTION_TIMEOUT  
                                  );  

    WDF_REQUEST_SEND_OPTIONS_SET_TIMEOUT(  
                                         &sendOptions,  
                                         DEFAULT_CONTROL_TRANSFER_TIMEOUT  
                                         );  

    WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR(&controlSetupPacket,  
                                        BmRequestDeviceToHost,       // Direction of the request
                                        BmRequestToDevice,           // Recipient
                                        USBFX2_GET_FIRMWARE_VERSION, // Vendor command
                                        0,                           // Value
                                        0);                          // Index    

    status = WdfUsbTargetDeviceSendControlTransferSynchronously(  
                                        DeviceContext->UsbDevice,  
                                        WDF_NO_HANDLE,               // Optional WDFREQUEST
                                        &sendOptions,  
                                        &controlSetupPacket,  
                                        &memoryDescriptor,           // MemoryDescriptor                                          
                                        NULL);                       // BytesTransferred    

    if (!NT_SUCCESS(status)) 
    {  
        KdPrint(("Device %d: Failed to get device firmware version 0x%x\n", DeviceContext->DeviceNumber, status));  
        TraceEvents(DeviceContext->DebugLog,  
                    TRACE_LEVEL_ERROR,  
                    DBG_RUN,  
                    "Device %d: Failed to get device firmware version 0x%x\n",  
                    DeviceContext->DeviceNumber,  
                    status);  
    }
    else 
    {  
        DeviceContext->Firmware.VersionAsUshort = firmwareVersion;  
        TraceEvents(DeviceContext->DebugLog,  
                    TRACE_LEVEL_INFORMATION,  
                    DBG_RUN,  
                    "Device %d: Get device firmware version : 0x%x\n",  
                    DeviceContext->DeviceNumber,  
                    firmwareVersion);  
    }  

    return;  
}  
```

##<a name="how-to-send-a-control-transfer-for-get_status---umdf"></a><a name="how-to-send-a-control-transfer-for-get_status---umdf"></a>如何发送 GET\_STATUS 的控制传输 - UMDF


以下过程演示了客户端驱动程序如何发送 GET\_STATUS 命令的控制传输。 请求的接收者为设备，请求获取 D1-D0 位中的信息。 有关详细信息，请参阅 USB 规范中的图 9-4。

1.  包括随附在 OSR USB Fx2 学习工具包的 UMDF 示例驱动程序中的头文件 Usb\_hw.h。
2.  说明 **WINUSB\_CONTROL\_SETUP\_PACKET** 结构。
3.  通过调用帮助器宏 **WINUSB\_CONTROL\_SETUP\_PACKET\_INIT\_GET\_STATUS** 来初始化设置数据包。
4.  指定 **BmRequestToDevice** 作为接收者。
5.  在 *Index* 值中指定 0。
6.  调用帮助器方法 SendControlTransferSynchronously，以同步方式发送请求。

    此帮助器方法通过调用 [**IWDFUsbTargetDevice::FormatRequestForControlTransfer**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer) 方法将初始化的设置数据包与框架请求对象和传输缓冲区相关联，以这种方式构建请求。 然后，此帮助器方法通过调用 [**IWDFIoRequest::Send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) 方法来发送请求。 在此方法返回后，检查返回的值。

7.  若要确定状态指示自驱动还是远程唤醒，请使用 **WINUSB\_DEVICE\_TRAITS** 枚举中定义的值：

以下代码示例通过发送控制传输请求来获取设备的状态。 此示例通过调用名为 SendControlTransferSynchronously 的帮助器方法以异步方式发送请求。

```cpp
HRESULT  
CDevice::GetDeviceStatus ()  
{  

    HRESULT hr = S_OK;

    USHORT deviceStatus;  
    ULONG bytesTransferred;  


    TraceEvents(TRACE_LEVEL_INFORMATION,  
                DRIVER_ALL_INFO,  
                "%!FUNC!: entry");  


    // Setup the control packet.      

    WINUSB_CONTROL_SETUP_PACKET setupPacket;  

    WINUSB_CONTROL_SETUP_PACKET_INIT_GET_STATUS(  
                                      &setupPacket,  
                                      BmRequestToDevice,  
                                      0);  

    hr = SendControlTransferSynchronously(  
                 &(setupPacket.WinUsb),  
                 & deviceStatus,  
                 sizeof(USHORT),  
                 &bytesReturned  
                ); 

     if (SUCCEEDED(hr))  
    {  
        if (deviceStatus & USB_GETSTATUS_SELF_POWERED)
        {
             m_Self_Powered = true;
        } 
        if (deviceStatus & USB_GETSTATUS_REMOTE_WAKEUP_ENABLED)
        {
             m_remote_wake-enabled = true;
        }  

    }  


    return hr;  

 }
```

以下代码示例演示了如何实现名为 SendControlTransferSynchronously 的帮助器方法。 此方法以异步方式发送请求。

```cpp
HRESULT  
CDevice::SendControlTransferSynchronously(  
    _In_ PWINUSB_SETUP_PACKET SetupPacket,  
    _Inout_ PBYTE Buffer,  
    _In_ ULONG BufferLength,  
    _Out_ PULONG LengthTransferred  
    )  
{  
    HRESULT hr = S_OK;  
    IWDFIoRequest *pWdfRequest = NULL;  
    IWDFDriver * FxDriver = NULL;  
    IWDFMemory * FxMemory = NULL;   
    IWDFRequestCompletionParams * FxComplParams = NULL;  
    IWDFUsbRequestCompletionParams * FxUsbComplParams = NULL;  

    *LengthTransferred = 0;  

    hr = m_FxDevice->CreateRequest( NULL, //pCallbackInterface
                                    NULL, //pParentObject
                                    &pWdfRequest);  

    if (SUCCEEDED(hr))  
    {  
        m_FxDevice->GetDriver(&FxDriver);  

        hr = FxDriver->CreatePreallocatedWdfMemory( Buffer,  
                                                    BufferLength,  
                                                    NULL,        //pCallbackInterface
                                                    pWdfRequest, //pParetObject
                                                    &FxMemory );  
    }  

    if (SUCCEEDED(hr))  
    {  
        hr = m_pIUsbTargetDevice->FormatRequestForControlTransfer( pWdfRequest,  
                                                                   SetupPacket,  
                                                                   FxMemory,  
                                                                   NULL); //TransferOffset
    }                                                            

    if (SUCCEEDED(hr))  
    {  
        hr = pWdfRequest->Send( m_pIUsbTargetDevice,  
                                WDF_REQUEST_SEND_OPTION_SYNCHRONOUS,  
                                0); //Timeout      }  

    if (SUCCEEDED(hr))  
    {  
        pWdfRequest->GetCompletionParams(&FxComplParams);  

        hr = FxComplParams->GetCompletionStatus();  
    }  

    if (SUCCEEDED(hr))  
    {  
        HRESULT hrQI = FxComplParams->QueryInterface(IID_PPV_ARGS(&FxUsbComplParams));  
        WUDF_TEST_DRIVER_ASSERT(SUCCEEDED(hrQI));  

        WUDF_TEST_DRIVER_ASSERT( WdfUsbRequestTypeDeviceControlTransfer ==   
                            FxUsbComplParams->GetCompletedUsbRequestType() );  

        FxUsbComplParams->GetDeviceControlTransferParameters( NULL,  
                                                             LengthTransferred,  
                                                             NULL,  
                                                             NULL );  
    }  

    SAFE_RELEASE(FxUsbComplParams);  
    SAFE_RELEASE(FxComplParams);  
    SAFE_RELEASE(FxMemory);  

    pWdfRequest->DeleteWdfObject();          
    SAFE_RELEASE(pWdfRequest);  

    SAFE_RELEASE(FxDriver);  

    return hr;  
}  
```

## <a name="remarks"></a>备注


如果使用 Winusb.sys 作为设备的功能驱动程序，则可从应用程序发送控制传输。 若要格式化 WinUSB 中的设置数据包，请使用 UMDF 帮助器宏和结构，详见本主题中的表。 若要发送请求，请调用 [**WinUsb\_ControlTransfer**](/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer) 函数。