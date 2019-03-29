---
Description: This topic presents frequently asked questions for driver developers who are new to developing and integrating USB devices and drivers with Windows operating systems.
title: Windows 中的 USB - 常见问题解答
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90e5ffd611ce4f41f4c575defff6bd3fc5531d53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576051"
---
# <a name="usb-in-windows---faq"></a>Windows 中的 USB - 常见问题解答


本主题介绍了一些常见问题的驱动程序开发人员还不熟悉开发以及将 USB 设备和驱动程序与 Windows 操作系统集成。

-   [我听到几乎可交换引发周围的大量 USB 条款。它们都代表什么？](#usbterms)
-   [我的 PC 是否有 USB 3.0 端口？](#pc-3-ports)
-   [我是否需要安装我的可扩展的宿主控制器的驱动程序？](#ext-drivers)
-   [为什么我的系统上看几个主机控制器？](#hosts)
-   [我已连接只有一个 USB 3.0 集线器时，为什么看到两个中心设备管理器中？](#twohubs)
-   [对于已连接到 2.0 端口的设备加载驱动程序的一组？](#portdrivers)
-   [如何确定是否作为 SuperSpeed 运行我的 USB 3.0 设备？](#superspeed)
-   [为何我的 SuperSpeed USB 设备比等效的高速 USB 设备？](#whynotfaster)
-   [是否可以具有复合和一套硬件中的复合设备？](#compositecompound)
-   [为什么是虚拟机移至新的端口时重新安装我的 USB 设备的一些？](#why-reinstalled)
-   [是否有 USB 产品打包的设计建议的列表？](#designrec)
-   [我是否必须重新编写我的客户端驱动程序以支持 USB 3.0 设备？](#rewritedriver)
-   [我 SuperSpeed 存储设备，Uaspstor.sys 或使用 Usbstor.sys 加载的驱动程序？](#loadeddriver)
-   [Microsoft 支持哪些 USB DWG 类？](#usbdwg)
-   [自定义的 USB 设备应使用哪些设备安装程序类？](#customclass)
-   [为什么不会我的 CPU 进入 C3 时将附加某些 USB 设备？](#cpucthree)
-   [哪些 USB 类驱动程序是否支持选择性挂起？](#selsuspend)
-   [为什么 USB 设备不能从 S3 唤醒 Windows？](#usbawake)
-   [我是否需要安装增强 (USB 2.0) 主机控制器的驱动程序？](#enhdriver)
-   [可以禁用"高速 USB 设备插入非高速 USB 端口"通知？](#disablehi)
-   [是我的 USB 2.0 中心单 TT 或多 TT？](#singlett)
-   [哪些字符或字节是否有效 USB 序列号中？](#usbsn)
-   [内容本地化版本的 Windows 上的字符串请求中使用 LANGID？](#langidloc)
-   [什么 LANGID 用于提取设备的序列号？](#langidsn)
-   [什么是不同的 Windows 版本的最大 USB 传输大小？](#maxxfer)
-   [如何应号分配给多个接口上的复合设备？](#nummultif)
-   [Usbccgp.sys 规定的主要限制是什么？](#usbccgp)
-   [如何启用 USB 核心二进制文件的调试跟踪？](#tracecorebin)
-   [Windows 是否支持接口关联描述符？](#iadesc)
-   [USB 堆栈句柄是否链接在 URB MDLs？](#mdlsinurb)
-   [驱动程序中可以有多个 URB IRP？](#urbirp)
-   [Windows 是否支持 USB 复合中心？](#supportcomposite)
-   [在哪里可以找到更多常见问题 USB 上？](#addlfaq)

## <a name="i-hear-numerous-usb-terms-thrown-around-almost-interchangeably-what-do-they-all-mean"></a>我听到几乎可交换引发周围的大量 USB 条款。 它们都代表什么？


*"得益于 USB 3.0 中，我可以 SuperSpeed USB 拇指驱动器连接到我的 PC 的 xHCI 主控制器和更快地复制文件。"*

让我们来了解一个句子中的 USB 条款。 USB 3.0、 USB 2.0 和 USB 1.0 指从 USB 规范修订号[USB 实现论坛](http://www.usb.org/home)。 USB 规范定义如何的主机 PC 和 USB 设备彼此。

版本号还指示最大传输速度。 最新规范修订版本是 USB 3.0，它指定最多为 5 Gbps; 最大传输速度。 USB 1.0 定义两个不同的数据速率，低速度 （最多 1.5 Mbps) USB 和全速 USB （最多 12 Mbps)。 USB 2.0 定义了新的数据速率，高速 USB (480 Mbps)，同时保持对低和完整速度设备的支持。 USB 3.0 将继续处理所有以前定义的数据速率。 如果您看一下产品打包，SuperSpeed USB 引用最新的 USB 3.0 设备。 高速 USB 用于描述高速 USB 2.0 设备。 USB、 与没有描述符是指低速和全速设备。

除了 USB 协议，还有 USB 主控制器的硬件设备连接到 PC 上的第二个规范。 主机控制器接口规范定义主机控制器硬件和软件交互的方式。 可扩展的主机控制器接口 (xHCI) 定义的 USB 3.0 主控制器。 增强的主机控制器接口 (EHCI) 定义 USB 2.0 主控制器。 通用主机控制器 (UHCI) 和打开主机控制器 (OHCI) 是两个，备用 USB 1.0 主控制器的实现。

## <a name="does-my-pc-have-usb-30-ports"></a>我的 PC 是否有 USB 3.0 端口？


USB 3.0 端口或者标有 SuperSpeed USB 徽标，或者端口是通常蓝色。

![使用 usb 徽标的端口](images/usb-intro-faq-fig1-usblogo.png)

![蓝色 usb 3.0 端口](images/usb-intro-faq-fig2-blueusbport.png)

较新的 Pc 具有 USB 3.0 和 USB 2.0 端口。 如果你想 SuperSpeed USB 设备执行以最高速度，找到 USB 3.0 端口并将设备连接到该端口。 SuperSpeed 设备是已连接 USB 2.0 端口，在高速度进行操作。

此外可以验证特定的端口是设备管理器中的 USB 3.0 端口。 在 Windows Vista 或更高版本的 Windows 中，打开设备管理器中，并从列表中选择端口。

![设备管理器中的 usb 主控制器](images/usb-host-controllers-dm.png)

如果您有一个可扩展的主机控制器，它支持 USB 3.0。

## <a name="do-i-need-to-install-drivers-for-my-extensible-host-controller"></a>我是否需要安装我的可扩展的宿主控制器的驱动程序？


Windows 8 和 Windows Server 2012 包括对 USB 3.0 支持。

如果 PC 具有 USB 3.0 端口，并且在运行早于 Windows 8 的 Windows 版本，由电脑制造商提供主机控制器驱动程序。 如果你需要重新安装这些驱动程序，你必须从制造商处获取它们。

如果您正在运行早于 Windows 8 的 Windows 版本的电脑添加 USB 3.0 控制器卡，则必须安装控制器卡制造商提供的驱动程序。

在 Windows 8 中，USB 3.0 驱动程序 （USB 驱动程序堆栈） 的 Microsoft 提供一套使用大多数主机控制器。 Microsoft USB 3.0 驱动程序堆栈并不适用于 Fresco 逻辑 FL1000 控制器。 若要确定你是否有 FL1000 控制器，打开设备管理器，然后展开**通用串行总线控制器**。 通过右键单击控制器节点中查看控制器属性。 上**详细信息**选项卡上，选择**硬件 Id**列表中的属性。 如果硬件 ID 开头 PCI\\即使\_1B73 & 开发\_1000，它是 FL1000。 该控制器中，下载并安装驱动程序从您的 PC 或控制器卡制造商。

## <a name="why-do-i-see-several-host-controllers-on-my-system"></a>为什么我的系统上看几个主机控制器？


除了连接到您的电脑的 USB 设备，还有多个设备内的 PC 可能通过 USB，如网络摄像机、 指纹读取器、 SD 卡读卡器连接的集成。 若要连接的所有这些设备，并仍提供外部 USB 端口，PC 支持多个 USB 主控制器。

USB 3.0 xHCI 主控制器是完全向后兼容所有 USB 设备的速度、 SuperSpeed、 高速度、 完整速度和较低的速度。 可以连接直接到 xHCI 控制器的任何设备，并期望该设备正常工作。 EHCI 控制器，不是这种情况。 尽管 USB 2.0 规范支持的设备的所有速度，EHCI 控制器仅都支持高速 USB 设备。 为了处理全速和低速 USB 设备，他们必须连接到 EHCI 控制器通过 USB 2.0 中心，或它们必须连接到 UHCI 或 OHCI 控制器。

对于更高版本的电脑，公开的 Pc 的大多数 USB 2.0 端口是 USB 2.0 中心的下游。 此中心连接到 EHCI 控制器。 这样，PC 的 USB 2.0 端口以使用所有的设备的速度。 SuperSpeed 设备为高速设备连接到 2.0 端口时的行为。

USB 2.0 规范发布后，电脑时使用主控制器的组合所支持的所有设备的速度。 单个 USB 2.0 端口将绑定到两个主机控制器、 EHCI 主控制器和 UHCI 或 OHCI 主控制器。 附加设备，硬件动态地将连接路由到两个主机之一。 例程依赖于设备的速度。

## <a name="why-do-i-see-two-hubs-in-device-manager-when-i-have-connected-only-one-usb-30-hub"></a>我已连接只有一个 USB 3.0 集线器时，为什么看到两个中心设备管理器中？


尽管 xHCI 主控制器适用于任何设备的速度，SuperSpeed 集线器将仅适用于 SuperSpeed 设备。 若要确保 USB 3.0 集线器可以使用所有的速度，他们具有两个部分： SuperSpeed 集线器和 USB 2.0 中心。 USB 3.0 集线器时能够支持所有速度的动态路由设备到 SuperSpeed 集线器或 2.0 的中心，根据设备的速度。

打开设备管理器，视图**依连接排序设备**，然后找到您可扩展的主控制器。 当单个 USB 3.0 集线器连接到 USB 3.0 端口时，有两个中心下游的控制器的根集线器。

![设备管理器中的 usb 3.0 集线器](images/usb-3-hub-dm.png)

在下面的示例中，SuperSpeed USB 存储设备和 USB 音频设备都连接到 USB 3.0 集线器。 您可以看到下游 SuperSpeed 集线器的存储设备，音频设备是 USB 2.0 中心的下游。

![使用设备管理器中连接的设备的 usb 3.0 集线器](images/usb-3-hub-connected-devices-dm.png)

## <a name="which-set-of-drivers-is-loaded-for-the-devices-that-are-connected-to-20-ports"></a>对于已连接到 2.0 端口的设备加载驱动程序的一组？


为每种类型的主控制器加载是一组不同的二进制文件。 请务必了解 USB 驱动程序堆栈，Windows 将加载对应于主机控制器，而不是已连接的设备的速度的类型。

在此图中，您可以看到哪些驱动程序加载为每个不同类型的 USB 主控制器。

![windows 8 中的 usb 驱动程序堆栈](images/usb-win8-driver-stacks.png)

如果 USB 3.0 端口正确路由到 xHCI 控制器，则 Windows 加载 xHCI 驱动程序堆栈 （也称为 USB 3.0 驱动程序堆栈）。

如果 USB 2.0 端口连接到通过 USB 2.0 中心 EHCI 控制器，通信都将通过 EHCI 控制器，并加载 USB 2.0 驱动程序堆栈。

有关 USB 驱动程序堆栈中的驱动程序的详细信息，请参阅[USB 宿主端驱动程序在 Windows 中的](https://go.microsoft.com/fwlink/p/?linkid=320134)。

如果 PC 的 USB 2.0 端口使用辅助控制器，该端口路由到主控制器取决于设备的速度。 例如，低速度设备连接通过 UHCI 或 OHCI 控制器，并使用 USBUHCI 或 USBOHCI 驱动程序。 PC 将高速设备路由到 EHCI 控制器，因此，Windows 将使用 USBEHCI 驱动程序。

不同设备的速度不用于确定加载为控制器的驱动程序。 但是，不同的设备的速度可能会确定使用哪个控制器。 控制器始终使用相同的驱动程序。

## <a name="how-do-i-determine-whether-my-usb-30-device-is-operating-as-superspeed"></a>如何确定是否作为 SuperSpeed 运行我的 USB 3.0 设备？


在 Windows 8 中，首先，请确保你已安装的 USB 3.0 端口和 xHCI 主控制器。 如果 SuperSpeed USB 设备连接到 xHCI 主控制器，Windows 8 的 Windows 8 用户界面的特定部分中显示"已连接到 USB 3.0"消息。 如果设备连接到 EHCI 控制器而不是在 XHCI 控制器，将改为读取消息，"设备时，才能执行更快地连接到 USB 3.0"。

在电脑设置中，可以查看这些用户界面消息。

1.  打开超级按钮栏 （将光标拖到顶部或底部右下角的屏幕，键入 Windows 键 + C，或从使用手指右轻扫）。
2.  选择**设置**，然后**更改电脑设置**。
3.  选择**设备**下**电脑设置**。

USB 3.0 设备操作 SuperSpeed 在时，此图显示了用户界面消息。

![运行 superspeed superspeed usb 设备 ](images/usb-superspeed.jpg)

USB 设备操作低于 SuperSpeed 总线速度时，此图显示了用户界面消息。

![superspeed 运行于的高速的 usb 设备 ](images/usb-high-speed.jpg)

这些映像中所示，可以在设备和打印机，查看类似的消息。

![运行 superspeed superspeed usb 设备](images/usb-superspeed-devices.jpg)

![运行于的高速 superspeed 设备](images/usb-high-speed-devices.jpg)

如果 USB 3.0 设备是存储设备，Windows 资源管理器显示类似的消息时选择卷标，如下所示。 请注意，**视图-&gt;详细信息**窗格必须选择要显示的消息。

![运行 superspeed superspeed usb 设备 ](images/usb-superspeed-storage-device.jpg)

![superspeed 运行于的高速的 usb 设备](images/usb-high-speed-storage-device.jpg)

如果你正在编写设备驱动程序， [USBView](https://go.microsoft.com/fwlink/p/?linkid=320135)工具，包括在 Windows Driver Kit (WDK) 中，是非常有用。 对于 Windows 8 WDK，Microsoft 更新 USBView 显示 SuperSpeed USB 信息。 可以使用此工具来确定在 SuperSpeed 运行你的设备。 此图显示了运行中 USBView SuperSpeed 的 USB 3.0 设备。

![运行 superspeed superspeed usb 设备](images/usb-superspeed-usbview.jpg)

如果是设备驱动程序开发人员， [USB 驱动程序堆栈](https://go.microsoft.com/fwlink/p/?linkid=320134)公开称为新 IOCTL [IOCTL\_USB\_获取\_节点\_连接\_信息\_EX\_V2](https://go.microsoft.com/fwlink/p/?linkid=320136)，可以使用的 USB 3.0 设备查询速度信息。

## <a name="why-isnt-my-superspeed-usb-device-faster-than-an-equivalent-high-speed-usb-device"></a>为何我的 SuperSpeed USB 设备比等效的高速 USB 设备？


通常情况下，如果不比高速的 USB 设备的 USB 3.0 USB 设备，未在执行在 SuperSpeed。 如果 SuperSpeed USB 设备连接到 USB 3.0 端口，它可能无法运行在 SuperSpeed，原因如下：

-   使用 USB 2.0 中心。

    如果使用一个中心，请验证它是一个 USB 3.0 集线器。 如果您使用 USB 2.0 中心，将以高速运行任何附加的 SuperSpeed USB 设备。 替换 USB 3.0 集线器，为中心，或者在设备直接连接到 USB 3.0 端口。

-   USB 3.0 集线器上的固件已过时。

    某些早期的 USB 3.0 集线器无法良好运行。 因此，Windows 只使用两个中心的 2.0 部分。 如果设备管理器指示"无法正常工作"中心，此图中所示，Windows 8 不会使用你的中心的 3.0 部分。

    ![非功能性 superspeed usb 集线器](images/usb-superspeed-nonfunctional.jpg)

    可以在 SuperSpeed 设备直接连接到 USB 3.0 端口，或中心上更新固件。 Windows 8 认识到较新的固件的中心。

-   设备使用 USB 2.0 电缆连接。

    请确保用于连接设备电缆是 USB 3.0 电缆。 还有可能 USB 3.0 电缆有信号完整性问题。 在这种情况下，设备可能会切换到高的速度。 如果发生这种情况，则必须使用不同的 USB 3.0 电缆。

-   在设备上的固件已过时。

    通过从制造商的网站获取最新版本更新 SuperSpeed USB 设备的固件。 某些 SuperSpeed USB 设备制造商发布修补程序，作为固件更新的设备中找到的 bug。

-   主控制器上的固件已过时。

    通过从您的 PC 制造商的网站或获取最新版本更新的 USB 3.0 控制器固件在卡制造商的站点中添加。 某些 USB 3.0 控制器制造商发布修补程序，在控制器中，找到作为固件更新的 bug。

-   为您的系统 BIOS 已过时。

    通过从电脑制造商获取最新版本更新为您的系统 BIOS。 某些母板上 BIOS 不正确路由到 xHCI 主控制器到 EHCI 控制器连接的设备。 不正确路由强制运行高速 SuperSpeed USB 设备。 BIOS 更新可以解决此问题。

## <a name="is-it-possible-to-have-a-composite-and-a-compound-device-in-one-piece-of-hardware"></a>是否可以具有复合和一套硬件中的复合设备？


是。 Microsoft Natural Keyboard Pro，它具有三个端口，总线供电集线器，是复合的复合 USB 设备的一个示例。 该设备已连接到端口 1 的复合设备。 向最终用户公开两个其他端口。

连接到端口 1 的设备是低速度复合设备。 设备有两个接口，这两种符合人机接口设备 (HID) 的 USB 设备的标准设备类定义。 复合设备提供了两个 HID 接口而不是多路复用，所有集合通过单一的 HID 接口使用顶级集合。 选择此设计是为了与较旧的 Bios 兼容。

## <a name="why-are-some-of-my-usb-devices-reinstalled-when-they-are-moved-to-a-new-port"></a>为什么是虚拟机移至新的端口时重新安装我的 USB 设备的一些？


在 Windows 2000 和更高版本操作系统，USB 设备从一个端口移至另一个时创建一个新的物理设备对象 (PDO)。 如果硬件报告唯一的 USB 序列号，则不会创建一个新的 PDO。

若要重复使用相同的 PDO 并确保设备体验并未改变设备重新插入到同一个端口或一个新的端口是否，硬件供应商必须在其设备上存储序列号。 Windows 硬件认证计划要求根据序列号必须是唯一的共享设备安装标识符的所有设备。

## <a name="is-there-a-list-of-design-recommendations-for-usb-product-packaging"></a>是否有 USB 产品打包的设计建议的列表？


U-如果已使用过 Microsoft 和其他 USB-如果成员公司开发的独立硬件供应商以包括在其包装的建议的列表。

USB 网站上提供了详细信息。

有关 USB 和高速 USB，请参阅： [ http://www.usb.org/developers/packaging ](http://www.usb.org/developers/packaging/)/。

有关 SuperSpeed USB 参考： <http://www.usb.org/channel/>。

## <a name="do-i-have-to-rewrite-my-client-driver-to-support-usb-30-devices"></a>我是否必须重新编写我的客户端驱动程序以支持 USB 3.0 设备？


所有现有客户端驱动程序应继续工作，因为完整，较低时，或者高速设备连接到 USB 3.0 端口。 在 Windows 8 中，我们已确保与现有客户端驱动程序的兼容性。

USB 3.0 驱动程序堆栈保留 IRQL 级别、 调用方上下文和错误状态;与设备，并确保现有的驱动程序都能够继续将更多交互时，重试频率和计时。 它仍是非常重要。

常见的故障原因是：

-   分析由于 SuperSpeed 终结点配套描述符存在中断的驱动程序的终结点描述符。
-   由于更高的速度，您可能会遇到计时问题应用程序级别的协议。
-   终结点支持的最大数据包大小可能不同。
-   \\由于函数电源管理，计时选择性挂起操作可能会有所不同。

在 Windows 7 和更早版本的操作系统，USB 3.0 驱动程序堆栈由第三方提供。 因此，我们强烈建议测试驱动程序以使用第三方 USB 驱动程序堆栈。

新客户端驱动程序在 Windows 8 中为高的速度和 SuperSpeed USB 设备应选择新的功能。

## <a name="which-driver-is-loaded-for-my-superspeed-storage-device-use-uaspstorsys-or-usbstorsys"></a>我 SuperSpeed 存储设备，Uaspstor.sys 或使用 Usbstor.sys 加载的驱动程序？


USB 附加 SCSI (UAS) 协议是新的大容量存储协议，旨在提高性能，通过已建立的 USB 大容量存储协议，大容量仅传输 (BOT)。 它会减少协议开销，支持 SATA 本机命令队列 (NCQ)，并处理多个并行命令。 若要执行此操作，UAS 利用了新的 USB 3.0 功能为大容量传输被调用的流。

现有大容量存储驱动程序，Usbstor.sys，使用智能机器人应用程序协议。 它适用于所有的设备，包括 SuperSpeed USB 设备的速度。

对于 Windows 8 中，Microsoft 包括新大容量存储类的驱动程序，它使用 UAS 协议 Uaspstor.sys。 由于流是 USB 3.0 中新增的因此 Uaspstor.sys 时，才能使用流在硬件支持 （SuperSpeed USB 设备连接到 xHCI 主控制器） 的流。 该驱动程序还包括对软件流支持，因此它还可以加载的设备高速，而不考虑主机类型。

如果将大容量存储设备连接到 Windows 8，并且该设备支持 UAS，Windows 将加载 Uaspstor.sys。 在某些情况下，那里可能知道特定 xHCI 主控制器上的硬件流的问题或设备的 UAS 协议实现的已知的问题。 在这些情况下，Windows 将回退到智能机器人应用程序协议，并改为加载 Usbstor.sys 驱动程序。

Uaspstor.sys 是 Windows 8 中新增的。 不存在的 Windows 早期版本中。

## <a name="which-usb-dwg-classes-does-microsoft-support"></a>Microsoft 支持哪些 USB DWG 类？


Windows 支持 USB 设备使用组 (DWG) 已定义的多个 USB 类。 有关 USB 类规范和类代码的当前列表，请访问 USB DWG 网站下载，网址[ http://www.usb.org/developers/devclass\_docs ]( https://go.microsoft.com/fwlink/p/?LinkId=623332)。

下表突出显示了在 Windows 中支持的 USB DWG 类，并还标识的支持的每个类的 Windows 版本。

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
<td>Bthusb.sys</td>
<td>Windows XP 及更高版本</td>
</tr>
<tr class="even">
<td>芯片/智能卡接口设备 (CCID)</td>
<td>0x0B</td>
<td>Usbccid.sys</td>
<td><p>Windows Server 2008 和更高版本</p>
<p>Windows Vista 及更高版本</p>
<p>Windows Server 2003<em></p>
<p>Windows XP</em></p>
<p>Windows 2000<em></p></td>
</tr>
<tr class="odd">
<td>Hub 类</td>
<td>0x09</td>
<td>Usbhub.sys</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="even">
<td>人体学接口设备 (HID)</td>
<td>0x03</td>
<td>Hidusb.sys</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="odd">
<td>大容量存储类 (MSC)</td>
<td>0x08</td>
<td>Usbstor.sys</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="even">
<td>USB Attached SCSI (UAS)</td>
<td>0x08</td>
<td>Uaspstor.sys</td>
<td><p>Windows Server 2012</p>
<p>Windows 8</p></td>
</tr>
<tr class="odd">
<td>打印类</td>
<td>0x07</td>
<td>Usbprint.sys</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="even">
<td>扫描/图像处理 (PTP)</td>
<td>0x06</td>
<td><p>WpdUsb.sys</p>
<p>Usbscan.sys</p></td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="odd">
<td>媒体传输 (MTP)</td>
<td>0x06</td>
<td>WpdUsb.sys</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p></td>
</tr>
<tr class="even">
<td>USB 音频类</td>
<td>0x01</td>
<td>Usbaudio.sys</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="odd">
<td>调制解调器类 (CDC)</td>
<td>0x02</td>
<td>Usbser.sys</td>
<td><p>Windows Server 2003 及更高版本</p>
<p>Windows XP 及更高版本</p>
<p>Windows 2000 及更高版本</p></td>
</tr>
<tr class="even">
<td>视频类 (UVC)</td>
<td>0x0E</td>
<td>Usbvideo.sys</td>
<td><p>Windows Vista 及更高版本</p>
<p>Windows XP</em></p></td>
</tr>
</tbody>
</table>

 

\*由于此驱动程序可能已释放晚于操作系统加载此驱动程序所需的特殊说明。 Windows 类驱动程序可能不支持的所有功能所述 DWG 类规范中。 在这种情况下，该驱动程序不会加载基于类匹配。 类规范中实现功能的其他详细信息，请参阅 WDK 文档。

## <a name="which-device-setup-class-should-i-use-for-a-custom-usb-device"></a>自定义的 USB 设备应使用哪些设备安装程序类？


Microsoft 提供的系统定义的安装程序类用于大多数设备类型。 系统定义的安装程序类 Guid Devguid.h 中定义。 有关其他信息，请参阅 WDK。 有关 Windows 的列表类 Guid，请参阅以下主题：

-   [向供应商提供的系统定义的设备安装程序类](https://go.microsoft.com/fwlink/p/?linkid=320141)
-   [保留供系统使用的系统定义的设备安装程序类](https://go.microsoft.com/fwlink/p/?linkid=320142)

独立硬件供应商必须使用 USB 设备的类型而不是总线类型相关联的安装程序类。 如果你要开发 Microsoft 尚未提供现有类 GUID 的设备类型，可以定义新的设备安装程序类。

在 Windows 8 中，定义新的安装程序类，名为**USBDevice** (ClassGuid = {88BAE032-5A81-49f0-BC3D-A4FF138216D6})。 如果你正在开发一种设备类型，将与设备相关联**USBDevice**而不是安装程序类， **USB**。 **USBDevice**类适用于 Windows Vista 和更高版本的操作系统。

安装程序类**USB** (ClassGuid = {36fc9e60-c465-11cf-8056-444553540000}) 已保留仅适用于 USB 主控制器和 USB 集线器和必须不能用于其他设备类别。 未正确使用此安装程序类可能会导致设备驱动程序故障 Windows 徽标测试。

## <a name="why-wont-my-cpu-enter-c3-when-i-attach-some-usb-devices"></a>为什么不会我的 CPU 进入 C3 时将附加某些 USB 设备？


当连接 USB 设备时，USB 主控制器轮询框架计划程序，这是一个直接内存访问 (DMA) 总线主操作。 "中断事件"如总线主流量、 中断或其他多个系统活动移动 C3 超出 CPU，因为根据定义，在 C3 时不能 snooped CPU 缓存。

有两种方法来解决此问题：

-   硬件删除操作。

    有时，可以从通用串行总线以电子方式断开硬件。 例如，存储媒体不再从 USB 读取器，USB 读取器可以模拟电子断开连接并重新插入媒体时重新连接。 在这种情况下，由于主机控制器上都不到 USB 设备，可能出现 C3 转换。

-   选择性挂起。

    Windows XP 和更高版本操作系统中提供唯一的替代方法是支持 USB 选择性挂起。 此功能允许挂起其控制当设备变为空闲状态，即使系统本身将保持完全正常运行的电源状态 (S0) USB 设备的驱动程序。 选择性挂起就特别有效，如果所有 USB 函数驱动程序都支持它。 如果一个驱动程序不支持它，CPU 无法进入 C3。 有关选择性挂起的其他信息，请参阅 WDK。

## <a name="which-usb-class-drivers-support-selective-suspend"></a>哪些 USB 类驱动程序是否支持选择性挂起？


下面是 USB 类在 Windows 8 中支持的驱动程序选择性挂起的列表：

-   蓝牙

    此驱动程序可以有选择地挂起正在运行 Windows XP Service Pack 2 和更高版本的 Windows 的计算机上的设备。 驱动程序需要蓝牙无线配置描述符中设置的自供电和远程唤醒位。 该驱动程序有选择地挂起 (D2) 蓝牙无线时没有活动的蓝牙连接存在。

-   USB HID

    此驱动程序可以有选择地挂起 HID 设备。 它由你负责触发上所有设备状态更改的远程唤醒信号。 若要启用 HID 堆栈中的选择性挂起，必须为特定设备的 VID + PID 启用 SelectiveSuspendEnabled 注册表值。 有关示例，请参阅 Input.inf。

    此驱动程序支持 Windows 8 的连接待机系统，在进入选择性挂起 (D2)，当系统处于连接待机状态时。 此驱动程序可将系统唤醒并在屏幕上。

-   USB 集线器

    此驱动程序可以有选择地挂起根或外部集线器时向其或附加到该中心的所有设备可以有选择地都挂起时没有连接任何设备。

-   USB 调制解调器

    没有活动的调制解调器的连接存在时，此驱动程序可以有选择地挂起设备。

-   USB 存储 （智能机器人应用程序）

    此驱动程序支持 Windows 8 连接待机，当这些系统进入连接待机的系统上，可以有选择地挂起 (D3) 存储设备。 HID，如没有注册表替代用于启用选择性挂起所有 Windows 8 系统上。

-   USB 存储 (UAS)

    此驱动程序可以有选择地挂起 (D3) 存储设备时磁盘超时时间处于空闲状态。

-   USB 视频

    此驱动程序可以有选择地挂起 (D3) 网络摄像头在 Windows Vista 和更高版本操作系统上。

-   USB 音频

    此驱动程序可以有选择地挂起 (D3) Windows 7 和更高版本操作系统上的 USB 音频设备在计算机使用电池电源时。

-   复合 USB

    在挂起所有子级时，此驱动程序可以有选择地都挂起 (D3) 复合设备。 在系统上支持 D3 冷，所有子项必须都选择加入 D3 冷。

-   USB 智能卡

    此驱动程序可以有选择地挂起 (D2) 智能卡接口设备，默认情况下，Windows 7 和更高版本操作系统中。

-   泛型 USB 外围设备 (WinUSB)

    此驱动程序在 Windows Vista 和更高版本操作系统上默认情况下，可以有选择地挂起 (D3) 设备。

-   WWAN:3g 或 WiMax 连接器

    此驱动程序可以有选择地挂起的设备。 如果有一个有效的订阅，则设备将进入 D2，而无需活动的订阅，则设备将进入 D3。

## <a name="why-cant-a-usb-device-awaken-windows-from-s3"></a>为什么 USB 设备不能从 S3 唤醒 Windows？


USB 设备不能被 Windows 唤醒从 S3，原因有多种，其中包括：

1.  不正确的 BIOS。

    验证在计算机上安装了最新的 BIOS。 若要获取最新的 bios 的计算机，请访问的 OEM 或考虑了 ODM 网站。

2.  未启用唤醒的 BIOS。

    某些 Bios，使其可以禁用从 S3 和 S4 唤醒。 验证已启用 BIOS 从 S3 唤醒。

3.  未设置 USBBIOSx 注册表项。

    Windows XP 的全新安装没有 USBBIOSx 注册表项。 如果 OEM 或考虑了 ODM 验证 BIOS 能否从 S3 唤醒，将此注册表项设置为 0x00 并重新启动计算机。

4.  主控制器没有 S3 和 S4 中的能力。

    PC 处于低功率状态时，很多时候 PC 剪切到外接卡电源。 如果外接卡未通电，它将不是能够检测到发生唤醒事件，并且不能以唤醒 PC。

有关其他信息，请参阅帮助和支持中心在 Windows XP 和更高版本的 Windows 中的 USB 疑难解答。

## <a name="do-i-need-to-install-drivers-for-my-enhanced-usb-20-host-controller"></a>我是否需要安装增强 (USB 2.0) 主机控制器的驱动程序？


以下版本的 Windows 支持 USB 2.0 增强的主控制器：

-   Windows Vista 及更高版本
-   Windows Server 2003 及更高版本
-   Windows XP Service Pack 1
-   Windows 2000 Service Pack 4

**请注意**  因为 Windows 2000 和 Windows XP 发布之前提供的 USB 2.0 硬件、 驱动程序针对这些操作系统 service pack 中发布。 若要安装驱动程序：

1.  按照以验证您的计算机有 USB 2.0 端口和需要安装增强的主控制器的驱动程序的第一个问题的答案中所述的过程。
2.  在设备管理器窗口中，展开**其他设备**部分中的第一个问题所述，然后双击**通用串行总线 (USB) 控制器**。
3.  上**常规**选项卡的属性对话框中，单击**重新安装驱动程序**。

    ![重新安装驱动程序](images/usb-reinstall-driver.jpg)

4.  在添加新硬件向导中，选择**自动安装软件 （推荐）**，然后单击**下一步**。 继续执行向导，接受所有默认选项，直到到达最后一页的向导中，然后单击**完成**。 您可能需要重新启动计算机以完成安装。

 

Windows XP Service Pack 1 中的 USB 2.0 的可用性的其他信息，请参阅 Microsoft 知识库文章 329632，"如何获取和安装 USB 2.0 Windows XP Service Pack 1 中的驱动程序"处[ http://support.microsoft.com/default.aspx?scid=KB;EN-US;Q329632 &](https://support.microsoft.com/kb/329632)。

**请注意**  以确保拥有最新的更新在计算机上安装，请定期访问 Windows Update。

 

## <a name="can-i-disable-the-hi-speed-usb-device-plugged-into-non-hi-speed-usb-port-notice"></a>可以禁用"高速 USB 设备插入非高速 USB 端口"通知？


Windows XP 和更高版本的 Windows 时高速 USB 设备插入到不支持高速的 USB 端口创建一个弹出通知。 若要从设备获取最快的性能，用户必须单击通知，并按照屏幕上的说明。

若要禁用通知，请按照下列步骤：

1.  启动设备管理器中，在此 FAQ 中的第一个问题中所述。
2.  在设备管理器窗口中，展开**通用串行总线控制器**节点。 查找标题中包含单词"通用"或"打开"的主机控制器。 如果找到，请双击它。
3.  上**高级**选项卡**属性**对话框中，选择**不要告诉我有关 USB 错误**。

**请注意**  前面的过程禁用所有 USB 通知，而不仅仅是"高速 USB 设备插入非高速端口"。

 

有关 Windows XP Service Pack 1 中的 USB 2.0 支持的其他信息，请参阅 Microsoft 知识库文章 329632，"如何获取和安装 USB 2.0 中 Windows XP Service Pack 1，驱动程序在[ http://support.microsoft.com/default.aspx?scid=KB;EN-US;Q329632](https://support.microsoft.com/kb/329632)。

## <a name="is-my-usb-20-hub-single-tt-or-multi-tt"></a>是我的 USB 2.0 中心单 TT 或多 TT？


USB 2.0 集线器能够拥有中心 (单个 TT) 上的所有下游面向的端口的一个事务转换器 (TT)，也可以有一个 TT 为中心 (多个 TT) 上每个下游面向的端口。

值**bDeviceProtocol** USB 设备描述符字段和**bInterfaceProtocol** USB 接口描述符字段指示集线器是否是单 TT 或者多 TT:

-   单 TT。 **bDeviceProtocol** == 0x01
-   多 TT。 **bDeviceProtocol** == 0x02

**Usbhub.sys**使用此设置来启用多 TT 模式或单 TT 模式。 Windows XP 及更高版本，Usbhub.sys 始终启用多 TT 集线器上的多 TT 模式。 TT 布局有关的其他详细信息，请参阅 11.14.1.3 和的 11.23.1 [USB 2.0 规范](http://www.usb.org/developers/docs)。

## <a name="what-characters-or-bytes-are-valid-in-a-usb-serial-number"></a>哪些字符或字节是否有效 USB 序列号中？


USB 设备描述符**iSerialNumber**字段指示设备是否具有序列号和数存储，按如下所示：

-   **iSerialNumber** = = 0x00:USB 设备有没有序列号。
-   **iSerialNumber** ！ = 0x00:USB 设备都有一个序列号。 分配给的值**iSerialNumber**是序列号的字符串索引。

如果设备具有序列号，序列号必须唯一标识同一设备的每个实例。

例如，如果两个设备描述符具有相同的值为 i**dVendor**， **idProduct**，并**bcdDevice**字段， **iSerialNumber**字段必须是不同，来区分从另一台设备。

Plug and Play 要求 USB 序列号中的每个字节有效。 如果单字节无效，Windows 将放弃序列号，并将设备视为如同它具有无序列号。 下面的字节值不是有效 USB 序列号的：

-   -   0x2C。
-   值小于 0x20。
-   大于 0x7F 的值。

有关其他详细信息**iSerialNumber**值，请参阅部分 9.6.1 [USB 2.0 规范](http://www.usb.org/developers/docs)。

## <a name="what-langid-is-used-in-a-string-request-on-localized-builds-of-windows"></a>内容本地化版本的 Windows 上的字符串请求中使用 LANGID？


USB 设备通过 USB 设备描述符将 iSerialNumber 字段设置为序列号的字符串索引指示序列号的存在。 若要检索序列号，Windows 问题字符串请求设置为 0x0409 （美国的语言标识符 (LANGID)英文版）。 Windows 始终使用此 LANGID 检索 USB 序列号，即使对于本地化为其他语言的 Windows 版本。

## <a name="what-langid-is-used-to-extract-a-devices-serial-number"></a>什么 LANGID 用于提取设备的序列号？


USB 设备通过 USB 设备描述符将 iSerialNumber 字段设置为序列号的字符串索引指示序列号的存在。 若要检索序列号，Windows 问题字符串请求设置为 0x0409 （美国的语言标识符 (LANGID)英文版）。 Windows 始终使用此 LANGID 检索 USB 序列号，即使对于本地化为其他语言的 Windows 版本。

## <a name="what-is-the-maximum-usb-transfer-size-for-different-windows-versions"></a>什么是不同的 Windows 版本的最大 USB 传输大小？


请参阅[传输各种操作系统上的最大大小的 USB](https://support.microsoft.com/kb/832430)。

## <a name="how-should-numbers-be-assigned-to-multiple-interfaces-on-a-composite-device"></a>如何应号分配给多个接口上的复合设备？


Windows 将为复合设备具有多个接口上的第一个配置的 USB 设备。

对于 Windows XP Service Pack 1 和 Windows 的早期版本：

-   接口号必须是从零开始。
-   接口号必须是连续和不断增加。

对于 Windows XP Service Pack 2 和更高版本的 Windows，接口号只需将不断增加，不连续。

有关接口号的其他信息，请参阅[复合 USB 设备的接口不按顺序编号不能在 Windows XP](https://support.microsoft.com/kb/814560)。

接口的备用设置应分配的所有版本的 Windows 中的如下所示：

-   接口的默认值始终是备用设置为零。
-   其他备用设置数字必须是连续和不断增加。

有关替代设置的其他信息，请参阅部分第 9.6.5 [USB 2.0 规范](http://www.usb.org/developers/docs)。

## <a name="what-are-the-major-restrictions-imposed-by-usbccgpsys"></a>Usbccgp.sys 规定的主要限制是什么？


**Usbccgp.sys**支持复合设备：

-   Windows Me
-   Windows XP
-   Windows Server 2003
-   Windows Vista
-   Windows Server 2008

尽管这仍是可以加载**Usbhub.sys**作为复合设备上这些及更高版本的父驱动程序版本的 Windows 中，Microsoft 不建议将它因为它可能会导致硬件兼容性错误。 应使用**Usbccgp.sys**相反。

若要确保加载正确的驱动程序为复合设备，使用 Include 和需求指令在 INF 文件中，按如下所示：

``` syntax
Include = USB.INF
Needs = Composite.Dev
```

硬件设备和驱动程序通过所规定的主要限制**Usbccgp.sys**如下所示：

-   Usbccgp 仅支持默认配置，配置 0。
-   Usbccgp 不支持选择性挂起 Windows XP 和 Windows Server 2003 中。 仅在 Windows Vista 和更高版本的 Windows 中支持此功能。
    **请注意**   Usbccgp 支持选择性挂起在 Windows XP SP1 和更高版本的 Windows XP 中，但使用有限的功能。 对于这些版本的 Windows，复合设备放入选择性挂起，仅当设备的每个子函数具有挂起的空闲 IRP。 Usbccgp 不支持选择性挂起中的 Windows XP RTM

     

-   Usbccgp 仅在 Windows XP SP2、 Windows Server 2003 SP1 和更高版本的 Windows 中支持的接口关联描述符 (IAD)。
-   Usbccgp 仅在 Windows XP SP2、 Windows Server 2003 SP1 和更高版本的 Windows 中支持不连续接口数字。

## <a name="how-do-i-enable-debug-tracing-for-usb-core-binaries"></a>如何启用 USB 核心二进制文件的调试跟踪？


请参阅博客文章有关[如何包括和驱动程序的公共 PDB 文件中查看 WPP 跟踪消息](http://blogs.msdn.com/b/usbcoreblog/archive/2013/06/29/wpp-blog-post.aspx)。

有关 USB core 堆栈调试的其他信息，请参阅[如何启用详细调试跟踪在各种驱动程序和子系统中的](https://support.microsoft.com/kb/314743)。

## <a name="does-windows-support-interface-association-descriptors"></a>Windows 是否支持接口关联描述符？


是。 USB 2.0 接口关联描述符 (IAD) 工程更改通知 (ECN) 引入了描述的接口的分组和其替代函数内的设置的新标准方法。 IAD 可以用于标识两个或多个连续的接口和一个函数内的替代设置。

Microsoft 目前正与 Ihv 开发支持 IAD 的设备。 以下操作系统都具有对 IAD 支持：

-   Windows XP Service Pack 2 和更高版本
-   Windows Server 2003 Service Pack 1 和更高版本
-   Windows Vista

## <a name="does-the-usb-stack-handle-chained-mdls-in-a-urb"></a>USB 堆栈句柄是否链接在 URB MDLs？


通过堆栈，是 Windows 附带的 USB 3.0 驱动程序支持此功能。

## <a name="can-a-driver-have-more-than-one-urb-in-an-irp"></a>驱动程序中可以有多个 URB IRP？


否。 Windows 附带的 USB 堆栈不支持此功能。

## <a name="does-windows-support-usb-composite-hubs"></a>Windows 是否支持 USB 复合中心？


复合的 USB 设备-也称为多功能的 USB 设备的公开多个函数，其中每个可将其视为一个独立的设备。 系统将 USB 泛型父驱动程序，加载**Usbccgp.sys**，以充当 eaech 设备的函数的父驱动程序。 USB 泛型父驱动程序枚举复合设备函数，就好像它们是不同的 USB 设备，然后，创建一个 PDO 并构造一个设备堆栈，每个函数。

复合的 USB 设备不能公开作为的集线器的函数。 Windows 不会正确地枚举此类集线器和尝试安装该设备可能会导致系统崩溃。

## <a name="where-can-i-find-additional-faqs-on-usb"></a>在哪里可以找到更多常见问题 USB 上？


请参阅 USB-如果常见问题解答页面<http://www.usb.org/developers/usbfaq/>。

## <a name="related-topics"></a>相关主题
[对所有开发人员的 USB 概念](usb-concepts-for-all-developers.md)  
[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



