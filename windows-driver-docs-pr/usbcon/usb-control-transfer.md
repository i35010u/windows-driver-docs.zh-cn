---
Description: 本主题介绍了控件传输的结构，以及客户端驱动程序应如何向设备发送控制请求。
title: 如何发送 USB 控制传输
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 6b36ef04e75ced0c51a1c145024ee67db01ddfee
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007593"
---
# <a name="how-to-send-a-usb-control-transfer"></a>如何发送 USB 控制传输


本主题介绍了控件传输的结构，以及客户端驱动程序应如何向设备发送控制请求。

本主题内容：

-   [关于默认终结点](#about-the-default-endpoint)
-   [控件传输布局](#layout-of-a-control-transfer)
-   [支持的驱动程序模型](#supported-driver-models)
    -   [相关技术](#related-technologies)
-   [必备条件](#prerequisites)
-   [用于发送控制传输请求的 Microsoft 定义的方法](#microsoft-defined-methods-for-sending-control-transfer-requests)
-   [如何为供应商命令发送控件传输-KMDF](#how-to-send-a-control-transfer-for-vendor-commands---kmdf)
-   [如何为 GET @ no__t 发送控件传输-1STATUS](#how-to-send-a-control-transfer-for-get_status---umdf)

## <a name="about-the-default-endpoint"></a>关于默认终结点


所有 USB 设备必须至少支持一个名为 "*默认终结*点" 的终结点。 针对默认终结点的任何传输称为 "*控制传输*"。 控制传输的目的是使主机能够获取设备信息、配置设备或执行设备独有的控制操作。

首先，我们将研究默认终结点的这些特性。

-   默认终结点的地址是0。
-   默认终结点是双向的，也就是说，主机可以将数据发送到终结点，并在一次传输内接收数据。
-   默认终结点在设备级别提供，不在设备的任何接口中定义。
-   当主机和设备之间建立连接后，默认终结点就会处于活动状态。 即使在选择配置之前仍处于活动状态。
-   默认终结点的最大数据包大小取决于设备的总线速度。 低速、8字节;完整和高速，64字节;SuperSpeed，512字节。

## <a name="layout-of-a-control-transfer"></a>控件传输布局


由于控制传输为高优先级传输，因此主机将在总线上保留一定量的带宽。 对于低和全速设备，为 10% 的带宽;SuperSpeed 传输设备的 20%。 现在，让我们看看控件传输的布局。

![usb 控件传输](images/control-transfer.png)

控件传输分为三个事务： "*设置事务*"、"*数据事务*" 和 "*状态事务*"。 每个事务都包含三种类型的数据包：*令牌数据包*、*数据包*和*握手数据包*。

某些字段对所有包都是通用的。 这些字段是：

-   指示数据包开始的 "同步" 字段。
-   指示数据包类型的数据包标识符（PID）、事务的方向以及握手数据包的情况，表示事务的成功或失败。
-   EOP 字段指示数据包的结尾。

其他字段依赖于数据包类型。

-   **令牌数据包**

    每个安装事务都以令牌数据包开始。 下面是数据包的结构。 主机始终发送令牌包。

    ![令牌数据包布局](images/token.png)

    PID 值指示令牌数据包的类型。 下面是可能的值：

    -   程序指示控件传输中的设置事务的开始。
    -   中指示主机正在从设备请求数据（读取大小写）。
    -   弄指示主机将数据发送到设备（写入大小写）。
    -   S （属于指示帧的开头。 这种类型的令牌数据包包含11位帧号。 主机发送 S (属于数据包。 发送此数据包的频率取决于总线速度。 为了全速，主机每1millisecond 发送数据包;高速总线上每125微秒。

<!-- -->

-   **数据包**

    紧跟令牌数据包后，就是包含有效负载的数据包。 每个数据包可以包含的字节数取决于默认终结点的最大数据包大小。 根据传输方向，该主机或设备可以发送该数据包。

    ![数据数据包布局](images/data.png)

<!-- -->

-   **握手数据包**

    紧跟在数据包后面是握手数据包。 数据包的 PID 指示主机或设备是否接收了数据包。 根据传输方向，该主机或设备可以发送握手数据包。

    ![握手数据包布局](images/handshake.png)

可以通过使用任何 USB 分析器，如 Beagle、Ellisys、LeCroy USB 协议分析器来查看事务和数据包的结构。 分析器设备显示数据是如何通过网络发送或接收的。 在此示例中，我们将检查 LeCroy USB 分析器捕获的一些跟踪。 此示例仅供参考。 这不是 Microsoft 的认可。

-   **设置事务**

    宿主始终启动控件传输。 它通过发送安装事务来实现此目的。 此事务包含一个名为*安装程序令牌*的令牌数据包，后跟8个字节的数据包。 此屏幕截图显示了一个示例安装程序事务。

    ![安装事务的跟踪。](images/setup-trans.png)

    在前面的跟踪中，主机通过发送安装令牌数据包 1434 @no__t （由**H ↓**指示）控制传输。 请注意，PID 指定了用于指示安装令牌的设置。 PID 后跟终结点的设备地址和地址。 对于控件传输，该终结点地址始终为0。

    接下来，主机将数据包 @no__t 发送到0435。 PID 为 DATA0，该值用于数据包排序（要讨论）。 PID 后跟8个字节，其中包含与此请求有关的主要信息。 这8个字节表示请求的类型，以及设备将在其中写入其响应的缓冲区大小。

    按相反顺序接收所有字节。 如9.3 节所述，我们将看到以下字段和值：

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
    <th>Size</th>
    <th>ReplTest1</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>bmRequestType</strong> （请参阅 9.3.1 bmRequestType）</td>
    <td>1</td>
    <td>0x80</td>
    <td><p>数据传输方向来自设备到主机（D7 为1）</p>
    <p>请求是标准请求（D6 。D5 为0）</p>
    <p>请求的接收方是设备（D4 是0）</p></td>
    </tr>
    <tr class="even">
    <td><strong>bRequest</strong> （请参阅9.3.2 和表9-4）</td>
    <td>1</td>
    <td>0x06</td>
    <td>请求类型为 GET_DESCRIPTOR。</td>
    </tr>
    <tr class="odd">
    <td><strong>wValue</strong> （请参阅表9-5）</td>
    <td>2</td>
    <td>0x0100</td>
    <td>请求值指示描述符类型为 "设备"。</td>
    </tr>
    <tr class="even">
    <td><strong>wIndex</strong>（请参阅9.3.4 部分）</td>
    <td>2</td>
    <td>0x0000</td>
    <td><p>方向是从主机到设备（D7 为1）</p>
    <p>终结点编号为0。</p></td>
    </tr>
    <tr class="odd">
    <td><strong>wLength</strong> （请参阅9.3.5 部分）</td>
    <td>2</td>
    <td>0x0012</td>
    <td>请求是检索18个字节。</td>
    </tr>
    </tbody>
    </table>

    这样，我们就可以得出这样的结论：在此控制（读取）传输中，主机发送一个请求来检索设备描述符，并将18个字节指定为保留该描述符的传输长度。 设备发送这18个字节的方式取决于默认终结点可在一个事务中发送的数据量。 该信息包含在设备在数据事务中返回的设备描述符中。

    作为响应，设备发送握手数据包（\#436，由**D ↓**表示）。 请注意，PID 值为 ACK （ACK 数据包）。 这表明设备确认了该事务。

-   **数据事务**

    现在，让我们看看设备为响应请求而返回的内容。 在数据事务中传输实际数据。

    下面是数据事务的跟踪。

    ![示例数据事务的跟踪。](images/datra-trans.png)

    收到 ACK 数据包后，主机将启动数据事务。 若要启动该事务，它将发送一个与 IN （在令牌中称为）方向相同的令牌数据包（\#450）。

    在响应中，设备发送在令牌后面的数据包（\#451）。 此数据包包含实际的设备描述符。 第一个字节指示设备描述符的长度，18个字节（0x12）。 此数据包中的最后一个字节指示默认终结点支持的最大数据包大小。 在这种情况下，我们发现设备每次可以通过其默认终结点发送8个字节。

    **注意** 默认终结点的最大数据包大小取决于设备的速度。 高速设备的默认终结点为64字节;低速设备是8个字节。

    主机通过向设备发送 ACK 数据包（\#452）来确认数据事务。

    让我们来计算返回的数据量。 在安装程序事务中的数据包（\#435）的**wLength**字段中，主机请求了18个字节。 在数据事务中，我们看到只从设备接收到了前8个字节的设备描述符。 那么，主机如何接收存储在剩余10个字节中的信息呢？ 设备在两个事务中执行此操作：8字节，最后2个字节。

    既然主机知道了默认终结点的最大数据包大小，主机就会启动新的数据事务，并根据数据包大小请求下一部分。

    下面是下一个数据事务：

    ![示例数据事务的跟踪。](images/datra-trans2.png)

    主机通过发送令牌（\#463）并从设备请求接下来的8个字节来启动前面的数据事务。 设备使用数据包（\#464）进行响应，该数据包包含设备描述符的后8个字节。

    接收到8个字节后，主机会将 ACK 数据包（\#465）发送到设备。

    接下来，主机在另一个数据事务中请求最后2个字节，如下所示：

    ![示例数据事务的跟踪。](images/datra-trans3.png)

    因此，我们发现，要将18个字节从设备传输到主机，主机将跟踪传输的字节数和启动的三个数据事务（8 + 8 + 2）。

    **注意**  请注意数据事务19，23，26中的数据包 PID。 PID 在 DATA0 和 DATA1 之间交替。 此顺序称为数据切换。 在存在多个数据事务的情况下，将使用数据切换来验证数据包序列。 此方法可确保数据包不会重复或丢失。

    通过将合并的数据包映射到设备描述符的结构（请参阅表9-8），我们可以看到以下字段和值：

    | 字段                  | Size | ReplTest1  | 描述                                                                       |
    |------------------------|------|--------|-----------------------------------------------------------------------------------|
    | **bLength**            | 1    | 0x12   | 设备描述符的长度，即18个字节。                               |
    | **bDescriptorType**    | 1    | 0x01   | 描述符类型为 "设备"。                                                    |
    | **bcdUSB**             | 2    | 0x0100 | 规范版本号为1.00。                                         |
    | **bDeviceClass**       | 1    | 0x00   | 设备类为0。 配置中的每个接口都具有类信息。 |
    | **bDeviceSubClass**    | 1    | 0x00   | 子类为0，因为设备类为0。                                          |
    | **bProtocol**          | 1    | 0x00   | 协议为0。 此设备不使用任何特定于类的协议。             |
    | **bMaxPacketSize0**    | 1    | 0x08   | 终结点的最大数据包大小为8个字节。                               |
    | **idVendor**           | 2    | 0x0562 | 电传通信。                                                             |
    | **idProduct**          | 2    | 0x0002 | USB 麦克风。                                                                   |
    | **bcdDevice**          | 2    | 0x0100 | 指示设备发布号。                                              |
    | **iManufacturer**      | 1    | 0x01   | 制造商字符串。                                                              |
    | **iProduct**           | 1    | 0x02   | 产品字符串。                                                                   |
    | **iSerialNumber**      | 1    | 0x03   | 序列号。                                                                    |
    | **bNumConfigurations** | 1    | 0x01   | 配置数。                                                         |



    通过检查这些值，我们有一些有关设备的初步信息。 设备是低速 USB 麦克风。 默认终结点的最大数据包大小为8个字节。 设备支持一种配置。

-   **状态事务**

    最后，主机通过启动最后一个事务：状态事务来完成控制传输。

    ![示例数据事务的跟踪。](images/status-trans.png)

    主机使用输出令牌数据包（\#481）启动该事务。 此数据包的用途是验证设备是否发送了所有请求的数据。 此状态事务中没有发送任何数据包。 设备使用 ACK 数据包进行响应。 如果发生错误，PID 可能是 NAK 或卡住。

## <a name="supported-driver-models"></a>支持的驱动程序模型


### <a name="related-technologies"></a>相关技术

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [WinUSB](winusb.md)

## <a name="prerequisites"></a>先决条件


在客户端驱动程序可以枚举管道之前，请确保满足以下要求：

-   客户端驱动程序必须已创建框架 USB 目标设备对象。

    如果使用的是随 Microsoft Visual Studio Professional 2012 一起提供的 USB 模板，则模板代码将执行这些任务。 模板代码获取目标设备对象的句柄，并将其存储在设备上下文中。

    \* * KMDF 客户端驱动程序： * *

    KMDF 客户端驱动程序必须通过调用[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法获取 WDFUSBDEVICE 句柄。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构（KMDF）中的](understanding-the-kmdf-template-code-for-usb.md)"设备源代码"。

    \* * UMDF 客户端驱动程序： * *

    UMDF 客户端驱动程序必须通过查询框架目标设备对象来获取[**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)指针。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构（UMDF）](understanding-the-umdf-template-code-for-usb.md)中的 "[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)实现和特定于 USB 的任务"。

-   控件传输的最重要方面是正确设置设置令牌的格式。 在发送请求之前，请收集以下信息集：

    -   请求方向：主机到设备或要托管的设备。
    -   请求的接收方：设备、接口、终结点或其他。
    -   请求类别：标准、类或供应商。
    -   请求的类型，例如 GET @ no__t-0DESCRIPTPOR 请求。 有关详细信息，请参阅 USB 规范中的9.5 节。
    -   **wValue**和**wIndex**值。 这些值取决于请求的类型。

    你可以从官方 USB 规范获取所有这些信息。

-   如果你正在编写一个 UMDF 驱动程序，请从 OSR USB Fx2 学习工具包的 UMDF 示例驱动程序获取头文件、Usb @ no__t-0hw。 此标头文件包含用于设置控件传输的安装包格式的有用宏和结构。

    所有 UMDF 驱动程序必须与内核模式驱动程序通信，以便从设备发送和接收数据。 对于 USB UMDF 驱动程序，内核模式驱动程序始终是 Microsoft 提供的驱动程序[WinUSB](winusb.md) （WinUSB）。

    每当 UMDF 驱动程序发出对 USB 驱动程序堆栈的请求时，Windows i/o 管理器都会向 WinUSB 发送请求。 收到请求后，WinUSB 将处理该请求或将其转发到 USB 驱动程序堆栈。

## <a name="microsoft-defined-methods-for-sending-control-transfer-requests"></a>用于发送控制传输请求的 Microsoft 定义的方法


主机上的 USB 客户端驱动程序将启动大多数控制请求，以获取有关设备的信息、配置设备或发送供应商控制命令。 所有这些请求均可分类为：

-   标准请求-标准请求是在 USB 规范中定义的。 发送这些请求的目的是获取有关设备、其配置、接口和终结点的信息。 每个请求的接收方取决于请求的类型。 接收方可以是设备、接口、终结点。

    **注意** 任何控件传输的目标始终是默认终结点。 接收方是设备的实体，其信息（描述符、状态等）会对主机感兴趣。

    可以进一步将这些请求归类为：配置请求、功能请求和状态请求。

    -   发送配置请求以从设备获取信息，以便主机可以对其进行配置，例如 GET @ no__t-0DESCRIPTOR 请求。 这些请求还可以是主机发送的、用于设置设备中特定配置或备用设置的写入请求。
    -   功能请求由客户端驱动程序发送，用于启用或禁用设备、接口或终结点支持的某些布尔设备设置。
    -   USB 设备支持状态请求，以允许主机获取或设置设备、终结点或接口的 USB 定义的状态位。

    有关详细信息，请参阅2.0 中的9.4 节。 标准请求类型定义了标头文件 Usbspec。

-   类请求-由特定的设备类规范定义。
-   供应商请求-由供应商提供，取决于设备支持的请求。

Microsoft 提供的 USB 堆栈处理与设备的所有协议通信，如前面的跟踪中所示。 驱动程序公开设备驱动程序接口（DDIs），使客户端驱动程序可以通过多种方式发送控制传输。 如果客户端驱动程序是 Windows Driver Foundation （WDF）驱动程序，它可以直接调用例程来发送常见类型的控制请求。 WDF 支持 KMDF 和 UMDF 的控件传输。

某些类型的控制请求不通过 WDF 公开。 对于这些请求，客户端驱动程序可以使用 WDF 混合模型。 此模型允许客户端驱动程序生成 WDM URB 样式请求并设置其格式，然后使用 WDF 框架对象发送这些请求。 混合模型仅适用于内核模式驱动程序。

**对于 UMDF 驱动程序：**

使用在 usb @ no__t-0hw 中定义的帮助程序宏和结构。 此标头包含在 OSR USB Fx2 学习工具包的 UMDF 示例驱动程序中。

使用此表来确定将控制请求发送到 USB 驱动程序堆栈的最佳方式。 如果无法查看此表，请参阅[本主题](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)中的表。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>如果要将控制请求发送到 。</th>
<th>如果你是 KMDF 驱动程序，请使用这些 KMDF DDIs 。</th>
<th>如果你是 UMDF 驱动程序，请使用以下 UMDF 方法 。</th>
<th>如果您是 WDM 驱动程序，则生成 URB 结构（Helper 例程）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>CLEAR_FEATURE:禁用设备、其配置、接口和终结点中的某些功能设置。 请参阅 USB 规范中的9.4.1 部分。</td>
<td><ol>
<li>声明安装包。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>结构。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a>初始化安装包。</li>
<li>指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>中定义的收件人值。</li>
<li>指定功能选择器（<strong>wValue</strong>）。 请参阅 Usbspec 中的 USB_FEATURE_XXX 常量。 另请参阅 USB 规范中的表9-6。</li>
<li>将<em>SetFeature</em>设置为<strong>FALSE</strong>。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>发送请求。</li>
</ol></td>
<td><ol>
<li>声明安装包。 请参阅 usb_hw 中声明的<strong>WINUSB_CONTROL_SETUP_PACKET</strong>结构。</li>
<li>通过调用在 usb_hw 中定义的 helper 宏<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong>初始化安装包。</li>
<li>指定在<strong>WINUSB_BMREQUEST_RECIPIENT</strong>中定义的收件人值。</li>
<li>指定功能选择器（<strong>wValue</strong>）。 请参阅 Usbspec 中的<strong>USB_FEATURE_XXX</strong>常量。 另请参阅 USB 规范中的表9-6。</li>
<li>将<em>SetFeature</em>设置为<strong>FALSE</strong>。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice：： FormatRequestForControlTransfer</strong></a>方法，通过将初始化的安装包与框架请求对象和传输缓冲区关联来生成请求。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest：： send</strong></a>方法发送请求。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>（<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>）</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>GET_CONFIGURATION:获取当前的 USB 配置。 请参阅 USB 规范中的9.4.2 部分。</td>
<td><p>默认情况下，KMDF 选择第一个配置。 检索设备定义的配置编号：</p>
<ol>
<li>格式化<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>并将其<strong>bRequest</strong>成员设置为<strong>USB_REQUEST_GET_CONFIGURATION</strong>。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>发送请求。</li>
</ol></td>
<td><p>UMDF 默认情况下选择第一个配置。 检索设备定义的配置编号：</p>
<ol>
<li>声明安装包。 请参阅 usb_hw 中声明的<strong>WINUSB_CONTROL_SETUP_PACKET</strong>结构。</li>
<li>通过调用在 usb_hw 中定义的 helper 宏<strong>WINUSB_CONTROL_SETUP_PACKET_INIT</strong>初始化安装包。</li>
<li>将<strong>BmRequestToDevice</strong>指定为方向，将<strong>BmRequestToDevice</strong>指定为接收方，将<strong>USB_REQUEST_GET_CONFIGURATION</strong>指定为请求。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice：： FormatRequestForControlTransfer</strong></a>方法，通过将初始化的安装包与框架请求对象和传输缓冲区关联来生成请求。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest：： send</strong></a>方法发送请求。</li>
<li>接收传输缓冲区中的配置编号。 通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a>方法访问该缓冲区。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_CONFIGURATION</p></td>
</tr>
<tr class="odd">
<td>GET_DESCRIPTOR:获取设备、配置、接口和终结点描述符。 请参阅 USB 规范中的9.4.3 部分。
<p>有关详细信息，请参阅<a href="usb-descriptors.md" data-raw-source="[USB Descriptors](usb-descriptors.md)">USB 描述符</a>。</p></td>
<td><p>调用以下方法：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetEndpointInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation)"><strong>WdfUsbInterfaceGetEndpointInformation</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)"><strong>WdfUsbTargetPipeGetInformation</strong></a>。 此方法在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_pipe_information" data-raw-source="[&lt;strong&gt;WDF_USB_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)"><strong>WDF_USB_PIPE_INFORMATION</strong></a>结构中返回终结点描述符字段。</li>
</ul></td>
<td><p>调用以下方法：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)"><strong>IWDFUsbInterface::GetInterfaceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)"><strong>IWDFUsbTargetPipe：： GetInformation</strong></a>。 此方法在<a href="https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information" data-raw-source="[&lt;strong&gt;WINUSB_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)"><strong>WINUSB_PIPE_INFORMATION</strong></a>结构中返回终结点描述符字段。</li>
</ul></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>（<a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>UsbBuildGetDescriptorRequest</strong></a>）</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_INTERFACE</p></td>
</tr>
<tr class="even">
<td>GET_INTERFACE:获取接口的当前替代设置。 请参阅 USB 规范中的9.4.4 部分。</td>
<td><p></p>
<ol>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)"><strong>WdfUsbTargetDeviceGetInterface</strong></a>方法获取目标接口对象的 WDFUSBINTERFACE 句柄。</li>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetConfiguredSettingIndex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex)"><strong>WdfUsbInterfaceGetConfiguredSettingIndex</strong></a>方法。</li>
</ol></td>
<td><ol>
<li>获取指向目标接口对象的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)"><strong>IWDFUsbInterface</strong></a>指针。</li>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetConfiguredSettingIndex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)"><strong>IWDFUsbInterface：： GetConfiguredSettingIndex</strong></a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_interface_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_INTERFACE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_interface_request)"><strong>_URB_CONTROL_GET_INTERFACE_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>GET_STATUS:从设备、终结点或接口获取状态位。 请参阅9.4.5 部分。 在 USB 规范中。</td>
<td><ol>
<li>声明安装包。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>结构。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong></a>初始化安装包。</li>
<li>指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>中定义的收件人值。</li>
<li>指定要获取的状态：设备、接口或终结点（<strong>wIndex</strong>）。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>发送请求。</li>
</ol></td>
<td><ol>
<li>声明安装包。 请参阅 usb_hw 中声明的<strong>WINUSB_CONTROL_SETUP_PACKET</strong>结构。</li>
<li>通过调用在 usb_hw 中定义的 helper 宏<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong>初始化安装包。</li>
<li>指定在<strong>WINUSB_BMREQUEST_RECIPIENT</strong>中定义的收件人值。</li>
<li>指定要获取的状态：设备、接口或终结点（<strong>wIndex</strong>）。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice：： FormatRequestForControlTransfer</strong></a>方法，通过将初始化的安装包与框架请求对象和传输缓冲区关联来生成请求。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest：： send</strong></a>方法发送请求。</li>
<li>接收传输缓冲区中的状态值。 通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a>方法访问该缓冲区。</li>
<li>若要确定状态是否指示自驱动的远程唤醒，请使用<strong>WINUSB_DEVICE_TRAITS</strong>枚举中定义的三个值：</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_status_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_STATUS_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_status_request)"><strong>_URB_CONTROL_GET_STATUS_REQUEST</strong></a></p>
<p>（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildgetstatusrequest" data-raw-source="[&lt;strong&gt;UsbBuildGetStatusRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildgetstatusrequest)"><strong>UsbBuildGetStatusRequest</strong></a>）</p>
<p>URB_FUNCTION_GET_STATUS_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_INTERFACE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_STATUS_FROM_OTHER.</p></td>
</tr>
<tr class="even">
<td>SET_ADDRESS:请参阅 9.4.6 in USB 规范部分。</td>
<td>此请求由 USB 驱动程序堆栈处理;客户端驱动程序无法执行此操作。</td>
<td>此请求由 USB 驱动程序堆栈处理;客户端驱动程序无法执行此操作。</td>
<td>此请求由 USB 驱动程序堆栈处理;客户端驱动程序无法执行此操作。</td>
</tr>
<tr class="odd">
<td>SET_CONFIGURATION:设置配置。 请参阅 9.4.7 in USB 规范部分。
<p>有关详细信息，请参阅<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何为 USB 设备选择配置</a>。</p></td>
<td>默认情况下，KMDF 选择每个接口中的默认配置和首个替代设置。 客户端驱动程序可以通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfigType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype)"><strong>WdfUsbTargetDeviceSelectConfigType</strong></a>方法并将<strong>WdfUsbTargetDeviceSelectConfigTypeUrb</strong>指定为 request 选项来更改默认配置。 然后，必须为此请求设置 URB 的格式，并将其提交到 USB 驱动程序堆栈。</td>
<td>默认情况下，UMDF 选择每个接口中的默认配置和首选项设置。 客户端驱动程序无法更改配置。</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_configuration" data-raw-source="[&lt;strong&gt;_URB_SELECT_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_configuration)"><strong>_URB_SELECT_CONFIGURATION</strong></a></p>
<p>（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a>）</p>
<p>URB_FUNCTION_SELECT_CONFIGURATION</p></td>
</tr>
<tr class="even">
<td>SET_DESCRIPTOR:更新现有设备、配置或字符串描述符。 请参阅 9.4.8 in USB 规范部分。
<p>此请求不常用。 但是，USB 驱动程序堆栈接受来自客户端驱动程序的此类请求。</p></td>
<td><ol>
<li>为请求分配和生成<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)"><strong>URB</strong></a> 。</li>
<li>在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a>结构中指定传输信息。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForUrb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)"><strong>WdfUsbTargetDeviceFormatRequestForUrb</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendUrbSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)"><strong>WdfUsbTargetDeviceSendUrbSynchronously</strong></a>发送请求。</li>
</ol></td>
<td><ol>
<li>声明安装包。 请参阅 usb_hw 中声明的<strong>WINUSB_CONTROL_SETUP_PACKET</strong>结构。</li>
<li>按照 USB 规范指定传输信息。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice：： FormatRequestForControlTransfer</strong></a>方法，通过将初始化的安装包与框架请求对象和传输缓冲区关联来生成请求。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest：： send</strong></a>方法发送请求。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_DEVICE</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SET_FEATURE:启用设备、其配置、接口和终结点中的某些功能设置。 请参阅 USB 规范中的9.4.9 部分。</td>
<td><ol>
<li>声明安装包。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>结构。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a>初始化安装包。</li>
<li>指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>中定义的收件人值（设备、接口、终结点）。</li>
<li>指定功能选择器（<strong>wValue</strong>）。 请参阅 Usbspec 中的 USB_FEATURE_XXX 常量。 另请参阅 USB 规范中的表9-6。</li>
<li>将<em>SetFeature</em>设置为<strong>TRUE</strong></li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>发送请求。</li>
</ol></td>
<td><ol>
<li>声明安装包。 请参阅 usb_hw 中声明的<strong>WINUSB_CONTROL_SETUP_PACKET</strong>结构。</li>
<li>通过调用在 usb_hw 中定义的 helper 宏<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong>初始化安装包。</li>
<li>指定在<strong>WINUSB_BMREQUEST_RECIPIENT</strong>中定义的收件人值。</li>
<li>指定功能选择器（<strong>wValue</strong>）。 请参阅 Usbspec 中的<strong>USB_FEATURE_XXX</strong>常量。 另请参阅 USB 规范中的表9-6。</li>
<li>将<em>SetFeature</em>设置为<strong>TRUE</strong>。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice：： FormatRequestForControlTransfer</strong></a>方法，通过将初始化的安装包与框架请求对象和传输缓冲区关联来生成请求。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest：： send</strong></a>方法发送请求。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>（<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>）</p>
<p>URB_FUNCTION_SET_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>SET_INTERFACE:更改界面中的备用设置。 请参阅 USB 规范中的9.4.9 部分。
<p>有关详细信息，请参阅<a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">如何在 USB 接口中选择替代设置</a>。</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a>
<p></p>
<ol>
<li>获取目标接口对象的 WDFUSBINTERFACE 句柄。</li>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)"><strong>WdfUsbInterfaceSelectSetting</strong></a>方法。</li>
</ol></td>
<td><ol>
<li>获取指向目标接口对象的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)"><strong>IWDFUsbInterface</strong></a>指针。</li>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)"><strong>IWDFUsbInterface：： SelectSetting</strong></a>方法。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_interface" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_interface)"><strong>_URB_SELECT_INTERFACE</strong></a></p>
<p>（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)"><strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong></a>）</p>
<p>URB_FUNCTION_SELECT_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SYNC_FRAME:设置和获取终结点的同步帧号。 请参阅 USB 规范中的9.4.10 部分。</td>
<td>此请求由 USB 驱动程序堆栈处理;客户端驱动程序无法执行此操作。</td>
<td>此请求由 USB 驱动程序堆栈处理;客户端驱动程序无法执行此操作。</td>
<td>此请求由 USB 驱动程序堆栈处理;客户端驱动程序无法执行此操作。</td>
</tr>
<tr class="even">
<td>对于设备类特定的请求和供应商命令。</td>
<td><ol>
<li>声明安装包。 请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>结构。</li>
<li>通过对供应商命令调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS</strong></a>特定的请求或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong></a>来初始化安装包。</li>
<li>指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>中定义的收件人值（设备、接口、终结点）。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>发送请求。</li>
</ol></td>
<td><ol>
<li>声明安装包。 请参阅 usb_hw 中声明的<strong>WINUSB_CONTROL_SETUP_PACKET</strong>结构。</li>
<li>调用<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_CLASS</strong>或<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong>（在 usb_hw 中定义）来初始化安装包。</li>
<li>指定方向（请参阅<strong>WINUSB_BMREQUEST_DIRECTION</strong>枚举）、接收方（请参阅<strong>WINUSB_BMREQUEST_RECIPIENT</strong>枚举）和请求，如类或硬件规范中所述。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice：： FormatRequestForControlTransfer</strong></a>方法，通过将初始化的安装包与框架请求对象和传输缓冲区关联来生成请求。</li>
<li>通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest：： send</strong></a>方法发送请求。</li>
<li>接收传输缓冲区中设备的信息。 通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a>方法访问该缓冲区。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_vendor_or_class_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_VENDOR_OR_CLASS_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_vendor_or_class_request)"><strong>_URB_CONTROL_VENDOR_OR_CLASS_REQUEST</strong></a></p>
<p>（<a href="https://docs.microsoft.com/previous-versions/ff538986(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildVendorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538986(v=vs.85))"><strong>UsbBuildVendorRequest</strong></a>）</p>
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



## <a name="how-to-send-a-control-transfer-for-vendor-commands---kmdf"></a>如何为供应商命令发送控件传输-KMDF


此过程说明客户端驱动程序如何发送控件传输。 在此示例中，客户端驱动程序发送供应商命令，该命令从设备检索固件版本。

1.  为供应商命令声明一个常数。 研究硬件规范并确定要使用的供应商命令。
2.  声明[**wdf @ no__t-2MEMORY @ no__t-3DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor)结构，并通过调用[**WDF @ no__t-6MEMORY @ no__t-7DESCRIPTOR @ no__t-8INIT @ no__t**](https://msdn.microsoft.com/library/windows/hardware/ff552392_init_buffer)宏来对其进行初始化。 此结构将在 USB 驱动程序完成请求后接收来自设备的响应。
3.  根据你是同步发送请求还是异步发送请求，请指定发送选项：
    -   如果通过调用[**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)同步发送请求，请指定超时值。 该值非常重要，因为如果没有超时，可以无限期地阻止该线程。

        为此，请声明一个[**wdf @ no__t-2REQUEST @ no__t-3SEND @ no__t-4OPTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_send_options)结构，然后调用[**wdf @ no__t-7REQUEST @ no__t-8SEND @ no__t-9OPTIONS @** ](https://msdn.microsoft.com/library/windows/hardware/ff552491_init) no__t 宏来对其进行初始化。 将选项指定为**WDF @ no__t-1REQUEST @ no__t-2SEND @ no__t-3OPTION @ no__t-4TIMEOUT**。

        接下来，通过调用[**WDF @ no__t-2REQUEST @ no__t-3SEND @ no__t-4OPTIONS @ no__t-5SET @ no__t**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdf_request_send_options_set_timeout) -6TIMEOUT 宏来设置超时值。

    -   如果要以异步方式发送请求，请实现完成例程。 在完成例程中释放所有已分配的资源。

4.  声明一个[**WDF @ no__t-2USB @ no__t-3CONTROL @ no__t-4SETUP @ no__t-5PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)结构，以包含安装令牌并设置结构格式。 为此，请调用[**WDF @ no__t-2USB @ no__t-3CONTROL @ no__t-4SETUP @ no__t-5PACKET @ no__t-6INIT @ no__t**](https://msdn.microsoft.com/library/windows/hardware/ff552568_init_vendor) -7VENDOR 宏来设置安装包的格式。 在调用指定中，请求的方向、接收方、发送请求选项（在步骤3中初始化）和供应商命令的常量。
5.  通过调用[**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)或[**WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)发送请求。
6.  检查框架返回的 NTSTATUS 值并检查接收到的值。

此代码示例向 USB 设备发送控制传输请求，以检索其固件版本。 将同步发送请求，客户端驱动程序会将相对超时值指定为5秒（以100毫微秒为单位）。 驱动程序将接收的响应存储在驱动程序定义的设备上下文中。

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

##<a name="how-to-send-a-control-transfer-for-get_status---umdf"></a>如何为 GET @ no__t 发送控件传输-1STATUS


此过程说明客户端驱动程序如何为 GET @ no__t-0STATUS 命令发送控件传输。 请求的接收方是设备，请求将获取 bits D1-D0 中的信息。 有关详细信息，请参阅 USB 规范中的图9-4。

1.  将标头文件 Usb @ no__t-0hw 与 OSR USB Fx2 学习工具包的 UMDF 示例驱动程序一起使用。
2.  声明**WINUSB @ no__t-1CONTROL @ no__t-2SETUP @ no__t-3PACKET**结构。
3.  通过调用 helper 宏**WINUSB @ no__t-1CONTROL @ no__t-2SETUP @ no__t-3PACKET @ no__t-4INIT @ no__t-5GET**@ no__t-6STATUS 初始化安装包。
4.  指定**BmRequestToDevice**作为接收方。
5.  在*索引*值中指定0。
6.  调用帮助器方法 SendControlTransferSynchronously 以同步发送请求。

    Helper 方法生成请求，方法是将初始化的安装包与框架请求对象和传输缓冲区关联，方法是调用[**IWDFUsbTargetDevice：： FormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)方法。 然后，帮助器方法通过调用[**IWDFIoRequest：： Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)方法发送请求。 方法返回后，检查返回的值。

7.  若要确定状态是否表示自驱动的远程唤醒，请使用在**WINUSB @ no__t-1DEVICE @ no__t-2TRAITS**枚举中定义的这些值：

此代码示例将控制传输请求发送到获取设备的状态。 该示例通过调用名为 SendControlTransferSynchronously 的帮助器方法来同步发送请求。

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

下面的代码示例演示了名为 SendControlTransferSynchronously 的 helper 方法的实现。 此方法同步发送请求。

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


如果使用 Winusb 作为设备的函数驱动程序，则可以从应用程序发送控制传输。 若要设置 WinUSB 中的安装包的格式，请使用此主题中的表中所述的 UMDF helper 宏和结构。 若要发送请求，请调用[**WinUsb @ no__t-2ControlTransfer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)函数。








