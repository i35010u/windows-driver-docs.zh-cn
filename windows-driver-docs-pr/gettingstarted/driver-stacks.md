---
title: 驱动程序堆栈
description: 发送到设备驱动程序的大部分请求都打包在 I/O 请求数据包 (IRP) 中。
ms.assetid: 8D55CB83-C50A-48B8-9379-ECF2CF30AEE5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3b4acd32c0824b28c7c45101b6da0c57aedae67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825182"
---
# <a name="driver-stacks"></a>驱动程序堆栈


发送到设备驱动程序的大部分请求都打包在 [I/O 请求数据包](i-o-request-packets.md) (IRP) 中。 每个设备都用设备节点表示，每个设备节点都有一个设备堆栈。 有关详细信息，请参阅[设备节点和设备堆栈](device-nodes-and-device-stacks.md)。 若要将读、写或控制请求发送至某个设备，I/O 管理器会查找设备的设备节点，然后将 IRP 发送至该节点的设备堆栈。 有时，处理 I/O 请求的过程中会涉及到多个设备堆栈。 无论涉及了多少个设备堆栈，参与 I/O 请求的驱动程序整体序列称为请求的“驱动程序堆栈”  。 我们还使用术语“驱动程序堆栈”  来引用特定技术的分层驱动程序组。

## <a name="span-idi_o_requests_that_are_processed_by_several_device_stacksspanspan-idi_o_requests_that_are_processed_by_several_device_stacksspanspan-idi_o_requests_that_are_processed_by_several_device_stacksspanio-requests-that-are-processed-by-several-device-stacks"></a><span id="I_O_requests_that_are_processed_by_several_device_stacks"></span><span id="i_o_requests_that_are_processed_by_several_device_stacks"></span><span id="I_O_REQUESTS_THAT_ARE_PROCESSED_BY_SEVERAL_DEVICE_STACKS"></span>由多个设备堆栈处理的 I/O 请求


在某些情形下，处理 IRP 的过程中会涉及到多个设备堆栈。 下图说明了处理单个 IRP 的过程中涉及到四个设备堆栈的情形。

![一个示意图：其中显示了四个设备节点，每个都有一个设备堆栈](images/chain01.png)

以下是图中的每个编号阶段 IRP 的处理方式：

1.  IRP 由 Disk.sys 创建，Disk.sys 是“我的 USB 存储设备”节点的设备堆栈中的函数驱动程序。 Disk.sys 将 IRP 沿着设备堆栈向下传递到 Usbstor.sys。

2.  注意，Usbstor.sys 为“我的 USB 存储设备”节点的 PDO 驱动程序，为“USB 大容量存储设备”节点的 FDO 驱动程序。 此时，决定 IRP 由（PDO、Usbstor.sys）对所有还是由（FDO、Usbstor.sys）对所有并不重要。 IRP 由驱动程序 Usbstor.sys 所有，并且该驱动程序可以访问 PDO 和 FDO。
3.  当 Usbstor.sys 完成处理 IRP 后，它会将 IRP 传递到 Usbhub.sys。 Usbhub.sys 为“USB 大容量存储设备”节点的 PDO 驱动程序，为“USB 根集线器”节点的 FDO 驱动程序。 决定 IRP 由（PDO、Usbhub.sys）对所有还是由（FDO、Usbhub.sys）对所有并不重要。 IRP 由驱动程序 Usbhub.sys 所有，并且该驱动程序可以访问 PDO 和 FDO。

4.  当 Usbhub.sys 完成处理 IRP 后，它会将 IRP 传递到（Usbuhci.sys、Usbport.sys）对。

    Usbuhci.sys 为微型端口驱动程序，Usbport.sys 为端口驱动程序。 （微型端口、端口）对扮演单个驱动程序的角色。 在此情形下，微型端口驱动程序和端口驱动程序都由 Microsoft 编写。 （Usbuhci.sys、Usbport.sys）对为“USB 根集线器”节点的 PDO 驱动程序，（Usbuhci.sys、Usbport.sys）对也为“USB 主控制器”节点的 FDO 驱动程序。 （Usbuhci.sys、Usbport.sys）对执行与主控制器硬件的实际通信，该硬件反过来与物理 USB 存储设备通信。

## <a name="span-idthe_driver_stack_for_an_i_o_requestspanspan-idthe_driver_stack_for_an_i_o_requestspanspan-idthe_driver_stack_for_an_i_o_requestspanthe-driver-stack-for-an-io-request"></a><span id="The_driver_stack_for_an_I_O_request"></span><span id="the_driver_stack_for_an_i_o_request"></span><span id="THE_DRIVER_STACK_FOR_AN_I_O_REQUEST"></span>I/O 请求的驱动程序堆栈


考虑参与上图中所说明 I/O 请求的四个驱动程序的序列。 我们可以通过关注驱动程序而非设备节点及其单个设备堆栈来获取该序列的其他视图。 下图采用从上到下的顺序说明驱动程序。 注意，Disk.sys 与一个设备对象关联，但其他三个驱动程序中的每个都与两个设备对象关联。

![驱动程序堆栈的示意图，其中显示了仅与 fdo 关联的顶部驱动程序，以及与 pdo 和 fdo 关联的其他三个驱动程序](images/driverstack01.png)

参与 I/O 请求的驱动程序的序列称为 *I/O 请求的驱动程序堆栈*。 若要说明 I/O 请求的驱动程序堆栈，我们按照驱动程序参与请求的次序从上到下画驱动程序。

注意，I/O 请求的驱动程序堆栈与设备节点的设备堆栈完全不同。 还注意，I/O 请求的驱动程序堆栈不必要留在设备树的某一分支中。

## <a name="span-idtechnology_driver_stacksspanspan-idtechnology_driver_stacksspanspan-idtechnology_driver_stacksspantechnology-driver-stacks"></a><span id="Technology_driver_stacks"></span><span id="technology_driver_stacks"></span><span id="TECHNOLOGY_DRIVER_STACKS"></span>技术驱动程序堆栈


考虑上图中显示的 I/O 请求的驱动程序堆栈。 如果我们为每个驱动程序提供友好名称并对该图做一些细小更改，则会有一个框图与 Windows 驱动程序工具包 (WDK) 文档中出现的多个框图类似。

![驱动程序堆栈的示意图，其中显示了驱动程序的友好名称：顶部为“磁盘类驱动程序”，接着是“USB 存储端口驱动程序”，然后是“USB 集线器驱动程序”和（USB 2 微型端口、USB 端口）驱动程序](images/driverstack02.png)

在该示意图中，驱动程序堆栈分为三个部分。 我们可以将每个部分都视为属于特定技术或属于操作系统的特定组件或一部分。 例如，我们可以说，驱动程序堆栈顶部的第一个部分属于卷管理器，第二个部分属于操作系统的存储组件，第三个部分属于操作系统的核心 USB 部分。

考虑第三个部分中的驱动程序。 这些驱动程序为一组较大的核心 USB 驱动程序的子集，Microsoft 提供这些驱动程序用于处理各种 USB 请求和 USB 硬件。 下图显示了整个 USB 核心框图的外观。

![一个示意图，其中显示了可能的 USB 核心框的技术驱动程序堆栈 ](images/technologystack01.png)

显示特定技术或操作系统的特定组件或一部分的所有驱动程序的框图称为“技术驱动程序堆栈”  。 通常，会为技术驱动程序堆栈命名，如 USB 核心驱动程序堆栈、存储堆栈、1394 驱动程序堆栈以及音频驱动程序堆栈。

**注意**  本主题中的 USB 核心框图显示了说明 USB 1.0 和 2.0 技术驱动程序堆栈的几种可能方法之一。 有关 USB 1.0、2.0 以及 3.0 驱动程序堆栈的正式图，请参阅 [USB 驱动程序堆栈体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设备节点和设备堆栈](device-nodes-and-device-stacks.md)

[微型驱动程序和驱动程序对](minidrivers-and-driver-pairs.md)

[适用于所有驱动程序开发人员的概念](concepts-and-knowledge-for-all-driver-developers.md)

 

 






