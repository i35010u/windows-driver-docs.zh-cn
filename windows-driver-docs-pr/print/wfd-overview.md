---
title: Wi-Fi Direct 打印概述
description: 提供有关受支持的用户体验和用例 Wi-Fi Direct 打印信息。
ms.assetid: 40ED3410-EC46-42C8-B09B-8010639F2268
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e6949b11b989e091aa6ed932b711625b6059c07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547781"
---
# <a name="wi-fi-direct-printing-overview"></a>Wi-Fi Direct 打印概述


## <a name="supported-user-experiences"></a>受支持的用户体验


**与从 Windows Wi-Fi Direct 打印机配对**

在与海外伙伴会议中，业务执行经理接收一个协定修订并现在必须打印在她会议前的已更新的副本。

她查找 Windows 认证的合作伙伴的机构支持 Wi-Fi Direct 的打印设备。 她启动配对设备与她的 Windows 图面之间和她快速建立到设备的连接并已准备就绪。 她将打印该文档的多个副本，并且能够向其合作伙伴提供的新的、 已批准的协定。

在她的老伴到机场; 她是几个小时更高版本在手动签名协定。

此方案描述了：

配对使用 PIN

-   在控制面板中选择设备后系统会提示她的 PIN 的连接。 她输入提供给她的接线员的 PIN 号码。 完成连接和她已准备就绪

配对使用 Ad Hoc PIN

-   之后，在控制面板中选择设备设备的控制面板会要求她输入 PIN 匹配一个她 （就像蓝牙配对） 其设备上输入。 她在设备上的控制面板上输入 pin 码，然后在提示进入相同数量，在 PC 上。 完成连接和她已准备就绪。

**打印到以前配对的 Wi-Fi Direct 打印机**

其他用户使用其移动宽带连接时他是在家里其 Windows PC 上获取 Internet 连接。 他拥有 Wi-Fi Direct 打印设备，其中他以前配对到并安装在他的 Windows PC 上。

他致力于在家里的文档，并需要打印打印件。 他在他的应用程序中选择"打印"。 他 Wi-Fi Direct 打印机始终是广播通过 Wi-Fi Direct，他目前在范围内。 打印对话框出现时，他 Wi-Fi Direct 打印机将显示"联机"。 他选择设备，并单击打印。 他的 Windows PC 建立与设备的连接并发送打印作业。 向他，他 Wi-Fi Direct 打印机将显示如何根据他已通过网络或直接使用任何其他打印机连接。 打印作业输出，他可以继续编辑。

## <a name="use-cases"></a>用例


**打印机的首次配对**

手动连接到的 WI-FI DIRECT 通过新式设备控件面板前置条件的打印设备

-   用户位于范围内 Wi-Fi Direct 打印设备
-   Wi-Fi Direct 打印设备的驱动程序是在用户设备上
-   Wi-Fi Direct 打印设备满足 Windows 认证要求

触发器

用户类型在"添加打印机"Windows 开始屏幕中，选择"设置"，并将启动设备控制面板。

步骤

1.  设备控制可用的打印设备的面板中搜索
2.  DAF 发出 L2 质询的 Wi-Fi Direct (WFD) 设备
3.  可用 WFD 打印设备显示为用户的设备列表中的可用选项
4.  用户单击 WFD 打印设备上
5.  DAF 建立 WFD 设备和触发的 L2/L3 连接垂直配对使用 WSD 提供程序。 为设备生成队列和驱动程序配置。
6.  WFD 提供程序断开与设备的连接

后置条件

-   建立 Wi-Fi Direct 打印机的打印队列
-   打印队列将显示"可用"，只要 WFD L2 信号质询成功

备用流

不适用

注意事项

不适用

 

手动连接到的 WI-FI DIRECT 打印设备通过添加打印机向导前置条件

-   用户位于范围内 Wi-Fi Direct 打印设备
-   Wi-Fi Direct 打印设备的驱动程序是在用户设备上
-   Wi-Fi Direct 打印设备满足 Windows 认证要求

触发器

用户打开经典控制面板，并启动设备和打印机控制面板。

步骤

1.  用户启动的设备和打印机控制面板
2.  用户单击"添加设备"
3.  DAF 发出 L2 质询的 Wi-Fi Direct (WFD) 设备
4.  可用 WFD 打印设备显示为用户的设备列表中的可用选项
5.  用户单击 WFD 打印设备上
6.  DAF 建立 WFD 设备和触发的 L2/L3 连接垂直配对使用 WSD 提供程序。 为设备生成队列和驱动程序配置。
7.  WFD 提供程序断开与设备的连接

后置条件

-   建立 Wi-Fi Direct 打印机的打印队列
-   打印队列将显示"可用"，只要 WFD L2 信号质询成功

备用流

不适用

注意事项

不适用

 

错误连接到打印设备前置条件

用户启动配对使用：

-   新式设备控制面板中，"手动连接到 WI-FI 直接打印设备通过现代设备 CONTROL PANEL"更高版本中所述
-   设备和打印机控制面板中，如上面"手动连接到 WI-FI DIRECT 打印设备通过添加打印机向导"中所述

触发器

在配对/队列安装期间发生失败事件。

步骤

1.  删除任何部分设置打印队列。
2.  失败的通知用户。

后置条件

-   用户的打印系统返回到前配对尝试的状态

备用流

-   如果错误是由于缺少驱动程序，可以下载该驱动程序，或将其添加 （x86 或 amd64 不按流量计费的连接上），被提示用户要执行此操作，然后重新尝试配对。

注意事项

不适用

 

连接到 WI-FI DIRECT 打印设备使用必需 PIN 前提条件

用户启动配对使用：

-   新式设备控制面板中，"手动连接到 WI-FI 直接打印设备通过现代设备 CONTROL PANEL"更高版本中所述
-   设备和打印机控制面板中，如上面"手动连接到 WI-FI DIRECT 打印设备通过添加打印机向导"中所述

触发器

设备需要 PIN 才能配对

步骤

1.  1. 用户已收到所需的打印设备的 PIN
2.  2. WSD 在安装期间，系统会提示用户输入 PIN
3.  3. 用户输入 PIN 和配对完成

后置条件

-   打印队列已正确设置

备用流

-   如果错误是由于缺少驱动程序，可以下载该驱动程序，或将其添加 （x86 或 amd64 不按流量计费的连接上），被提示用户要执行此操作，然后重新尝试配对。

注意事项

-   Ad hoc PIN
    1.  需要这两个在打印机上输入的 PIN 和类似于蓝牙配对设备。
    2.  WSD 在安装期间，用户输入正确的 PIN 在设备上和客户端电脑出现提示时。
    3.  用户输入 PIN 和配对完成。

<!-- -->

-   无法输入 PIN
    1.  用户已收到客户端 PIN 或临时 PIN 是必需的。
    2.  WFD 安装期间输入 PIN 提示用户。
    3.  用户输入 PIN 不正确。
    4.  PIN 不正确，并且配对无法完成，则通知用户。
    5.  发现已终止。 没有队列是设置。

**后置条件**:任何打印队列不是设置。

 

**打印**

从应用程序的前置条件的 WI-FI DIRECT 打印设备的使用

-   用户位于范围内 Wi-Fi Direct 打印设备
-   用户已成功完成的首次与 Wi-Fi Direct 打印设备中，匹配"打印机-第一次上面的配对"中所述。

触发器

用户尝试从应用程序打印

步骤

1.  DAF 问题 L2 面临的挑战 Wi-Fi Direct (WFD) 设备。
2.  对 L2 的质询的响应已知的 WFD 打印设备显示为"可用"给用户
3.  用户选择 WFD 打印设备并单击"打印"
4.  DAF 与用户选择 WFD 设备建立 L2/L3 连接，并建立 L3 WSD 连接。 到设备的引用计数会递增。
5.  后台处理、 呈现，并向设备发送打印作业
6.  到设备的引用计数将递减。 如果引用计数后递减等于 0，则连接将关闭。

后置条件

-   打印作业已成功发送到打印设备。

备用流

不适用

注意事项

-   队列是相同的所有其他打印队列中保留在 Windows PC 上。 用户预期能够重新连接和打印到而不考虑时间失效之间配对设备且后续使用。 用户应具有重新配对打印到的唯一情况是如果打印机具有修剪的连接信息和配对，用户的信息已被删除。 应尽量减少重新配对，以提供更好的用户体验。 这意味着该设备必须保持在内存中的合理地维护用于预期用途的配对数。 例如，适用于家庭打印机可能维护 10-25 配对。 办公室中使用的打印机可以维护多得多。

 

## <a name="considerations-for-pairing"></a>有关配对的注意事项


**持久的组**

Windows 需要，一旦创建 Wi-Fi Direct 打印设备的打印队列时，Windows 客户端将能够重新连接到该设备，而无需重新配对。 为 Wi-Fi Direct DAF 提供程序将关闭连接后，会创建队列和设备。 因此必须将配对的信息保存为用户在打印时与设备重新连接。

如果在设备端上删除配对的信息，而且每次连接后，用户将永远无法打印到该设备。 用户将在其中将设备添加 PC 设置、 安装后，关闭连接和配对中删除一个循环中要求用户再次在电脑设置添加设备。

**并发连接**

应打印设备将能够对 PC 的多个连接请求做出响应。 因此打印设备应以满足此方案中实现具有多个组的并发连接。

**已删除的配对**

Windows 需要维护配对的信息，以允许用户打印到 Wi-Fi Direct 队列而不重新预配的 Wi-Fi Direct 设备。 但是，理解有有限数量的设备可以存储的配对。 强烈建议在设备具有足够的内存来维护合理的配对的预期用法的连接数。 例如，适用于家庭或小型办公室中使用的设备可能还记得 30 连接。 但是，旨在用于被广泛使用并在公共环境中的反复使用的设备可能需要记住更多的用户，以确保连接不太频繁地修剪。

**已删除的配对方案**:Windows 不会重新建立与 Wi-Fi Direct 设备的完整连接用户提交打印作业为止。 因此，如果设备已删除适用于 Windows PC 的配对信息，Windows 将不知道这直到打印作业已排入队列。 **用户将能够重新使用设备设置的连接和重新配对，但是，这样做会导致打印队列中删除并重新生成和任何已排队的打印作业都将丢失进程中。** 通过维护足够数量的内存中的配对，设备可以尽量减少用户必须重新配对和重新提交它们的打印作业的实例数。

**适用于 PC 的 Wi-fi 驱动程序注意事项**

Windows 8 徽标要求的 Wi-fi 模块需要模块以支持 Wi-Fi Direct。 但是，还必须在模块提供的驱动程序中支持此功能。 即使该模块是能够执行此操作在 Windows 8 中的大多数收件箱驱动程序不支持 Wi-Fi Direct。 这些模块的制造商已更新的驱动程序可用其驱动程序网站。 更新的驱动程序将会更广泛之后的下一个 Windows 版本。

**Windows 8 徽标的 WI-FI 模块**:下表提供针对 Windows 8 提交徽标的 Wi-fi 直接模块的非详尽列表。 此信息在 NDA 下共享并不是以任何形式重新分发。 提供数据，帮助合作伙伴标识应能够使用 Wi-Fi Direct Wi-fi 模块。 如中所述**6.2.4**、 这些设备的收件箱驱动程序可能不支持 Wi-Fi Direct 和更新的驱动程序将需要下载和安装前测试。

Windows RT

Broadcom 802.11abgn 无线 SDIO 适配器 Marvell AVASTAR 无线 N 网络控制器 (SDIO) Windows 8 （64 位）

Atheros 无线网络适配器 Broadcom 802.11 a c 无线网络适配器 Broadcom 802.11 a c 无线 USB 适配器 Broadcom 802.11n 双外网络无线适配器 Broadcom 802.11n 网络适配器 Broadcom 802.11n 无线网络适配器 intel （)迅驰® 高级 N + WiMAX 6150 intel （） 迅驰® 高级 N + WiMAX 6250 intel （） 迅驰® 高级-N 6200 intel （） 迅驰® 高级-N 6205 intel （） 迅驰® 高级-N 6235 intel （） 迅驰® ULTIMATE-N 6300 intel （） 迅驰ULTIMATE-N 6300 AGN intel （) 迅驰® 无线 N 105 intel （) 迅驰® 无线 N 135 intel （) 迅驰® 无线 N 2200 intel （) 迅驰® 无线 N 2230 杀手级无线 N Marvell AVASTAR 350N 无线网络控制器 N150MA N300MA QualcommAtheros 无线网络适配器 Realtek 8812AU 无线 LAN 802.11 a c USB NIC Realtek RTL8188CE 无线 LAN 802.11n PCI-E NIC Realtek RTL8188CU/RTL8191CU/RTL8192CU/RTL8188RU 无线 LAN 802.11n USB 2.0 网络适配器 Realtek RTL8188E 无线 LAN802.11 n PCI-E NIC Realtek RTL8188EE 无线 LAN 802.11n PCI-E NIC Realtek RTL8723A 无线 LAN 802.11n USB 2.0 网络适配器 Realtek RTL8723AE 无线 LAN 802.11n PCI-E NIC Realtek 无线 LAN 802.11n USB 2.0 端口的网络适配器 WNA3100M Windows 8 （32 位）

Atheros 无线网络适配器 Broadcom 11ac 网络无线适配器 Broadcom 802.11abgn 无线 LAN SDIO 适配器 Broadcom 802.11abgn 无线 SDIO 适配器 Broadcom 802.11ac 无线网络适配器 Broadcom 802.11ac 无线 USB 适配器 Broadcom802.11 n 双外网络无线适配器 Broadcom 802.11n 网络适配器 Broadcom 802.11n 无线网络适配器 intel （) 迅驰® 高级 N + WiMAX 6150 intel （） 迅驰® 高级 N + WiMAX 6250 intel （） 迅驰® 高级-N 6200 intel （）迅驰® 高级-N 6205 intel （) 迅驰® 高级-N 6235 intel （) 迅驰® ULTIMATE-N 6300 intel （) 迅驰® ULTIMATE-N 6300 AGN intel （) 迅驰® 无线 N 105 intel （) 迅驰® 无线 N 135 intel （) 迅驰® 无线-N 2200Intel （) 迅驰® 无线 N 2230 杀手级无线 N Marvell AVASTAR 350N 无线网络控制器 N150MA N300MA Qualcomm Atheros 无线网络适配器 Realtek 8812AU 无线 LAN 802.11 a c USB NIC Realtek RTL8188CE 无线 LAN 802.11n PCI-E NICRealtek RTL8188CU/RTL8191CU/RTL8192CU/RTL8188RU 无线 LAN 802.11n USB 2.0 网络适配器 Realtek RTL8188E 无线 LAN 802.11n PCI-E NIC Realtek RTL8188EE 无线 LAN 802.11n PCI-E NIC Realtek RTL8723A 无线 LAN 802.11n USB 2.0 网络适配器Realtek RTL8723AE 无线 LAN 802.11n PCI-E NIC Realtek 无线 LAN 802.11n USB 2.0 端口的网络适配器 WNA3100M**在 Windows 中的设备名称**

Windows 使用的 Wi-fi P2P IE 格式 P2P 设备信息子元素的设备名称属性组所有者设备时在 Windows 中设置的设备名称。 作为设备的名称在所有 Windows 用户界面中将显示在中，此属性应包含用户有意义的名称。

![p2p ie 格式 oob 设备信息元素](images/wfd-p2pieformat.png)

*P2P IE 格式 OOB 设备信息元素*

**组所有权**

打印设备必须始终为组所有者。 Windows 打印系统不支持 Windows PC 所在组的所有者的方案。

存在一些已知问题有关组所有权和 5 GHz 网络。 Windows 不支持与设备使用 2.4 GHz 通道，如果在 PC 已启动组所有者，并且已连接到 5 GHz AP 或 P2P 组超过 5 GHz 配对。

时作为组所有者的 Windows Wi-Fi Direct 设备协商连接，Windows 提供首选的通道进行通信。 如果首选的渠道在 5 GHz 范围内，支持仅 2.4 GHz 的设备不能使用该通道。 Windows 将不维护双带宽组并且没有将现有组或 AP 连接移动到 2.4 GHz 的功能。 在这种情况下，打印设备将被发现但配对将始终失败，因为没有通道。

若要防止用户遇到这种情况下，Windows 打印需要打印设备是组所有者。 Windows 作为一种 P2P 网络上的客户端是能够管理双外方案。 因此永远不会没有用户可以发现打印机，但将不能对由于其现有的接入点连接到的情况。

 

 




