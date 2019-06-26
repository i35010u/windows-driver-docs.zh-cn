---
Description: 本主题介绍控制传输和如何客户端驱动程序应将控制请求发送到设备的结构。
title: 如何发送 USB 控制传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a663ffbaa5d49f74798bcc4247e7acf264d1bc7
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391435"
---
# <a name="how-to-send-a-usb-control-transfer"></a>如何发送 USB 控制传输


本主题介绍控制传输和如何客户端驱动程序应将控制请求发送到设备的结构。

本主题内容：

-   [有关默认终结点](#about-the-default-endpoint)
-   [控制传输的布局](#layout-of-a-control-transfer)
-   [支持的驱动程序模型](#supported-driver-models)
    -   [相关的技术](#related-technologies)
-   [必备条件](#prerequisites)
-   [Microsoft 定义的方法，用于发送控制传输请求](#microsoft-defined-methods-for-sending-control-transfer-requests)
-   [如何发送供应商命令-KMDF 控制传输](#how-to-send-a-control-transfer-for-vendor-commands---kmdf)
-   [如何将发送 GET 控制传输\_状态-UMDF](#how-to-send-a-control-transfer-for-get_status---umdf)

## <a name="about-the-default-endpoint"></a>有关默认终结点


所有 USB 设备必须都支持至少一个终结点调用*默认终结点*。 名为目标的默认终结点的传输所有*控制传输*。 控制传输的目的是使宿主能够获取设备信息，请配置设备，或执行是唯一的设备的控制操作。

让我们首先研究这些特征的默认终结点。

-   默认终结点的地址为 0。
-   默认终结点是双向的也就是说，主机可以将数据发送到终结点和一次传输中从其接收数据。
-   默认终结点可在设备级别，并且未在设备的任何接口中定义。
-   只要主机和设备之间建立连接的默认终结点处于活动状态。 即使之前选中了配置，它处于活动状态。
-   默认终结点的最大数据包大小取决于设备的总线速度。 低速度，8 个字节;完整和高速度、 64 个字节;SuperSpeed，512 个字节。

## <a name="layout-of-a-control-transfer"></a>控制传输的布局


控制传输量都是高优先级传输，因为一定量的带宽保留总线上的主机。 对于低和完整速度的设备，10%的带宽;高的 20%和 SuperSpeed 传输设备。 现在，让我们看一下控制传输的布局。

![usb 控制传输](images/control-transfer.png)

控制传输分为三个事务：*设置事务*，*数据事务*，并*状态事务*。 每个事务包含的数据包的三种类型：*令牌数据包*，*数据包*，并*握手数据包*。

某些字段是通用的所有数据包。 这些字段是：

-   同步字段，它指示数据包的开始。
-   数据包标识符 (PID) 指示类型的数据包，方向的事务，并在握手数据包时，它指示成功或失败的事务。
-   EOP 字段指示数据包的末尾。

其他字段取决于数据包的类型。

-   **令牌的数据包**

    安装程序的每个事务开始标记数据包。 下面是数据包的结构。 主机始终发送令牌的数据包。

    ![令牌数据包布局](images/token.png)

    PID 值指示令牌的数据包的类型。 下面是可能的值：

    -   安装程序：指示控制传输中的安装程序的事务的开始。
    -   中：指示主机从 （读取用例） 的设备请求数据。
    -   扩展：指示主机将数据发送到设备 （写入大小写）。
    -   SOF:指示帧的开始。 这种类型的令牌的数据包包含 11 位帧数。 主机发送 SOF 数据包。 从该处发送此数据包的频率取决于总线速度。 为完整的速度，主机会将数据包发送每个 1millisecond;高速总线上每个 125 低至微秒。

<!-- -->

-   **数据包**

    紧跟令牌数据包是数据包中包含的有效负载。 可以包含的每个数据包的字节数取决于默认终结点的最大数据包大小。 可以通过主机或设备，具体取决于传输的方向发送数据包。

    ![数据数据包布局](images/data.png)

<!-- -->

-   **握手数据包**

    紧跟数据数据包是握手数据包。 数据包的 PID 指示通过在主机或设备接收数据包。 可以通过在主机或设备，具体取决于传输的方向发送握手数据包。

    ![握手数据包布局](images/handshake.png)

可以使用任何 USB 分析器，例如小猎狗 Ellisys，LeCroy USB 协议分析器来查看事务和数据包的结构。 分析器设备显示了如何发送到或无法通过网络从 USB 设备接收数据。 在此示例中，让我们看一些由 LeCroy USB 分析器捕获的跟踪。 此示例是仅用于提供信息。 这并不代表 Microsoft 的认可。

-   **安装程序事务**

    主机始终启动控制传输。 它会通过将发送安装事务。 此事务包含名为令牌数据包*安装程序令牌*跟 8 字节数据包。 此屏幕截图显示了示例安装程序事务。

    ![安装程序事务跟踪。](images/setup-trans.png)

    在前面的跟踪中，主机将启动 (由**H↓**) 通过发送设置令牌数据包的控制转移\#434。 请注意 PID 指定安装程序，该值指示安装程序令牌。 PID 跟设备地址和终结点地址。 对于控制传输，该终结点地址始终是 0。

    接下来，在主机发送数据数据包\#435。 PID 为 DATA0 和使用值用于数据包排序 （若要讨论）。 PID 跟 8 个字节，其中包含有关此请求的主要信息。 这些 8 个字节表示的请求的类型和该设备将在其中编写其响应的缓冲区的大小。

    按相反的顺序接收的所有字节。 一部分 9.3 中所述，我们看到这些字段和值：

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
    <th>ReplTest1</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>bmRequestType</strong> (请参阅 9.3.1 bmRequestType)</td>
    <td>1</td>
    <td>0x80</td>
    <td><p>数据传输方向是从设备到主机 （D7 为 1）</p>
    <p>该请求是标准的请求 (D6...D5 为 0）</p>
    <p>请求的接收方是设备 （D4 为 0）</p></td>
    </tr>
    <tr class="even">
    <td><strong>bRequest</strong> （请参阅部分，请参阅 9.3.2 和表 9-4）</td>
    <td>1</td>
    <td>0x06</td>
    <td>请求类型为 GET_DESCRIPTOR。</td>
    </tr>
    <tr class="odd">
    <td><strong>wValue</strong> (请参阅表 9-5)</td>
    <td>2</td>
    <td>0x0100</td>
    <td>请求值指示描述符类型是设备。</td>
    </tr>
    <tr class="even">
    <td><strong>wIndex</strong>（请参阅部分 9.3.4）</td>
    <td>2</td>
    <td>0x0000</td>
    <td><p>方向是从主机到设备 （D7 为 1）</p>
    <p>终结点号为 0。</p></td>
    </tr>
    <tr class="odd">
    <td><strong>并将 wLength</strong> （请参阅部分 9.3.5）</td>
    <td>2</td>
    <td>0x0012</td>
    <td>请求是要检索 18 个字节。</td>
    </tr>
    </tbody>
    </table>

    因此，我们可以得出结论： 此控件 （读取） 传输，主机发送请求以检索设备说明符和指定为要保存该描述符的传输长度的 18 个字节。 设备发送这些 18 字节取决于数据量的方法的默认终结点可以在一个事务中发送。 该信息包括在返回的数据事务中的设备的设备描述符。

    在响应中，设备发送握手数据包 (\#436 为由**D↓**)。 请注意，PID 值是 ACK （ACK 数据包）。 这指示设备确认该事务。

-   **数据事务**

    现在，让我们看设备返回到请求的响应中。 实际数据传输中数据事务中。

    下面是数据事务的跟踪。

    ![示例数据事务跟踪。](images/datra-trans.png)

    收到 ACK 数据包时，主机将启动数据事务。 若要启动事务，它将发送令牌的数据包 (\#450) 如下所示 （在称为令牌） 的方向。

    在响应中，设备会发送一个数据包 (\#451) 遵循在令牌。 此包包含实际设备描述符。 第一个字节指示设备描述符，18 个字节 (0x12) 的长度。 在此包中的最后一个字节指示最大数据包大小支持的默认终结点。 在这种情况下，我们看到设备可通过其默认终结点一次发送的 8 个字节。

    **请注意**默认终结点的最大数据包大小取决于设备的速度。 高速设备的默认终结点为 64 个字节;较慢的设备是 8 个字节。

    主机通过发送 ACK 数据包确认数据事务 (\#452) 到设备。

    让我们来计算返回的数据量。 在中**并将 wLength**数据包的字段 (\#435) 在安装程序事务中，主机请求 18 个字节。 在数据事务中，我们看到，接收从设备到只有第一个 8 字节的设备描述符。 因此，主机如何接收中剩余的 10 个字节存储的信息？ 设备会在两个事务：8 个字节，然后最后 2 个字节。

    现在，主机知道默认终结点的最大数据包大小，主机开始新的数据事务，并请求数据包的大小的下一个部分。

    下面是下一个数据事务：

    ![示例数据事务跟踪。](images/datra-trans2.png)

    主机通过发送在令牌来启动前面的数据事务 (\#463) 并从设备请求下一步的 8 个字节。 设备会出现数据数据包 (\#464)，其中包含设备描述符的下一步的 8 个字节。

    收到 8 个字节时，主机会发送 ACK 数据包 (\#465) 到设备。

    接下来，该主机，如下所示请求另一个数据事务中的最后一个 2 字节：

    ![示例数据事务跟踪。](images/datra-trans3.png)

    因此，我们看到，为了将 18 个字节从设备传输到主机，主机跟踪的字节传输并启动三个数据事务数 (8 + 8 + 2)。

    **请注意**注意到的数据包数据事务 19，23，26 中的 PID。 PID DATA0 和 DATA1 之间交替。 此序列称为数据切换。 在情况下有多个数据事务，数据切换用于验证数据包序列。 此方法可确保数据包不重复或丢失。

    通过将合并的数据包映射到的设备描述符 (请参阅表 9-8) 结构，我们可以看到这些字段和值：

    | 字段                  | 大小 | ReplTest1  | 描述                                                                       |
    |------------------------|------|--------|-----------------------------------------------------------------------------------|
    | **bLength**            | 1    | 0x12   | 设备描述符，它是 18 个字节的长度。                               |
    | **bDescriptorType**    | 1    | 0x01   | 描述符类型是设备。                                                    |
    | **bcdUSB**             | 2    | 0x0100 | 规范版本编号是 1.00 之间的数值。                                         |
    | **bDeviceClass**       | 1    | 0x00   | 设备类为 0。 在配置中的每个接口都类信息。 |
    | **bDeviceSubClass**    | 1    | 0x00   | 由于设备类为 0，子类是 0。                                          |
    | **bProtocol**          | 1    | 0x00   | 协议为 0。 此设备不使用任何特定于类的协议。             |
    | **bMaxPacketSize0**    | 1    | 0x08   | 终结点的最大数据包大小为 8 个字节。                               |
    | **idVendor**           | 2    | 0x0562 | 电报通信。                                                             |
    | **idProduct**          | 2    | 0x0002 | USB 麦克风。                                                                   |
    | **bcdDevice**          | 2    | 0x0100 | 指示设备发行版号。                                              |
    | **iManufacturer**      | 1    | 0x01   | 制造商的字符串。                                                              |
    | **iProduct**           | 1    | 0x02   | 产品字符串。                                                                   |
    | **iSerialNumber**      | 1    | 0x03   | 序列号。                                                                    |
    | **bNumConfigurations** | 1    | 0x01   | 多个配置。                                                         |



    通过检查这些值，我们有一些有关设备的初步信息。 设备已存在低速 USB 麦克风。 默认终结点的最大数据包大小为 8 个字节。 设备支持的一种配置。

-   **事务状态**

    最后，在主机启动的最后一个事务完成的控制转移： 状态事务。

    ![示例数据事务跟踪。](images/status-trans.png)

    在主机开始事务时与扩展标记数据包 (\#481)。 此数据包的目的是验证设备发送的所有请求数据。 不没有在此状态的事务中发送任何数据包。 设备使用 ACK 数据包进行响应。 如果遇到错误，可能是 PID NAK 或停滞。

## <a name="supported-driver-models"></a>支持的驱动程序模型


### <a name="related-technologies"></a>相关技术

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [WinUSB](winusb.md)

## <a name="prerequisites"></a>系统必备


客户端驱动程序可以枚举管道之前，请确保满足这些要求：

-   客户端驱动程序必须已创建的 framework USB 目标设备对象。

    如果使用 Microsoft Visual Studio Professional 2012 使用提供的 USB 模板，模板代码执行这些任务。 模板代码获取目标设备对象的句柄，并将存储在设备上下文中。

    \* * KMDF 客户端驱动程序: * *

    KMDF 客户端驱动程序必须通过调用获取 WDFUSBDEVICE 句柄[ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法。 详细信息，请参阅"设备源代码"中[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)。

    \* * UMDF 客户端驱动程序: * *

    UMDF 客户端驱动程序必须获取[ **IWDFUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)通过查询框架目标设备对象的指针。 有关详细信息，请参阅"[**IPnpCallbackHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)实现和特定于 USB 的任务"中[了解 USB 客户端驱动程序代码结构 (UMDF)](understanding-the-umdf-template-code-for-usb.md)。

-   控制传输的最重要方面是正确格式设置标记。 发送请求之前, 收集此集的信息：

    -   请求的方向： 主机到设备或主机到设备。
    -   请求的收件人： 设备、 接口、 终结点，或其他。
    -   请求的类别： 标准、 类或供应商。
    -   类型的请求，如 GET\_DESCRIPTPOR 请求。 有关详细信息，请参阅 USB 规范中的部分 9.5。
    -   **wValue**并**wIndex**值。 这些值取决于请求的类型。

    可以从官方 USB 规范来获取所有这些信息。

-   如果你正在编写 UMDF 驱动程序，获取标头文件，Usb\_hw.h 从 OSR USB Fx2 学习工具包 UMDF 示例驱动程序。 此标头文件包含有用的宏和格式设置的控制转移安装数据包的结构。

    所有 UMDF 驱动程序必须与为了发送和接收来自设备的数据的内核模式驱动程序进行都通信。 对于 USB UMDF 驱动程序，内核模式驱动程序始终是由 Microsoft 提供的驱动程序[WinUSB](winusb.md) (Winusb.sys)。

    每当 UMDF 驱动程序发出请求的 USB 驱动程序堆栈，Windows I/O 管理器将请求发送到 WinUSB。 接收请求之后, WinUSB 处理请求或将其转发到 USB 驱动程序堆栈。

## <a name="microsoft-defined-methods-for-sending-control-transfer-requests"></a>Microsoft 定义的方法，用于发送控制传输请求


在主机上的 USB 客户端驱动程序启动的最大限度控制请求，以获取有关设备的信息、 配置设备，或将供应商发送控制命令。 所有这些请求可划分为：

-   标准请求 — 标准请求 USB 规范中定义。 发送这些请求的目的是获取有关设备、 其配置、 接口和终结点的信息。 每个请求的接收方取决于请求的类型。 接收方可以是设备、 接口、 终结点。

    **请注意**控制传输的所有目标始终是默认终结点。 接收方是设备的实体主机有兴趣获取其信息 （描述符、 状态等）。

    这些请求可进一步划分为： 配置请求、 功能请求和状态请求。

    -   配置请求发送以从设备获取信息，以便主机可以配置它，如 GET\_描述符请求。 这些请求也可以是主机发送的设备中设置特定的配置或替代设置的写入请求。
    -   若要启用或禁用设备、 接口或终结点支持某些布尔设备设置的客户端驱动程序发送功能请求。
    -   USB 设备支持状态请求，以启用主机获取或设置设备、 终结点或接口的 USB 定义的状态位。

    有关详细信息，请参阅 USB 规范，版本 2.0 中的部分 9.4。 定义了标准的请求类型的标头文件，Usbspec.h。

-   类请求-由特定设备类规范定义。
-   供应商请求 — 供应商提供，依赖于支持设备的请求。

Microsoft 提供的 USB 堆栈与设备中处理所有协议通信，如前面的跟踪中所示。 驱动程序公开设备驱动程序接口 (DDIs)，使客户端驱动程序将控件传输发送在许多方面。 如果您的客户端驱动程序是一个 Windows Driver Foundation (WDF) 驱动程序，它可以调用例程直接以发送常见控制请求的类型。 WDF KMDF 和 UMDF 本质上支持的控制转移。

未通过 WDF 公开某些类型的控制请求。 对于这些请求，客户端驱动程序可以使用 WDF 混合模型。 此模型允许客户端驱动程序，以生成并格式化 WDM URB 样式请求使用 WDF framework 对象，然后发送这些请求。 混合模型仅适用于内核模式驱动程序。

**对于 UMDF 驱动程序：**

使用的帮助器宏和 usb 中定义的结构\_hw.h。 OSR USB Fx2 学习工具包 UMDF 示例驱动程序包含此标头。

使用此表来确定将控制请求发送到 USB 驱动程序堆栈的最佳方式。 如果无法查看此表，请参阅中的表[本主题](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>如果你想要发送到控件请求...</th>
<th>如果你是 KMDF 驱动程序，使用这些 KMDF DDIs...</th>
<th>如果你是 UMDF 驱动程序，使用这些 UMDF 方法...</th>
<th>如果你是 WDM 驱动程序，生成 URB 结构 （帮助器例程）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>CLEAR_FEATURE:禁用设备，其配置、 接口和终结点中的某些功能设置。 请参阅部分 9.4.1 USB 规范中。</td>
<td><ol>
<li>声明安装数据包。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>结构。</li>
<li>通过调用初始化安装数据包<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a>。</li>
<li>指定接收方的值中定义<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"> <strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>。</li>
<li>指定功能选择器 (<strong>wValue</strong>)。 请参阅中 Usbspec.h USB_FEATURE_XXX 常量。 此外请参阅表 9-6 USB 规范中。</li>
<li>设置<em>SetFeature</em>到<strong>FALSE</strong>。</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><ol>
<li>声明安装数据包。 请参阅<strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h 中声明的结构。</li>
<li>通过调用帮助器宏，初始化安装数据包<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong>usb_hw.h 中定义。</li>
<li>指定接收方的值中定义<strong>WINUSB_BMREQUEST_RECIPIENT</strong>。</li>
<li>指定功能选择器 (<strong>wValue</strong>)。 请参阅<strong>USB_FEATURE_XXX</strong> Usbspec.h 中的常量。 此外请参阅表 9-6 USB 规范中。</li>
<li>设置<em>SetFeature</em>到<strong>FALSE</strong>。</li>
<li>通过将初始化的安装数据包与框架请求对象，传输缓冲区关联通过调用的生成请求<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>方法.</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"> <strong>IWDFIoRequest::Send</strong> </a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>GET_CONFIGURATION:获取当前的 USB 配置。 请参阅部分 9.4.2 USB 规范中。</td>
<td><p>KMDF 默认情况下选择的第一个配置。 若要检索的设备定义的配置号：</p>
<ol>
<li>格式<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>并设置其<strong>bRequest</strong>成员添加到<strong>USB_REQUEST_GET_CONFIGURATION</strong>。</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><p>UMDF 默认情况下选择的第一个配置。 若要检索的设备定义的配置号：</p>
<ol>
<li>声明安装数据包。 请参阅<strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h 中声明的结构。</li>
<li>通过调用帮助器宏，初始化安装数据包<strong>WINUSB_CONTROL_SETUP_PACKET_INIT</strong>usb_hw.h 中定义。</li>
<li>指定<strong>BmRequestToDevice</strong>方向，作为<strong>BmRequestToDevice</strong>作为接收方，并且<strong>USB_REQUEST_GET_CONFIGURATION</strong>与请求。</li>
<li>通过将初始化的安装数据包与框架请求对象，传输缓冲区关联通过调用的生成请求<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>方法.</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"> <strong>IWDFIoRequest::Send</strong> </a>方法。</li>
<li>传输缓冲区中接收配置编号。 通过调用访问该缓冲区<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"> <strong>IWDFMemory</strong> </a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_CONFIGURATION</p></td>
</tr>
<tr class="odd">
<td>GET_DESCRIPTOR:获取设备、 配置、 接口和终结点的描述符。 请参阅部分 9.4.3 USB 规范中。
<p>有关详细信息，请参阅<a href="usb-descriptors.md" data-raw-source="[USB Descriptors](usb-descriptors.md)">USB 描述符</a>。</p></td>
<td><p>调用这些方法：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetEndpointInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation)"><strong>WdfUsbInterfaceGetEndpointInformation</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)"> <strong>WdfUsbTargetPipeGetInformation</strong></a>。 此方法返回终结点中的描述符字段<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_pipe_information" data-raw-source="[&lt;strong&gt;WDF_USB_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)"> <strong>WDF_USB_PIPE_INFORMATION</strong> </a>结构。</li>
</ul></td>
<td><p>调用这些方法：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)"><strong>IWDFUsbInterface::GetInterfaceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)"><strong>IWDFUsbTargetPipe::GetInformation</strong></a>。 此方法返回终结点中的描述符字段<a href="https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information" data-raw-source="[&lt;strong&gt;WINUSB_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)"> <strong>WINUSB_PIPE_INFORMATION</strong> </a>结构。</li>
</ul></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>UsbBuildGetDescriptorRequest</strong></a>)</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_INTERFACE</p></td>
</tr>
<tr class="even">
<td>GET_INTERFACE:获取接口的当前备用设置。 请参阅部分 9.4.4 USB 规范中。</td>
<td><p></p>
<ol>
<li>通过调用获取目标接口对象的 WDFUSBINTERFACE 句柄<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)"> <strong>WdfUsbTargetDeviceGetInterface</strong> </a>方法。</li>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetConfiguredSettingIndex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex)"> <strong>WdfUsbInterfaceGetConfiguredSettingIndex</strong> </a>方法。</li>
</ol></td>
<td><ol>
<li>获取<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)"> <strong>IWDFUsbInterface</strong> </a>指向目标接口对象的指针。</li>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetConfiguredSettingIndex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)"> <strong>IWDFUsbInterface::GetConfiguredSettingIndex</strong> </a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_interface_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_INTERFACE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_interface_request)"><strong>_URB_CONTROL_GET_INTERFACE_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>GET_STATUS:从设备、 终结点或接口获取状态位。 请参阅部分 9.4.5。 中的 USB 规范。</td>
<td><ol>
<li>声明安装数据包。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>结构。</li>
<li>通过调用初始化安装数据包<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong></a>。</li>
<li>指定接收方的值中定义<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"> <strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>。</li>
<li>指定你想要获取其的状态： 设备、 接口或终结点 (<strong>wIndex</strong>)。</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><ol>
<li>声明安装数据包。 请参阅<strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h 中声明的结构。</li>
<li>通过调用帮助器宏，初始化安装数据包<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong>usb_hw.h 中定义。</li>
<li>指定接收方的值中定义<strong>WINUSB_BMREQUEST_RECIPIENT</strong>。</li>
<li>指定你想要获取其的状态： 设备、 接口或终结点 (<strong>wIndex</strong>)。</li>
<li>通过将初始化的安装数据包与框架请求对象，传输缓冲区关联通过调用的生成请求<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>方法.</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"> <strong>IWDFIoRequest::Send</strong> </a>方法。</li>
<li>传输缓冲区中接收的状态值。 通过调用访问该缓冲区<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"> <strong>IWDFMemory</strong> </a>方法。</li>
<li>若要确定是否状态指示自供电、 远程唤醒，请使用三个值中定义<strong>WINUSB_DEVICE_TRAITS</strong>枚举：</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_status_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_STATUS_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_status_request)"><strong>_URB_CONTROL_GET_STATUS_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildgetstatusrequest" data-raw-source="[&lt;strong&gt;UsbBuildGetStatusRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildgetstatusrequest)"><strong>UsbBuildGetStatusRequest</strong></a>)</p>
<p>URB_FUNCTION_GET_STATUS_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_INTERFACE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_STATUS_FROM_OTHER.</p></td>
</tr>
<tr class="even">
<td>SET_ADDRESS:请参阅部分 9.4.6 USB 规范中。</td>
<td>通过 USB 驱动程序堆栈; 处理此请求客户端驱动程序无法执行此操作。</td>
<td>通过 USB 驱动程序堆栈; 处理此请求客户端驱动程序无法执行此操作。</td>
<td>通过 USB 驱动程序堆栈; 处理此请求客户端驱动程序无法执行此操作。</td>
</tr>
<tr class="odd">
<td>SET_CONFIGURATION:将配置设置。 请参阅部分 9.4.7 USB 规范中。
<p>有关详细信息，请参阅<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何为 USB 设备选择一个配置</a>。</p></td>
<td>默认情况下 KMDF 选择默认配置，第一个备用设置中的每个接口。 客户端驱动程序可以通过调用来更改默认配置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfigType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype)"> <strong>WdfUsbTargetDeviceSelectConfigType</strong> </a>方法并指定<strong>WdfUsbTargetDeviceSelectConfigTypeUrb</strong>作为请求选项。 然后，必须设置此请求 URB 的格式并将其提交给 USB 驱动程序堆栈。</td>
<td>默认情况下 UMDF 选择默认配置，第一个备用设置中的每个接口。 客户端驱动程序不能更改配置。</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_configuration" data-raw-source="[&lt;strong&gt;_URB_SELECT_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_configuration)"><strong>_URB_SELECT_CONFIGURATION</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_CONFIGURATION</p></td>
</tr>
<tr class="even">
<td>SET_DESCRIPTOR:更新现有设备、 配置或字符串描述符。 请参阅部分 9.4.8 USB 规范中。
<p>此请求不常使用。 但是，USB 驱动程序堆栈接受此类请求从客户端驱动程序。</p></td>
<td><ol>
<li>分配并生成<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)"> <strong>URB</strong> </a>请求。</li>
<li>指定在传输信息<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"> <strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong> </a>结构。</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForUrb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)"> <strong>WdfUsbTargetDeviceFormatRequestForUrb</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendUrbSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)"> <strong>WdfUsbTargetDeviceSendUrbSynchronously</strong> </a> 。</li>
</ol></td>
<td><ol>
<li>声明安装数据包。 请参阅<strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h 中声明的结构。</li>
<li>指定根据 USB 规范的传输信息。</li>
<li>通过将初始化的安装数据包与框架请求对象，传输缓冲区关联通过调用的生成请求<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>方法.</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"> <strong>IWDFIoRequest::Send</strong> </a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_DEVICE</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SET_FEATURE:启用设备、 其配置、 接口和终结点中的某些功能设置。 请参阅部分 9.4.9 USB 规范中。</td>
<td><ol>
<li>声明安装数据包。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>结构。</li>
<li>通过调用初始化安装数据包<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a>。</li>
<li>指定收件人 （设备、 接口、 终结点） 中定义的值<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"> <strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>。</li>
<li>指定功能选择器 (<strong>wValue</strong>)。 请参阅中 Usbspec.h USB_FEATURE_XXX 常量。 此外请参阅表 9-6 USB 规范中。</li>
<li>设置<em>SetFeature</em>到<strong>，则返回 TRUE</strong></li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><ol>
<li>声明安装数据包。 请参阅<strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h 中声明的结构。</li>
<li>通过调用帮助器宏，初始化安装数据包<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong>usb_hw.h 中定义。</li>
<li>指定接收方的值中定义<strong>WINUSB_BMREQUEST_RECIPIENT</strong>。</li>
<li>指定功能选择器 (<strong>wValue</strong>)。 请参阅<strong>USB_FEATURE_XXX</strong> Usbspec.h 中的常量。 此外请参阅表 9-6 USB 规范中。</li>
<li>设置<em>SetFeature</em>到<strong>TRUE</strong>。</li>
<li>通过将初始化的安装数据包与框架请求对象，传输缓冲区关联通过调用的生成请求<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>方法.</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"> <strong>IWDFIoRequest::Send</strong> </a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_SET_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>SET_INTERFACE:在接口中的备用设置更改。 请参阅部分 9.4.9 USB 规范中。
<p>有关详细信息，请参阅<a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">如何在 USB 界面中选择一项备用设置</a>。</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a>
<p></p>
<ol>
<li>获取目标接口对象的 WDFUSBINTERFACE 句柄。</li>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)"> <strong>WdfUsbInterfaceSelectSetting</strong> </a>方法。</li>
</ol></td>
<td><ol>
<li>获取<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)"> <strong>IWDFUsbInterface</strong> </a>指向目标接口对象的指针。</li>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)"> <strong>IWDFUsbInterface::SelectSetting</strong> </a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_interface" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_interface)"><strong>_URB_SELECT_INTERFACE</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)"><strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SYNC_FRAME:设置和获取与终结点的同步的帧数。 请参阅部分 9.4.10 USB 规范中。</td>
<td>通过 USB 驱动程序堆栈; 处理此请求客户端驱动程序无法执行此操作。</td>
<td>通过 USB 驱动程序堆栈; 处理此请求客户端驱动程序无法执行此操作。</td>
<td>通过 USB 驱动程序堆栈; 处理此请求客户端驱动程序无法执行此操作。</td>
</tr>
<tr class="even">
<td>为设备特定于类的请求和供应商命令。</td>
<td><ol>
<li>声明安装数据包。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>结构。</li>
<li>通过调用初始化安装数据包<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS</strong></a>的特定请求或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong></a>供应商命令。</li>
<li>指定收件人 （设备、 接口、 终结点） 中定义的值<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"> <strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>。</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><ol>
<li>声明安装数据包。 请参阅<strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h 中声明的结构。</li>
<li>通过调用帮助器宏，初始化安装数据包<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_CLASS</strong>或<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong>usb_hw.h 中定义。</li>
<li>指定的方向 (请参阅<strong>WINUSB_BMREQUEST_DIRECTION</strong>枚举)，接收方 (请参阅<strong>WINUSB_BMREQUEST_RECIPIENT</strong>枚举)，并在类中所述的请求或硬件规格。</li>
<li>通过将初始化的安装数据包与框架请求对象，传输缓冲区关联通过调用的生成请求<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>方法.</li>
<li>将请求发送通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"> <strong>IWDFIoRequest::Send</strong> </a>方法。</li>
<li>从传输缓冲区中的设备接收信息。 通过调用访问该缓冲区<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"> <strong>IWDFMemory</strong> </a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_vendor_or_class_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_VENDOR_OR_CLASS_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_vendor_or_class_request)"><strong>_URB_CONTROL_VENDOR_OR_CLASS_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538986(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildVendorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538986(v=vs.85))"><strong>UsbBuildVendorRequest</strong></a>)</p>
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



## <a name="how-to-send-a-control-transfer-for-vendor-commands---kmdf"></a>如何发送供应商命令-KMDF 控制传输


此过程演示如何控制传输发送客户端驱动程序。 在此示例中，客户端驱动程序将发送从设备检索固件版本的供应商命令。

1.  声明该供应商命令的常量。 研究硬件规范，并确定你想要使用的供应商命令。
2.  声明[ **WDF\_内存\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor)结构，并将其初始化通过调用[ **WDF\_内存\_描述符\_INIT\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552392_init_buffer)宏。 USB 驱动程序完成请求后，此结构将从设备接收响应。
3.  具体取决于是否同步或异步发送请求，指定发送的选项：
    -   如果发送请求以同步方式通过调用[ **WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)，指定超时值。 此值非常重要，因为没有超时，您可以阻止该线程无限期。

        对于此操作，请声明[ **WDF\_请求\_发送\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_send_options)结构，并将其初始化通过调用[ **WDF\_请求\_发送\_选项\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552491_init)宏。 选项指定**WDF\_请求\_发送\_选项\_超时**。

        接下来，通过调用设置的超时值[ **WDF\_请求\_发送\_选项\_设置\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdf_request_send_options_set_timeout)宏。

    -   如果要以异步方式发送请求，实现完成例程。 免费完成例程中的所有已分配的资源。

4.  声明[ **WDF\_USB\_控制\_安装\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)结构，以包含 token 安装程序并设置格式结构。 若要执行此操作，调用[ **WDF\_USB\_控制\_安装\_数据包\_INIT\_供应商**](https://msdn.microsoft.com/library/windows/hardware/ff552568_init_vendor)宏来设置格式设置数据包。 在调用中指定，请求、 接收方、 发送请求选项 （在步骤 3 中初始化） 和供应商命令常量的方向。
5.  将请求发送通过调用[ **WdfUsbTargetDeviceSendControlTransferSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)或[ **WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer).
6.  检查由框架返回的 NTSTATUS 值，并检查接收的值。

此代码示例将控制传输请求发送给 USB 设备，以检索其固件版本。 同步发送请求和客户端驱动程序指定的相对的超时值为 5 秒 （以 100 毫微秒为单位）。 该驱动程序存储在驱动程序定义的设备上下文中接收到的响应。

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

##<a name="how-to-send-a-control-transfer-for-get_status---umdf"></a>如何将发送 GET 控制传输\_状态-UMDF


此过程说明如何客户端驱动程序可以发送 GET 控制传输\_状态命令。 请求的接收方是设备，并请求获取信息以位为单位 D1 D0。 有关详细信息，请参阅 USB 规范中的图 9-4。

1.  包括标头文件 Usb\_hw.h 附带 OSR USB Fx2 学习工具包 UMDF 示例驱动程序。
2.  声明**WINUSB\_控制\_安装程序\_数据包**结构。
3.  通过调用帮助器宏，初始化安装数据包**WINUSB\_控制\_安装程序\_数据包\_INIT\_获取\_状态**。
4.  指定**BmRequestToDevice**作为接收方。
5.  指定在 0*索引*值。
6.  调用帮助器方法 SendControlTransferSynchronously 以同步方式发送请求。

    帮助器方法生成请求通过将初始化的安装数据包与框架请求对象，传输缓冲区关联通过调用[ **IWDFUsbTargetDevice::FormatRequestForControlTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)方法。 帮助器方法然后将请求发送通过调用[ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)方法。 该方法返回后，检查返回的值。

7.  若要确定是否状态指示自供电、 远程唤醒，请使用这些值中定义**WINUSB\_设备\_特征**枚举：

此代码示例将控制传输请求发送到获取设备的状态。 该示例通过调用名为 SendControlTransferSynchronously 的帮助器方法以同步方式发送请求。

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

下面的代码示例显示了名为 SendControlTransferSynchronously 的帮助器方法的实现。 此方法以同步方式发送请求。

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


如果您使用 Winusb.sys 作为功能驱动程序为你的设备，可以从应用程序发送的控制转移。 若要设置格式 WinUSB 中的安装程序数据包，请使用 UMDF 帮助器宏和结构，本主题中的表中所述。 若要发送请求，调用[ **WinUsb\_ControlTransfer** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)函数。








