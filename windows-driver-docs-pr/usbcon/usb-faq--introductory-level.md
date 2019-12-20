---
Description: 本主题为驱动程序开发人员提供了一些常见问题，这些问题是开发并将 USB 设备和驱动程序与 Windows 操作系统集成的不熟悉的开发人员。
title: Windows 中的 USB - 常见问题解答
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 280052d878eeb9ffd367fc43039a7d22c9332d6e
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210621"
---
# <a name="usb-in-windows---faq"></a>Windows 中的 USB - 常见问题解答

本主题为驱动程序开发人员提供了一些常见问题，这些问题是开发并将 USB 设备和驱动程序与 Windows 操作系统集成的不熟悉的开发人员。

- [我收到了几乎以交换方式引发的许多 USB 术语。它们的意思是什么？](#i-hear-numerous-usb-terms-thrown-around-almost-interchangeably-what-do-they-all-mean)
- [我的 PC 是否有 USB 3.0 端口？](#does-my-pc-have-usb-30-ports)
- [是否需要安装可扩展主机控制器的驱动程序？](#do-i-need-to-install-drivers-for-my-extensible-host-controller)
- [为什么我在我的系统上看到了几个主机控制器？](#why-do-i-see-several-host-controllers-on-my-system)
- [为什么仅连接了一个 USB 3.0 集线器就会在设备管理器中看到两个中心？](#why-do-i-see-two-hubs-in-device-manager-when-i-have-connected-only-one-usb-30-hub)
- [为连接到2.0 端口的设备加载哪组驱动程序？](#which-set-of-drivers-is-loaded-for-the-devices-that-are-connected-to-20-ports)
- [如何实现确定我的 USB 3.0 设备是否作为 SuperSpeed 运行？](#how-do-i-determine-whether-my-usb-30-device-is-operating-as-superspeed)
- [为什么 SuperSpeed USB 设备不能比等效的高速 USB 设备更快？](#why-isnt-my-superspeed-usb-device-faster-than-an-equivalent-high-speed-usb-device)
- [是否可以在一个硬件中创建复合设备和复合设备？](#is-it-possible-to-have-a-composite-and-a-compound-device-in-one-piece-of-hardware)
- [为什么当我的一些 USB 设备移动到新端口时，它们会重新安装？](#why-are-some-of-my-usb-devices-reinstalled-when-they-are-moved-to-a-new-port)
- [是否有适用于 USB 产品打包的设计建议列表？](#is-there-a-list-of-design-recommendations-for-usb-product-packaging)
- [我是否必须重写我的客户端驱动程序以支持 USB 3.0 设备？](#do-i-have-to-rewrite-my-client-driver-to-support-usb-30-devices)
- [已为 SuperSpeed 存储设备使用、Uaspstor 或 Usbstor 加载哪个驱动程序？](#which-driver-is-loaded-for-my-superspeed-storage-device-use-uaspstorsys-or-usbstorsys)
- [Microsoft 支持哪些 USB DWG 类？](#which-usb-dwg-classes-does-microsoft-support)
- [自定义 USB 设备应该使用哪个设备安装程序类？](#which-device-setup-class-should-i-use-for-a-custom-usb-device)
- [为什么在附加某些 USB 设备时，CPU 不会进入 C3？](#why-wont-my-cpu-enter-c3-when-i-attach-some-usb-devices)
- [哪些 USB 类驱动程序支持选择性挂起？](#which-usb-class-drivers-support-selective-suspend)
- [为什么 USB 设备无法从 S3 唤醒 Windows？](#why-cant-a-usb-device-awaken-windows-from-s3)
- [是否需要安装增强型（USB 2.0）主机控制器的驱动程序？](#do-i-need-to-install-drivers-for-my-enhanced-usb-20-host-controller)
- [能否禁用 "将高速 USB 设备插入非高速 USB 端口" 通知？](#can-i-disable-the-hi-speed-usb-device-plugged-into-non-hi-speed-usb-port-notice)
- [我的 USB 2.0 集线器单 TT 还是多 TT？](#is-my-usb-20-hub-single-tt-or-multi-tt)
- [USB 序列号中哪些字符或字节有效？](#what-characters-or-bytes-are-valid-in-a-usb-serial-number)
- [对 Windows 的本地化版本发出字符串请求时使用了哪些 LANGID？](#what-langid-is-used-in-a-string-request-on-localized-builds-of-windows)
- [用于提取设备序列号的 LANGID 是什么？](#what-langid-is-used-to-extract-a-devices-serial-number)
- [不同 Windows 版本的最大 USB 传输大小是多少？](#what-is-the-maximum-usb-transfer-size-for-different-windows-versions)
- [如何将数字分配给复合设备上的多个接口？](#how-should-numbers-be-assigned-to-multiple-interfaces-on-a-composite-device)
- [Usbccgp 的主要限制是什么？](#what-are-the-major-restrictions-imposed-by-usbccgpsys)
- [如何实现为 USB core 二进制文件启用调试跟踪？](#how-do-i-enable-debug-tracing-for-usb-core-binaries)
- [Windows 是否支持接口关联描述符？](#does-windows-support-interface-association-descriptors)
- [USB stack 是否在 URB 中处理链接的 MDLs？](#does-the-usb-stack-handle-chained-mdls-in-a-urb)
- [某个驱动程序是否可以在 IRP 中具有多个 URB？](#can-a-driver-have-more-than-one-urb-in-an-irp)
- [Windows 是否支持 USB 复合中心？](#does-windows-support-usb-composite-hubs)

## <a name="i-hear-numerous-usb-terms-thrown-around-almost-interchangeably-what-do-they-all-mean"></a>我收到了几乎以交换方式引发的许多 USB 术语。 它们的意思是什么？

假设您看到了类似于*USB 3.0 的内容，我可以将 SUPERSPEED usb 拇指驱动器连接到 PC 的 xHCI 主机控制器并更快地复制文件。 "*

让我们了解该句子中的 USB 条款。 Usb 3.0、USB 2.0 和 USB 1.0 指[Usb 实现论坛](https://www.usb.org/)中的 usb 规范修订号。 USB 规范定义主机 PC 和 USB 设备彼此通信的方式。

版本号还指示最大传输速率。 最新的规格修订版为 USB 3.0，它指定最高可达 5 Gbps 的传输速度。 USB 1.0 定义了两个不同的数据速率、低速 USB （高达 1.5 Mbps）和全速 USB （最高可达 12 Mbps）。 USB 2.0 定义了一种新的数据速率、高速 USB （480 Mbps），同时保持对低速和全速设备的支持。 USB 3.0 将继续使用之前定义的所有数据速率。 如果你查看产品打包，SuperSpeed USB 将引用最新的 USB 3.0 设备。 高速 USB 用于描述高速 USB 2.0 设备。 USB，无描述符，是指低速和全速设备。

除了 USB 协议外，还存在另一个用于 USB 主机控制器的规范，即设备连接到的 PC 上的硬件块。 主机控制器接口规范定义主机控制器硬件和软件如何交互。 可扩展主机控制器接口（xHCI）定义 USB 3.0 主机控制器。 增强型主机控制器接口（EHCI）定义 USB 2.0 主机控制器。 通用主机控制器（UHCI）和开放式主机控制器（OHCI）是 USB 1.0 主机控制器的两个备用实现。

## <a name="does-my-pc-have-usb-30-ports"></a>我的 PC 是否有 USB 3.0 端口？

USB 3.0 端口标记有 SuperSpeed USB 徽标，或端口通常为蓝色。

![带有 usb 徽标的端口](images/usb-intro-faq-fig1-usblogo.png)

![蓝色 usb 3.0 端口](images/usb-intro-faq-fig2-blueusbport.png)

较新的 Pc 同时具有 USB 3.0 和 USB 2.0 端口。 如果希望 SuperSpeed USB 设备的速度最快，请找到 USB 3.0 端口并将设备连接到该端口。 连接了 USB 2.0 端口的 SuperSpeed 设备，运行速度快。

还可以验证特定端口是否为设备管理器中的 USB 3.0 端口。 在 Windows Vista 或更高版本的 Windows 中，打开 "设备管理器"，然后从列表中选择相应的端口。

![设备管理器中的 usb 主机控制器](images/usb-host-controllers-dm.png)

如果具有可扩展的主机控制器，则它支持 USB 3.0。

## <a name="do-i-need-to-install-drivers-for-my-extensible-host-controller"></a>是否需要安装可扩展主机控制器的驱动程序？

Windows 8 和 Windows Server 2012 包括对 USB 3.0 的支持。

如果 PC 具有 USB 3.0 端口，并且运行的 Windows 版本低于 Windows 8，则计算机制造商提供主机控制器驱动程序。 如果需要重新安装这些驱动程序，则必须从制造商处获取它们。

如果你在运行早于 Windows 8 的 Windows 版本的计算机上添加了 u 3.0 控制器卡，则必须安装由控制器卡制造商提供的驱动程序。

在 Windows 8 中，Microsoft 提供的 USB 3.0 驱动程序集（USB 驱动程序堆栈）可与大多数主机控制器一起使用。 Microsoft USB 3.0 驱动程序堆栈无法与 Fresco 逻辑 FL1000 控制器一起使用。 若要确定是否有 FL1000 控制器，请打开设备管理器并展开 "**通用串行总线控制器**"。 右键单击控制器节点，查看控制器属性。 在 "**详细信息**" 选项卡上，选择列表中的 "**硬件 id** " 属性。 如果硬件 ID 以 PCI\\即使\_1B73 & 开发\_1000，则为 FL1000。 对于该控制器，请从您的 PC 或控制器卡制造商处下载并安装驱动程序。

## <a name="why-do-i-see-several-host-controllers-on-my-system"></a>为什么我在我的系统上看到了几个主机控制器？

除了连接到您的 PC 的 USB 设备之外，还可以通过 USB 连接多台设备（例如网络摄像机、指纹读取器、SD 卡读卡器）。 若要连接所有这些设备并仍提供外部 USB 端口，电脑支持多个 USB 主机控制器。

USB 3.0 xHCI 主机控制器完全向后兼容所有 USB 设备速度、SuperSpeed、高速、全速和低速。 可以直接将任何设备连接到 xHCI 控制器，并期望该设备正常运行。 对于 EHCI 控制器，不是这样。 尽管 USB 2.0 规范支持设备的所有速度，但 EHCI 控制器仅支持高速 USB 设备。 为了使全速和低速 USB 设备正常运行，必须通过 USB 2.0 集线器连接到 EHCI 控制器，或者必须将其连接到 UHCI 或 OHCI 控制器。

对于更高版本的电脑，电脑公开的大多数 USB 2.0 端口都是 USB 2.0 集线器的下游。 此集线器连接到 EHCI 控制器。 这允许 PC 的 USB 2.0 端口与设备的所有速度一起工作。 连接到2.0 端口时，SuperSpeed 设备的行为与高速设备相同。

在发布 USB 2.0 规范后，电脑将组合使用主机控制器以支持设备的所有速度。 单个 USB 2.0 端口将连接到两个主机控制器： EHCI 主机控制器和 UHCI 或 OHCI 主机控制器。 附加设备时，硬件会将连接动态路由到两个主机之一。 例程取决于设备的速度。

## <a name="why-do-i-see-two-hubs-in-device-manager-when-i-have-connected-only-one-usb-30-hub"></a>为什么仅连接了一个 USB 3.0 集线器就会在设备管理器中看到两个中心？

尽管 xHCI 主机控制器适用于设备的任何速度，但 SuperSpeed 集线器仅适用于 SuperSpeed 设备。 为了确保 USB 3.0 中心可以使用所有速度，它们有两部分： SuperSpeed 集线器和 USB 2.0 集线器。 USB 3.0 集线器能够通过将设备动态路由到 SuperSpeed 集线器或2.0 中心（基于设备速度）来支持所有速度。

打开设备管理器，**按连接查看设备**，然后找到可扩展的主机控制器。 将单个 USB 3.0 集线器连接到 USB 3.0 端口时，控制器的根集线器有两个下游集线器。

![设备管理器中的 usb 3.0 集线器](images/usb-3-hub-dm.png)

在下面的示例中，SuperSpeed USB 存储设备和 USB 音频设备均连接到 USB 3.0 集线器。 你可以看到，存储设备是 SuperSpeed 集线器的下游，而音频设备是 USB 2.0 集线器的下游。

![设备管理器中的带连接设备的 usb 3.0 集线器](images/usb-3-hub-connected-devices-dm.png)

## <a name="which-set-of-drivers-is-loaded-for-the-devices-that-are-connected-to-20-ports"></a>为连接到2.0 端口的设备加载哪组驱动程序？

为每种类型的主机控制器加载一组不同的二进制文件。 必须了解，Windows 加载的 USB 驱动程序堆栈与主机控制器的类型相关，而不是与连接的设备的速度关联。

在此图中，可以看到为每种不同类型的 USB 主机控制器加载了哪些驱动程序。

![windows 8 中的 usb 驱动程序堆栈](images/usb-win8-driver-stacks.png)

如果 USB 3.0 端口正确路由到 xHCI 控制器，Windows 将加载 xHCI 驱动程序堆栈（也称为 USB 3.0 驱动程序堆栈）。

如果 USB 2.0 端口通过 USB 2.0 集线器连接到 EHCI 控制器，则流量将通过 EHCI 控制器进行，并加载 USB 2.0 驱动程序堆栈。

有关 USB 驱动程序堆栈中的驱动程序的详细信息，请参阅[Windows 中的 USB 主机端驱动程序](https://go.microsoft.com/fwlink/p/?linkid=320134)。

如果 PC 的 USB 2.0 端口使用配套控制器，则端口路由到的主机控制器取决于设备速度。 例如，低速设备通过 UHCI 或 OHCI 控制器进行连接，并使用 USBUHCI 或 USBOHCI 驱动程序。 计算机将高速设备路由到 EHCI 控制器，因此，Windows 使用 USBEHCI 驱动程序。

不同的设备速度并不确定为控制器加载的驱动程序。 但是，不同的设备速度可能会确定使用的控制器。 控制器始终使用同一个驱动程序。

## <a name="how-do-i-determine-whether-my-usb-30-device-is-operating-as-superspeed"></a>如何实现确定我的 USB 3.0 设备是否作为 SuperSpeed 运行？

首先，在 Windows 8 中，请确保具有 USB 3.0 端口和 xHCI 主机控制器。 如果 SuperSpeed USB 设备连接到 xHCI 主机控制器，Windows 8 将在 Windows 8 UI 的特定部分中显示 "已连接到 USB 3.0" 消息。 如果设备连接到 EHCI 控制器而不是 XHCI 控制器，消息将被读取 "设备在连接到 USB 3.0 时可以更快地执行"。

你可以在 "电脑设置" 中查看这些 UI 消息。

1. 打开 "超级按钮" 栏（将光标拖到屏幕的右上角或右下角，键入 "Windows 键 + C"，或用手指从右轻扫）。
2. 选择 "**设置**"，然后**更改 "电脑设置**"。
3. 选择 "**电脑设置**" 下的**设备**。

此图像显示 USB 3.0 设备在 SuperSpeed 上运行时的 UI 消息。

![superspeed usb 设备在 superspeed 上运行 ](images/usb-superspeed.jpg)

此图像显示 USB 设备在低于 SuperSpeed 的总线速度下运行时的 UI 消息。

![superspeed usb 设备高速操作 ](images/usb-high-speed.jpg)

你可以在设备和打印机中查看类似消息，如以下图像中所示。

![superspeed usb 设备在 superspeed 上运行](images/usb-superspeed-devices.jpg)

![superspeed 设备以高速运行](images/usb-high-speed-devices.jpg)

如果 USB 3.0 设备是存储设备，Windows 资源管理器会在选择卷标签时显示类似消息，如下所示。 请注意，必须选择 "**视图"-"&gt; 详细信息**" 窗格，才能显示该消息。

![superspeed usb 设备在 superspeed 上运行 ](images/usb-superspeed-storage-device.jpg)

![superspeed usb 设备高速操作](images/usb-high-speed-storage-device.jpg)

如果你正在编写设备驱动程序，则 Windows 驱动程序工具包（WDK）中包含的[USBView](https://go.microsoft.com/fwlink/p/?linkid=320135)工具非常有用。 对于 Windows 8 WDK，Microsoft 更新了 USBView 以显示 SuperSpeed USB 信息。 你可以使用此工具来确定你的设备是否在 SuperSpeed 上运行。 此图显示了在 USBView 的 SuperSpeed 中运行的 USB 3.0 设备。

![superspeed usb 设备在 superspeed 上运行](images/usb-superspeed-usbview.jpg)

如果你是设备驱动程序开发人员，则[usb 驱动程序堆栈](https://go.microsoft.com/fwlink/p/?linkid=320134)会公开称为 IOCTL\_的新 IOCTL， [\_获取\_节点\_连接\_\_EX\_V2](https://go.microsoft.com/fwlink/p/?linkid=320136)，可用于查询 USB 3.0 设备的速度信息。

## <a name="why-isnt-my-superspeed-usb-device-faster-than-an-equivalent-high-speed-usb-device"></a>为什么 SuperSpeed USB 设备不能比等效的高速 USB 设备更快？

通常，如果 USB 3.0 USB 设备的速度不如高速 USB 设备的速度快，则它不会在 SuperSpeed 中执行。 如果 SuperSpeed USB 设备连接到 USB 3.0 端口，则它可能无法在 SuperSpeed 上操作，原因如下：

- 你使用的是 USB 2.0 集线器。

    如果你使用的是集线器，请确认它是 USB 3.0 集线器。 如果使用的是 USB 2.0 集线器，则任何附加的 SuperSpeed USB 设备都将以高速速度运行。 请将集线器替换为 USB 3.0 集线器，或将设备直接连接到 USB 3.0 端口。

- USB 3.0 集线器上的固件已过时。

    某些较早的 USB 3.0 集线器运行不正常。 因此，Windows 只使用这些中心的2.0 部分。 如果设备管理器指示 "不起作用" 的中心（如此图所示），则 Windows 8 不使用中心的3.0 部分。

    ![不能正常运行的 superspeed usb 集线器](images/usb-superspeed-nonfunctional.jpg)

    可以将 SuperSpeed 设备直接连接到 USB 3.0 端口，或在中心更新固件。 Windows 8 识别了具有较新固件的集线器。

- 设备使用 USB 2.0 电缆进行连接。

    确保用于连接设备的电缆是 USB 3.0 电缆。 USB 3.0 电缆也可能存在信号完整性问题。 在这种情况下，设备可能会切换到高速。 如果出现这种情况，则必须使用不同的 USB 3.0 电缆。

- 设备上的固件已过时。

    通过从制造商的网站获取最新版本来更新 SuperSpeed USB 设备的固件。 某些 SuperSpeed USB 设备制造商版本修复了设备中发现的 bug，如固件更新。

- 主控制器上的固件已过期。

    通过从你的电脑制造商站点或添加的卡制造商站点获取最新版本，更新 USB 3.0 控制器的固件。 某些 USB 3.0 控制器制造商版本修复了在控制器中找到的 bug，如固件更新。

- 系统的 BIOS 已过期。

    通过从电脑 maker 获取最新版本来更新系统的 BIOS。 在某些主板上，BIOS 会将连接到 xHCI 主机控制器的设备错误地路由到 EHCI 控制器。 这种不正确的路由强制 SuperSpeed USB 设备以高速操作。 BIOS 更新可以解决此问题。

## <a name="is-it-possible-to-have-a-composite-and-a-compound-device-in-one-piece-of-hardware"></a>是否可以在一个硬件中创建复合设备和复合设备？

是 具有三端口总线供电集线器的 Microsoft 自然键盘专业人员是复合复合 USB 设备的一个示例。 设备已将复合设备连接到端口1。 另外两个端口向最终用户公开。

附加到端口1的设备是低速复合设备。 设备有两个接口，两者都符合设备接口设备（HID）的 USB 标准设备类定义。 复合设备提供两个 HID 接口，而不是通过使用顶级集合在单个 HID 接口上对所有集合进行多路复用。 选择此设计是为了与较旧的 BIOSs 兼容。

## <a name="why-are-some-of-my-usb-devices-reinstalled-when-they-are-moved-to-a-new-port"></a>为什么当我的一些 USB 设备移动到新端口时，它们会重新安装？

在 Windows 2000 和更高版本的操作系统中，当 USB 设备从一个端口移到另一个端口时，将创建一个新的物理设备对象（PDO）。 如果硬件报告了唯一的 USB 序列号，则不会创建新的 PDO。

若要重复使用同一 PDO 并确保设备体验不会改变，无论设备是否已重新插入相同的端口或新端口，硬件供应商必须在其设备上存储一个序列号。 根据 Windows 硬件认证计划的要求，每个共享设备安装标识符的设备的序列号必须是唯一的。

## <a name="is-there-a-list-of-design-recommendations-for-usb-product-packaging"></a>是否有适用于 USB 产品打包的设计建议列表？

USB-如果与其他 USB 成员公司合作，为独立硬件供应商开发建议，以将其打包。

USB 网站上提供了详细信息。

对于 USB 高速和 SuperSpeed，请参阅： [https://www.usb.org/](https://www.usb.org/)。

## <a name="do-i-have-to-rewrite-my-client-driver-to-support-usb-30-devices"></a>我是否必须重写我的客户端驱动程序以支持 USB 3.0 设备？

所有现有的客户端驱动程序都应继续工作，就像在连接到 USB 3.0 端口时，使用低、全速或高速设备时。 在 Windows 8 中，我们确保了与现有客户端驱动程序的兼容性。

USB 3.0 驱动程序堆栈维持 IRQL 级别、调用方上下文和错误状态;与设备交互时重试频率和时间，以及确保现有驱动程序可以继续正常运行。 测试仍非常重要。

发生常见故障的原因是：

- 由于存在 SuperSpeed 终结点伴随描述符，驱动程序的终结点描述符分析中断。
- 由于速度提高，你可能会遇到应用程序协议级别的计时问题。
- 终结点支持的最大数据包大小可能不同。
- 由于功能电源管理，选择性挂起操作的计时可能不同。

在 Windows 7 和更早版本的操作系统中，USB 3.0 驱动程序堆栈由第三方提供。 因此，强烈建议您测试驱动程序以使用第三方 USB 驱动程序堆栈。

Windows 8 中的新客户端驱动程序，适用于高速和 SuperSpeed USB 设备，应选择新的功能。

## <a name="which-driver-is-loaded-for-my-superspeed-storage-device-use-uaspstorsys-or-usbstorsys"></a>已为 SuperSpeed 存储设备使用、Uaspstor 或 Usbstor 加载哪个驱动程序？

USB 连接 SCSI （UAS）协议是一种新的大容量存储协议，旨在通过已建立的 USB 大容量存储协议、仅批量传输（机器人）来改善性能。 它通过减少协议开销来实现此目的，它支持 SATA 本机命令队列（NCQ），并通过并行处理多个命令。 为此，需要使用新的 USB 3.0 功能进行大容量传输（称为流）。

现有大容量存储驱动程序 Usbstor 使用机器人协议。 它适用于设备的所有速度，包括 SuperSpeed USB 设备。

对于 Windows 8，Microsoft 包括了一个新的大容量存储类驱动程序，Uaspstor 使用了 UAS 协议。 由于流是 USB 3.0 的新手，因此 Uaspstor 只能在硬件支持流（SuperSpeed USB 设备连接到 xHCI 主机控制器）时使用流。 该驱动程序还包括对软件流的支持，因此，它还可以针对高速运行的设备加载，而不考虑主机类型。

如果将大容量存储设备连接到 Windows 8，并且该设备支持 UAS，则 Windows 将加载 Uaspstor。 在某些情况下，特定 xHCI 主机控制器上可能存在硬件流的已知问题，或设备的 UAS 协议实现的已知问题。 在这些情况下，Windows 将回退到机器人协议并改为加载 Usbstor 驱动程序。

Uaspstor 是 Windows 8 的新手。 它在早期版本的 Windows 中不存在。

## <a name="which-usb-dwg-classes-does-microsoft-support"></a>Microsoft 支持哪些 USB DWG 类？

Windows 支持 USB 设备工作组（DWG）定义的多个 USB 类。 有关 USB 类规范和类代码的当前列表，请访问[https://www.usb.org/documents]( https://go.microsoft.com/fwlink/p/?LinkId=623332)上的 usb DWG 网站。

此表突出显示了 Windows 中受支持的 USB DWG 类，还标识了支持每个类的 Windows 版本。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>类规范</th>
<th>bDeviceClass 代码</th>
<th>驱动程序名称</th>
<th>Windows 支持</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>蓝牙类</td>
<td>0xE0</td>
<td>Bthusb</td>
<td>Windows XP 及更高版本</td>
</tr>
<tr class="even">
<td>芯片/智能卡接口设备（CCID）</td>
<td>0x0B</td>
<td>Usbccid</td>
<td><p>Windows Server 2008 及更高版本</p>
<p>Windows Vista 及更高版本</p>
<p>Windows Server 2003<em></p>
<p>Windows XP</em></p>
<p>Windows 2000<em></p></td>
</tr>
<tr class="odd">
<td>Hub 类</td>
<td>0x09</td>
<td>Usbhub</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="even">
<td>人体学接口设备 (HID)</td>
<td>0x03</td>
<td>Hidusb</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="odd">
<td>大容量存储类（MSC）</td>
<td>0x08</td>
<td>Usbstor</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="even">
<td>USB 连接 SCSI （UAS）</td>
<td>0x08</td>
<td>Uaspstor</td>
<td><p>Windows Server 2012</p>
<p>Windows 8</p></td>
</tr>
<tr class="odd">
<td>打印类</td>
<td>0x07</td>
<td>Usbprint</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="even">
<td>扫描/映像（PTP）</td>
<td>0x06</td>
<td><p>WpdUsb</p>
<p>Usbscan</p></td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="odd">
<td>媒体传输（MTP）</td>
<td>0x06</td>
<td>WpdUsb</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p></td>
</tr>
<tr class="even">
<td>USB 音频类</td>
<td>0x01</td>
<td>Usbaudio</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="odd">
<td>调制解调器类（CDC）</td>
<td>0x02</td>
<td>Usbser</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="even">
<td>视频类（UVC）</td>
<td>0x0E</td>
<td>Usbvideo</td>
<td><p>Windows Vista 及更高版本</p>
<p>Windows XP</em></p></td>
</tr>
</tbody>
</table>

为了加载此驱动程序，需要 \*特殊说明，因为此驱动程序可能已发布到操作系统之后。 Windows 类驱动程序可能不支持 DWG 类规范中所述的所有功能。 在这种情况下，驱动程序不会基于类匹配加载。 有关类规范内实现的功能的更多详细信息，请参阅 WDK 文档。

## <a name="which-device-setup-class-should-i-use-for-a-custom-usb-device"></a>自定义 USB 设备应该使用哪个设备安装程序类？

Microsoft 为大多数设备类型提供系统定义的安装程序类。 系统定义的安装程序类 Guid 是在 Devguid 中定义的。 有关其他信息，请参阅 WDK。 有关 Windows 类 Guid 的列表，请参阅以下主题：

- [向供应商提供的系统定义的设备安装程序类](https://go.microsoft.com/fwlink/p/?linkid=320141)
- [系统定义的设备安装程序类保留供系统使用](https://go.microsoft.com/fwlink/p/?linkid=320142)

独立硬件供应商必须使用与 USB 设备类型（而不是总线类型）关联的安装程序类。 如果要开发的设备类型的 Microsoft 尚未提供现有的类 GUID，则可以定义新的设备安装程序类。

在 Windows 8 中，已定义了一个名为**USBDevice** （ClassGuid = {88BAE032-5A81-49f0-BC3D-A4FF138216D6}）的新安装程序类。 如果要开发设备类型，请将设备与**USBDevice**而不是安装程序类（ **USB**）相关联。 **USBDevice**类适用于 Windows Vista 和更高版本的操作系统。

安装程序类**usb** （ClassGuid = {36fc9e60; c465-8056-444553540000}）仅为 usb 主机控制器和 usb 集线器保留，而不能用于其他设备类别。 如果使用此安装程序类不当，可能会导致设备驱动程序无法运行 Windows 徽标测试。

## <a name="why-wont-my-cpu-enter-c3-when-i-attach-some-usb-devices"></a>为什么在附加某些 USB 设备时，CPU 不会进入 C3？

连接 USB 设备时，USB 主机控制器会轮询帧计划程序，这是一个直接内存访问（DMA）总线主机操作。 "中断事件" （如总线主机流量、中断或其他几个系统活动）将 CPU 移出 C3，因为根据定义，当 CPU 处于 C3 中时，它无法 snooped。

可以通过两种方法解决此问题：

- 硬件删除。

    有时，硬件可以通过电子方式与通用串行总线断开连接。 例如，如果从 USB 读取器中删除存储媒体，则 USB 读取器可以模拟电子断开连接，并在重新插入媒体时重新连接。 在这种情况下，可能会发生 C3 转换，因为主机控制器上没有 USB 设备。

- 选择性挂起。

    Windows XP 和更高版本的操作系统中唯一可用的替代方法是支持 USB 选择性挂起。 此功能使驱动程序可以在设备进入空闲状态时暂停其控制的 USB 设备，即使系统本身仍处于完全操作电源状态（S0）。 如果所有 USB 函数驱动程序都支持选择性挂起，则此功能特别强大。 即使一个驱动程序不支持该驱动程序，CPU 也不能进入 C3。 有关选择性挂起的其他信息，请参阅 WDK。

## <a name="which-usb-class-drivers-support-selective-suspend"></a>哪些 USB 类驱动程序支持选择性挂起？

下面列出了支持选择性挂起的 Windows 8 中的 USB 类驱动程序：

- “蓝牙”

    此驱动程序可以有选择地在运行 Windows XP Service Pack 2 和更高版本的 Windows 的计算机上挂起设备。 驱动程序要求蓝牙收音机设置配置描述符中的自驱动和远程唤醒位。 当不存在活动的蓝牙连接时，驱动程序会有选择地挂起（D2）蓝牙收音机。

- USB HID

    此驱动程序可以有选择地挂起 HID 设备。 你需要在所有设备状态发生更改时触发远程唤醒信号。 若要在 HID 堆栈中启用选择性挂起，必须为设备的特定 VID + PID 启用 SelectiveSuspendEnabled 注册表值。 有关示例，请参阅输入 .inf。

    在支持 Windows 8 连接备用的系统上，当系统处于连接待机状态时，该驱动程序将进入选择性挂起（D2）。 此驱动程序可以唤醒系统并打开屏幕。

- USB 集线器

    此驱动程序可以在没有设备连接到根或外部集线器时有选择地挂起，也可以有选择地挂起附加到该集线器的所有设备。

- USB 调制解调器

    如果不存在活动的调制解调器连接，此驱动程序可以有选择地挂起设备。

- USB 存储（机器人）

    当这些系统进入连接待机状态时，此驱动程序可以在支持 Windows 8 连接备用的系统上有选择地挂起（D3）存储设备。 与 HID 一样，在所有 Windows 8 系统上都有一个用于启用选择性挂起的注册表替代。

- USB 存储（UAS）

    当存储设备处于空闲状态时，此驱动程序可以有选择地将其挂起（D3）。

- USB 视频

    此驱动程序可以在 Windows Vista 和更高版本的操作系统上有选择地挂起网络摄像机。

- USB 音频

    当计算机使用电池电源时，此驱动程序可以在 Windows 7 及更高版本的操作系统上有选择地挂起 USB 音频设备。

- 复合 USB

    当所有子级处于挂起状态时，此驱动程序可以有选择地挂起（D3）复合设备。 在支持 D3-冷的系统上，所有子女都必须选择 "D3-冷"。

- USB 智能卡

    默认情况下，此驱动程序可以在 Windows 7 和更高版本的操作系统中选择性地挂起（D2）智能卡接口设备。

- 通用 USB 外围设备（WinUSB）

    默认情况下，此驱动程序可以在 Windows Vista 和更高版本的操作系统上选择性地挂起（D3）设备。

- WWAN：3G 或 WiMax 连接器

    此驱动程序可以有选择地挂起设备。 如果有活动的订阅，则设备进入 D2，没有活动的订阅，设备进入 D3。

## <a name="why-cant-a-usb-device-awaken-windows-from-s3"></a>为什么 USB 设备无法从 S3 唤醒 Windows？

USB 设备无法唤醒 Windows from S3 的原因有多种，其中包括：

1. BIOS 不正确。

    验证计算机上是否安装了最新的 BIOS。 若要获取计算机的最新 BIOS 修订版本，请访问 OEM 或 ODM 的网站。

2. 没有启用唤醒功能的 BIOS。

    某些 BIOSs 使你可以禁用从 S3 和 S4 唤醒。 验证是否已启用 BIOS 从 S3 唤醒。

3. 未设置 USBBIOSx 注册表项。

    Windows XP 的全新安装不具有 USBBIOSx 注册表项。 如果 OEM 或 ODM 验证 BIOS 能否从 S3 唤醒，请将此注册表项设置为0x00，然后重新启动计算机。

4. 主机控制器没有 S3 或 S4 的电源。

    很多情况下，当 PC 处于低功耗状态时，PC 会对外接卡供电。 如果外接程序卡不能通电，它将无法检测唤醒事件，并且将无法唤醒 PC。

有关其他信息，请参阅 Windows XP 和更高版本的 Windows 中的 "帮助和支持中心" 中的 "USB 疑难解答"。

## <a name="do-i-need-to-install-drivers-for-my-enhanced-usb-20-host-controller"></a>是否需要安装增强型（USB 2.0）主机控制器的驱动程序？

以下版本的 Windows 支持 USB 2.0 增强型主机控制器：

- Windows Vista 及更高版本
- Windows Server 2003 及更高版本
- Windows XP Service Pack 1
- Windows 2000 Service Pack 4

**请注意**   由于在 USB 2.0 硬件可用之前已发布 windows 2000 和 windows XP，因此这些操作系统的驱动程序已在 service pack 中发布。 若要安装驱动程序：

1. 按照第一个问题的答案中所述的过程来验证你的计算机是否安装了 USB 2.0 端口，并且是否需要为增强型主机控制器安装驱动程序。
2. 在 "设备管理器" 窗口中，展开第一个问题中所述的 "**其他设备**" 部分，然后双击 "**通用串行总线（USB）控制器**"。
3. 在 "属性" 对话框的 "**常规**" 选项卡上，单击 "**重新安装驱动程序**"。

    ![重新安装驱动程序](images/usb-reinstall-driver.jpg)

4. 在 "添加新硬件" 向导中，选择 "**自动安装软件（推荐）**"，然后单击 "**下一步**"。 继续执行向导，接受所有默认选项，直到到达向导的最后一页，然后单击 "**完成**"。 可能需要重新启动计算机才能完成安装。

**请注意**   要确保计算机上安装了最新更新，请定期访问 Windows 更新。

## <a name="can-i-disable-the-hi-speed-usb-device-plugged-into-non-hi-speed-usb-port-notice"></a>能否禁用 "将高速 USB 设备插入非高速 USB 端口" 通知？

Windows XP 和更高版本的 Windows 在高速 USB 设备插入不支持高速的 USB 端口时创建一个弹出通知。 若要从设备获得最快的性能，用户必须单击该通知并按照屏幕上的说明进行操作。

若要禁用该通知，请执行以下步骤：

1. 开始设备管理器，如此常见问题中的第一个问题中所述。
2. 在 "设备管理器" 窗口中，展开 "**通用串行总线控制器**" 节点。 在标题中查找 "通用" 或 "打开" 一词的主机控制器。 如果找到一个，请双击它。
3. 在 "**属性**" 对话框的 "**高级**" 选项卡上，选择 "**请勿告诉我有关 USB 错误**"。

**请注意**   前面的过程会禁用所有 USB 通知，而不只是 "连接到无高速端口的高速 USB 设备"。

## <a name="is-my-usb-20-hub-single-tt-or-multi-tt"></a>我的 USB 2.0 集线器单 TT 还是多 TT？

对于中心（单 TT）上所有面向下游的端口，USB 2.0 集线器可以有一个事务转换器（TT），也可以为集线器上的每个面向下游的端口使用一个 TT （多 TT）。

Usb 设备描述符的**bDeviceProtocol**字段值和 usb 接口描述符的**bInterfaceProtocol**字段值指示集线器是单 tt 还是多 tt：

- 单 TT。 **bDeviceProtocol** = = 0x01
- 多 TT。 **bDeviceProtocol** = = 0x02

**Usbhub**使用此设置来启用多 TT 模式或单 TT 模式。 在 Windows XP 和更高版本上，Usbhub 在多 TT 中心始终启用多 TT 模式。 有关 TT 布局的其他详细信息，请参阅[USB 2.0 规范](https://www.usb.org/documents)的11.14.1.3 和11.23.1 部分。

## <a name="what-characters-or-bytes-are-valid-in-a-usb-serial-number"></a>USB 序列号中哪些字符或字节有效？

USB 设备描述符的**iSerialNumber**字段指示设备是否具有序列号和存储数字，如下所示：

- **iSerialNumber** = = 0X00： USB 设备没有序列号。
- **iSerialNumber** ！ = 0X00： USB 设备具有序列号。 分配给**iSerialNumber**的值是序列号的字符串索引。

如果设备具有序列号，则序列号必须唯一标识同一设备的每个实例。

例如，如果两个设备描述符的 "i**dVendor**"、" **idProduct**" 和 " **bcdDevice** " 字段的值相同，则**iSerialNumber**字段必须不同，以便将一台设备与另一台设备区分开来。

即插即用要求 USB 序列号中的每个字节都有效。 如果单个字节无效，Windows 会丢弃序列号，并将设备视为不具有序列号。 对于 USB 序列号，以下字节值无效：

- 0x2C.
- 小于0x20 的值。
- 大于0x7F 的值。

有关**iSerialNumber**值的其他详细信息，请参阅[USB 2.0 规范](https://www.usb.org/documents)的9.6.1 部分。

## <a name="what-langid-is-used-in-a-string-request-on-localized-builds-of-windows"></a>对 Windows 的本地化版本发出字符串请求时使用了哪些 LANGID？

USB 设备通过将 USB 设备描述符的 iSerialNumber 字段设置为序列号的字符串索引，指示是否存在序列号。 若要检索序列号，Windows 将发出一个字符串请求，并将语言标识符（LANGID）设置为0x0409 （美国英语）。 即使针对其他语言进行了本地化的 Windows 版本，Windows 始终使用此 LANGID 来检索 USB 序列号。

## <a name="what-langid-is-used-to-extract-a-devices-serial-number"></a>用于提取设备序列号的 LANGID 是什么？

USB 设备通过将 USB 设备描述符的 iSerialNumber 字段设置为序列号的字符串索引，指示是否存在序列号。 若要检索序列号，Windows 将发出一个字符串请求，并将语言标识符（LANGID）设置为0x0409 （美国英语）。 即使针对其他语言进行了本地化的 Windows 版本，Windows 始终使用此 LANGID 来检索 USB 序列号。

## <a name="what-is-the-maximum-usb-transfer-size-for-different-windows-versions"></a>不同 Windows 版本的最大 USB 传输大小是多少？

请参阅[各种操作系统上的最大 USB 传输大小](https://support.microsoft.com/help/832430/maximum-size-of-usb-transfers-on-various-operating-systems)。

## <a name="how-should-numbers-be-assigned-to-multiple-interfaces-on-a-composite-device"></a>如何将数字分配给复合设备上的多个接口？

Windows 将第一个配置上具有多个接口的 USB 设备视为复合设备。

对于 Windows XP Service Pack 1 和更早版本的 Windows：

- 接口编号必须从零开始。
- 接口编号必须是连续的并且递增。

对于 Windows XP Service Pack 2 和更高版本的 Windows，只需要增加接口号，而不是连续的。

有关接口号码的其他信息，请参阅[WINDOWS XP 中的接口未按顺序排列的复合 USB 设备不起作用](https://support.microsoft.com/help/814560)。

对于所有版本的 Windows，应按以下方式为接口分配备用设置：

- 接口的默认值始终为替代设置零。
- 其他备用设置号必须是连续且增加的。

有关替代设置的其他信息，请参阅 9.6.5 of the [USB 2.0 规范](https://www.usb.org/documents)。

## <a name="what-are-the-major-restrictions-imposed-by-usbccgpsys"></a>Usbccgp 的主要限制是什么？

**Usbccgp**支持复合设备：

- Windows Me
- Windows XP
- Windows Server 2003
- Windows Vista
- Windows Server 2008

尽管仍可以在这些和更高版本的 Windows 上将**Usbhub**作为复合设备的父驱动程序加载，但 Microsoft 不建议这样做，因为这可能会导致硬件兼容性错误。 应改为使用**Usbccgp** 。

若要确保为复合设备加载正确的驱动程序，请在 INF 文件中使用 Include 和需要指令，如下所示：

``` syntax
Include = USB.INF
Needs = Composite.Dev
```

**Usbccgp**对硬件设备和驱动程序施加的主要限制如下：

- Usbccgp 仅支持默认配置，配置0。
- Usbccgp 不支持在 Windows XP 和 Windows Server 2003 中选择挂起。 只有 Windows Vista 和更高版本的 Windows 支持此功能。
    **请注意**   Usbccgp 支持 WINDOWS xp SP1 和更高版本的 windows xp 中的选择性挂起，但功能有限。 对于这些版本的 Windows，仅当设备的每个子功能都有挂起的空闲 IRP 时，复合设备才会置于选择性挂起状态。 Usbccgp 在 Windows XP RTM 中不支持选择性挂起

- Usbccgp 仅支持 Windows XP SP2、Windows Server 2003 SP1 和更高版本的 Windows 中的接口关联描述符（IAD）。
- Usbccgp 仅支持 Windows XP SP2、Windows Server 2003 SP1 以及更高版本的 Windows 中不连续的接口号。

## <a name="how-do-i-enable-debug-tracing-for-usb-core-binaries"></a>如何实现为 USB core 二进制文件启用调试跟踪？

请参阅博客文章[，了解如何在驱动程序的公共 PDB 文件中包含和查看 WPP 跟踪消息](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/06/29/wpp-blog-post.aspx)。

有关 USB 核心堆栈调试的其他信息，请参阅[如何在各种驱动程序和子系统中启用详细的调试跟踪](https://support.microsoft.com/help/314743)。

## <a name="does-windows-support-interface-association-descriptors"></a>Windows 是否支持接口关联描述符？

是 USB 2.0 接口关联描述符（IAD）工程更改通知（ECN）引入了新的标准方法，用于描述函数中的一组接口及其备用设置。 IAD 可用于标识一个函数中的两个或多个连续接口和备用设置。

Microsoft 目前正在使用 Ihv 来开发支持 IAD 的设备。 以下操作系统支持 IAD：

- Windows XP Service Pack 2 及更高版本
- Windows Server 2003 Service Pack 1 及更高版本
- Windows Vista

## <a name="does-the-usb-stack-handle-chained-mdls-in-a-urb"></a>USB stack 是否在 URB 中处理链接的 MDLs？

Windows 附带的 USB 3.0 驱动程序堆栈支持此功能。

## <a name="can-a-driver-have-more-than-one-urb-in-an-irp"></a>某个驱动程序是否可以在 IRP 中具有多个 URB？

不相同。 Windows 附带的 USB stack 不支持此功能。

## <a name="does-windows-support-usb-composite-hubs"></a>Windows 是否支持 USB 复合中心？

复合 USB 设备（也称为多功能 USB 设备）公开多种功能，其中每个功能都可以被视为独立的设备。 系统加载 USB 通用父驱动程序**Usbccgp**，作为设备功能的 eaech 的父驱动程序。 USB 通用父驱动程序会枚举复合设备的功能，就像它们是单独的 USB 设备，然后创建一个 PDO 并为每个功能构造一个设备堆栈。

复合 USB 设备不能公开充当集线器的函数。 Windows 不能正确枚举此类集线器，尝试安装设备可能会导致系统崩溃。

## <a name="related-topics"></a>相关主题

[适用于所有开发人员的 USB 概念](usb-concepts-for-all-developers.md)  
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
