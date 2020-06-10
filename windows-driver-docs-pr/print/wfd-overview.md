---
title: Wi-fi 直接打印概述
description: 提供有关支持的用户体验和 Wi-fi 直接打印用例的信息。
ms.assetid: 40ED3410-EC46-42C8-B09B-8010639F2268
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5901d2857b858d3d1ae6daa35de47b3ceb97b12a
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638451"
---
# <a name="wi-fi-direct-printing-overview"></a>Wi-fi 直接打印概述

## <a name="supported-user-experiences"></a>支持的用户体验

**与 Windows 中的 Wi-fi Direct 打印机配对**

与海外合作伙伴见面时，企业主管会接收到合同的修订，并且必须打印更新的副本后才能进行会议。

它们在支持 Wi-fi Direct 的合作伙伴办公室找到 Windows 认证的打印设备。 它们会在设备与其 Windows 表面之间发起配对，并快速建立与设备的连接，并已准备好打印。 它们打印文档的多个副本，并能够向合作伙伴提供新的批准合同。

几个小时后，它们就会到机场。现有签名合同。

此方案描述：

使用 PIN 配对

- 在控制面板中选择设备后，系统会提示用户输入连接 PIN。 它们输入由接待员提供给他们的 PIN 号。 连接已完成，并且已准备好打印。

使用即席 PIN 配对

- 在控制面板中选择设备后，设备的控制面板会要求用户输入 PIN，该 PIN 将与设备在设备上输入的 PIN 匹配（就像蓝牙配对一样）。 它们在设备的控制面板上输入 PIN，然后在计算机上的提示中输入相同的数字。 连接已完成，并且已准备好打印。

**打印到以前配对的 Wi-fi Direct 打印机**

当用户在家时，其他用户只使用其移动宽带连接在其 Windows 电脑上获得 Internet 连接。 他们拥有 Wi-fi Direct 打印设备，它们之前已配对并安装在其 Windows 电脑上。

他们正在在家中处理文档，需要打印硬副本。 它们在应用程序中选择 "打印"。 其 Wi-fi Direct 打印机始终通过 Wi-fi Direct 广播，它们目前处于范围内。 显示 "打印" 对话框时，其 Wi-fi Direct 打印机显示为 "联机"。 它们选择该设备，然后单击 "打印"。 其 Windows PC 建立与设备的连接，并发送打印作业。 在这些设备上，Wi-fi Direct 打印机看起来像是通过网络或直接连接方式使用的任何其他打印机。 打印作业输出，并可继续编辑。

## <a name="use-cases"></a>用例

**打印机-首次配对**

通过新式设备手动连接到 WI-FI DIRECT 打印设备控制面板

Preconditions

- 用户处于 Wi-fi Direct 打印设备范围内

- Wi-fi Direct 打印设备的驱动程序位于用户的设备上

- Wi-fi Direct 打印设备符合 Windows 认证要求

触发器

用户类型在 Windows "开始" 屏幕中的 "添加打印机" 中，选择 "设置"，然后启动 "设备" 控制面板。

步骤

1. 设备控制面板搜索可用打印设备

1. DAF 为 Wi-fi Direct （WFD）设备发出 L2 质询

1. 可用 WFD 打印设备在 "设备" 列表中显示为 "用户" 选项

1. 用户单击 WFD 打印设备

1. DAF 使 L2/L3 连接到 WFD 设备，并通过 WSD 提供程序触发垂直配对。 已为设备和驱动程序配置了队列。

1. WFD 提供程序与设备断开连接

Postconditions

- 已建立 Wi-fi Direct 打印机的打印队列

- 每当 WFD L2 信标质询成功时，打印队列都将显示为 "可用"

备用流

空值

注意事项

空值

通过添加打印机向导手动连接到 WI-FI DIRECT 打印设备

Preconditions

- 用户处于 Wi-fi Direct 打印设备范围内

- Wi-fi Direct 打印设备的驱动程序位于用户的设备上

- Wi-fi Direct 打印设备符合 Windows 认证要求

触发器

用户打开经典控制面板，并启动设备和打印机控制面板。

步骤

1. 用户启动设备和打印机控制面板

1. 用户单击 "添加设备"

1. DAF 为 Wi-fi Direct （WFD）设备发出 L2 质询

1. 可用 WFD 打印设备在 "设备" 列表中显示为 "用户" 选项

1. 用户单击 WFD 打印设备

1. DAF 使 L2/L3 连接到 WFD 设备，并通过 WSD 提供程序触发垂直配对。 已为设备和驱动程序配置了队列。

1. WFD 提供程序与设备断开连接

Postconditions

- 已建立 Wi-fi Direct 打印机的打印队列

- 每当 WFD L2 信标质询成功时，打印队列都将显示为 "可用"

备用流

空值

注意事项

空值

连接打印设备时出错

Preconditions

用户使用以下操作启动配对：

- 新式设备控制面板，如上面的 "通过新式设备手动连接到 WI-FI DIRECT 打印设备" 中所述

- 设备和打印机控制面板，如上面的 "通过添加打印机向导手动连接到 WI-FI DIRECT 打印设备" 中所述

触发器

在配对/队列设置期间发生故障事件。

步骤

1. 将删除部分设置的打印队列。

1. 用户收到故障通知。

Postconditions

- 用户的打印系统在配对尝试之前返回到其状态

备用流

- 如果错误是由于缺少驱动程序而导致的，并且可以下载或添加驱动程序（在非按流量计费的连接上，x86 或 amd64），则系统会提示用户执行此操作，并重新尝试配对。

注意事项

空值

使用所需的 PIN 连接到 WI-FI DIRECT 打印设备

Preconditions

用户使用以下操作启动配对：

- 新式设备控制面板，如上面的 "通过新式设备手动连接到 WI-FI DIRECT 打印设备" 中所述

- 设备和打印机控制面板，如上面的 "通过添加打印机向导手动连接到 WI-FI DIRECT 打印设备" 中所述

触发器

设备需要 PIN 才能配对

步骤

1. 用户已收到打印设备所需的 PIN

1. 在 WSD 安装期间，系统会提示用户输入 PIN

1. 用户输入 PIN 和配对完成

Postconditions

- 正确设置了打印队列

备用流

- 如果错误是由于缺少驱动程序而导致的，并且可以下载或添加驱动程序（在非按流量计费的连接上，x86 或 amd64），则系统会提示用户执行此操作，并重新尝试配对。

注意事项

- 即席 PIN

    1. 用户需要在打印机和设备上输入 PIN，这一点与蓝牙配对类似。

    1. 在 WSD 设置期间，用户会在出现提示时在设备和客户端 PC 上输入正确的 PIN。

    1. 用户输入 PIN 码并完成配对。

- PIN 输入失败

    1. 用户已收到客户端 PIN 或需要即席 PIN。

    1. 在 WFD 安装期间，系统会提示用户输入 PIN。

    1. 用户输入的 PIN 不正确。

    1. 用户通知 PIN 不正确且配对无法完成。

    1. 发现被终止。 未设置任何队列。

后**置条件**：没有设置打印队列。

**打印**

从应用程序使用 WI-FI DIRECT 打印设备

Preconditions

- 用户处于 Wi-fi Direct 打印设备范围内

- 用户已成功完成与 Wi-fi Direct 打印设备的首次配对，如上面的 "打印机首次配对" 中所述。

触发器

用户尝试从应用程序打印

步骤

1. DAF 为 Wi-fi Direct （WFD）设备发出 L2 质询。

1. 对 L2 质询作出响应的已知 WFD 打印设备显示为 "可用"

1. 用户选择 WFD 打印设备，并单击 "打印"

1. DAF 使 L2/L3 连接与用户选择的 WFD 设备建立连接，并建立 L3 WSD 连接。 设备的引用计数增加。

1. 打印作业已进行后台处理、呈现并发送到设备

1. 设备的引用计数递减。 如果减量后的引用计数等于0，则连接将关闭。

Postconditions

- 打印作业已成功发送到打印设备。

备用流

空值

注意事项

- 在 Windows PC 上，队列的保留方式与所有其他打印队列的方式相同。 用户应能够重新连接和打印到设备，而不考虑配对和后续使用之间的时间。 只有当打印机已修剪了连接信息并且用户的配对信息已被删除时，用户才有必要重新配对才能进行打印。 应将重配对降到最低，以提供更好的用户体验。 这意味着，设备必须在内存中保留一定数量的配对，以便为预期用途而维护。 例如，家里使用的打印机可能会保留10-25 配对。 适用于办公室的打印机可能会维护得更多。

## <a name="considerations-for-pairing"></a>配对注意事项

**永久性组**

Windows 预期在为 Wi-fi Direct 打印设备创建打印队列后，Windows 客户端将能够重新连接到该设备，而无需重新配对。 用于 Wi-fi Direct 的 DAF 提供程序将在创建队列和设备后关闭该连接。 因此，配对信息必须保留，以使用户在打印时与设备重新连接。

如果在每次连接后将配对信息放在设备端，则用户将永远无法打印到设备。 用户将进入一个循环，用户在电脑设置中添加设备，在安装后关闭连接，并删除配对，要求用户再次将设备添加到电脑设置。

**并发连接数**

应该打印设备能够响应多台 PC 连接请求。 因此，打印设备应该实现与多个组的并发连接才能实现此方案。

**删除配对**

Windows 要求使用 Wi-fi Direct 设备来维护配对信息，使用户无需重新预配即可打印到 Wi-fi Direct 队列。 但是，我们了解到设备可存储的配对数量有限。 强烈建议设备有足够的内存来维护合理的目标使用连接数。 例如，适用于家庭或小型办公室的设备可能会记住30个连接。 但是，旨在广泛使用和在公共环境中重复使用的设备可能需要记住更多的用户，以确保不会过于频繁地修剪连接。

**删除配对方案**：在用户提交打印作业之前，Windows 不会重新建立与 wi-fi Direct 设备的完全连接。 因此，如果设备已删除 Windows 电脑的配对信息，则在打印作业已排入队列之前，Windows 将不知道这一点。 **但是，用户可以重新设置连接并与设备重新配对，但这样做会导致打印队列被删除并重新生成，并且任何排队的打印作业都将在该过程中丢失。** 通过在内存中维护适当数量的配对，设备可以最大程度地减少用户必须重新配对并重新提交其打印作业的实例数。

**适用于 PC 的 wi-fi 驱动程序注意事项**

Windows 8 Wi-fi 模块的徽标要求需要模块支持 Wi-fi Direct。 但是，还必须在为模块提供的驱动程序中支持此功能。 Windows 8 中的大部分收件箱驱动程序不支持 Wi-fi Direct，即使模块能够这样做也是如此。 这些模块的制造商已经更新了驱动程序站点中提供的驱动程序。 在下一个 Windows 版本后，更新的驱动程序将更广泛地提供。

**Windows 8 徽标 WI-FI 模块**：下表提供了针对 Windows 8 的徽标提交的 wi-fi direct 模块的非详尽列表。 此信息在保密协议下共享，不会以任何形式重新分发。 提供数据是为了帮助合作伙伴识别应使用 Wi-fi Direct 的 Wi-fi 模块。 如**6.2.4**中所述，这些设备的收件箱驱动程序可能不支持 wi-fi Direct，需要先下载并安装更新的驱动程序，然后才能进行测试。

Windows RT

Broadcom 802.11 abgn 无线 SDIO 适配器 Marvell AVASTAR Wireless-n 网络控制器（SDIO） Windows 8 （64位）

Atheros 无线网络适配器 Broadcom 802.11 ac 无线网络适配器 Broadcom 802.11 ac 无线 USB 适配器 Broadcom 802.11 n 双频网络无线适配器 Broadcom 802.11 n 网络适配器 Broadcom 802.11 n 无线网络适配器 Intel （R） Centrino （R） Advanced-n + WiMAX 6150 Intel （r） centrino （r） advanced-n + wimax 6250 intel （r） centrino （r） advanced-n 6200 intel （r）迅驰（r） advanced-n 6205 intel （r） centrino （r） advanced-n 6235 intel （r）迅驰（r） ultimate-n 6300 intel （r）6300（R） Centrino （R） Wireless-n 105 Intel （r） centrino （r） wireless-n 135 Intel （r） centrino （r） wireless-n 2200 Intel （R）迅驰（r） wireless-n 2230 Killer 无线 N Marvell AVASTAR 350N 无线网络控制器 N150MA N300MA Qualcomm Atheros 无线网络适配器 Realtek 8812AU 无线 LAN 802.11 ac USB NIC Realtek RTL8188CE 无线 LAN 802.11 N PCI-E NIC Realtek RTL8188CU/RTL8191CU/RTL8192CU/RTL8188RU 无线 LAN 802.11 n USB 2.0 网络适配器 Realtek RTL8188E 无线 LAN 802.11 n PCI E NIC Realtek RTL8188EE 无线 LAN 802.11 n PCI-E nic realtek RTL8723A2.0 网络适配器 Realtek RTL8723AE 无线 LAN 802.11 n PCI-E NIC Realtek 无线 LAN 802.11 n USB 2.0 网络适配器 WNA3100M Windows 8 （32位）

Atheros 无线网络适配器 Broadcom 11ac 网络无线适配器 Broadcom 802.11 abgn 无线 LAN SDIO 适配器 Broadcom 802.11 abgn 无线 SDIO 适配器 Broadcom 802.11 ac 无线网络适配器 Broadcom 802.11 ac 无线 USB 适配器 Broadcom 802.11 n 双频网络无线适配器 Broadcom 802.11 n 网络适配器 Broadcom 802.11 n 无线网络适配器 Intel （R）迅驰（R）高级-N + WiMAX 6150 Intel （R）迅驰（R）高级-N + WiMAX 6250 Intel （R） Centrino （R） Advanced-n 6200 Intel （r）迅驰（r） advanced-n 6205 Intel （R） Centrino （R）高级-N 6235 （R）旗舰 6300 Intel （R）迅驰（r）旗舰版 6300 AGN Intel （R） Centrino （R） Wireless-n 105 Intel （R） Centrino （R） Wireless-n 135 Intel （R） Centrino （R） wireless-n 2200 Intel （r） centrino （R） Wireless-n 2230 Killer 无线 N Marvell AVASTAR 350N 无线网络控制器 N150MA N300MA Qualcomm Atheros 无线网络适配器 Realtek 8812AU 无线 LAN 802.11 ac USB NIC Realtek RTL8188CE 无线 LAN 802.11 N PCI-E NIC Realtek RTL8188CU/RTL8191CU/RTL8192CU/RTL8188RU 无线 LAN 802.11 N USB 2.0 网络适配器 Realtek RTL8188E 无线 LAN802.11 n PCI-E NIC Realtek RTL8188EE 无线 LAN 802.11 n PCI-E NIC Realtek RTL8723A 无线 LAN 802.11 n USB 2.0 网络适配器 Realtek RTL8723AE 无线 LAN 802.11 n PCI-E NIC Realtek 无线 LAN 802.11 n USB 2.0 网络适配器 WNA3100M

**Windows 中的设备名称**

当设备是组所有者时，windows 使用 Wi-fi P2P IE 格式的 P2P 设备信息子元素的设备名称属性在 Windows 中设置设备名称。 此属性应包含用户的有意义的名称，因为它将在所有 Windows UI 中显示为设备名称。

![p2p ie 格式 oob 设备信息元素](images/wfd-p2pieformat.png)

*P2P IE 格式 OOB 设备信息元素*

**组所有权**

打印设备必须始终为组所有者。 Windows 打印系统不支持 Windows PC 是组所有者的方案。

有关组所有权和 5 GHz 网络的已知问题。 如果 PC 是组的所有者，并且它已连接到 5 ghz AP 或超过 5 GHz 的 P2P 组，则 Windows 不支持与使用 2.4 GHz 通道的设备配对。

当 Windows 作为组所有者与 Wi-fi Direct 设备协商连接时，Windows 将提供首选的通信通道。 如果首选通道处于 5 GHz 范围内，则仅支持 2.4 GHz 的设备将无法使用该通道。 Windows 不会维护双带宽组，也不能将现有组或接入点连接到 2.4 GHz。 在这种情况下，将发现打印设备，但配对始终会失败，因为无法建立通道。

若要防止用户遇到此情况，Windows 打印要求将打印设备作为组所有者。 Windows 作为 P2P 网络上的客户端能够管理双频方案。 这种情况下，用户可能会发现打印机，但由于其现有的 AP 连接而无法配对。
