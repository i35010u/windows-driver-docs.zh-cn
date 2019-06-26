---
title: 初始化子单元驱动程序并建立引脚连接
description: 初始化子单元驱动程序并建立引脚连接
ms.assetid: 08c7a604-3aa5-4ee0-be55-b58bea0e6df1
keywords:
- Avc.sys 功能驱动程序 WDK，初始化子单元驱动程序
- Avc.sys 功能驱动程序 WDK，pin 连接
- 将固定连接 WDK AV/C
- 连接 WDK AV/C
- 初始化 AV/C 子单元驱动程序
- pin 计数 WDK AV/C
- 格式 WDK AV/C
- 数据格式以 WDK AVStream
- AVCCONNECTINFO
- 外部即插即用连接 WDK AV/C
- KSPIN_DESCRIPTOR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6b606726bc6c909006d3df095ba09a478c83ec9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360681"
---
# <a name="initializing-a-subunit-driver-and-establishing-pin-connections"></a>初始化子单元驱动程序并建立引脚连接


若要初始化的子单元驱动程序并建立 pin 的连接，完成以下过程：

1.  提交[ **AVC\_函数\_获取\_PIN\_计数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-pin-count)请求。 使用此过程中的后续函数中生成的 pin 计数指示 （偏移量范围介于 0 到 PinCount 1） 的 pin。

2.  对于每个插针，提交[ **AVC\_函数\_获取\_PIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-pin-descriptor)请求。 若要完成流式处理 (KS) 筛选器定义内核，使用返回[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)隶属[ **AVC\_PIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_pin_descriptor)结构，它使用传递**AVC\_函数\_获取\_PIN\_描述符**请求。 *Avc.sys*填入**MediumsCount**，**媒介**，**数据流**，并**通信**KSPIN的成员\_描述符。 允许子单元驱动程序复制 KSPIN\_描述符结构并且重写任何成员，但建议它使中型列表保持不变 （该列表可能包含合成为永久子单元即插即用连接的 Guid）.

    指针在 KSPIN 中的\_描述符结构指向保持，直到删除子单元驱动程序的物理设备对象 (PDO) 页面缓冲池。 无法销毁内容，必须格外小心。

    子单元驱动程序允许替换指针; 如果它具有更好，或更好的结构，以指向。 但是，子单元驱动程序必须释放这些内存范围。 如果子单元驱动程序使用 AVStream （而不是 Stream 类），则应使用**KsEdit**例程，以替换此类内存的引用。

    请注意， *Avc.sys* does*不*填写 KSPIN\_描述符的**接口**， **DataRanges**， **类别**，**名称**，或**ConstrainedDataRanges**成员。 子单元驱动程序填充这些成员中，并将**IntersectHandler**和可选**上下文**成员 （在步骤 3 中所述） 如果低筛选器驱动程序， *Avcstrm.sys*，不存在。

    而不考虑的原点**DataRanges**成员，每个标准的范围必须成对出现的重复的范围之内，具有[ **AVCPRECONNECTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avcpreconnectinfo)结构追加 （通过使用适当的说明符 Guid） 以支持设备到计算机*和*设备的连接。 *Avc.sys*可以提供一个 AVCPRECONNECTINFO 结构对于通过每个插针[ **AVC\_函数\_获取\_CONNECTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-connectinfo)请求。

3.  **IntersectHandler**例程创建了**DataFormat**用于匹配成对的结构**DataRanges**结构。 中的结果或者提供交集例程**AVC\_函数\_获取\_PIN\_描述符**或提供的子单元驱动程序。 如果子单元驱动程序提供了自己交集的处理程序，请参阅[ **AV/C 相交处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/nc-avc-pfnavcintersecthandler)。 有关数据交集详细信息，请参阅[AVStream DataRange 结合](data-range-intersections-in-avstream.md)。

    **DataFormat**结构匹配的 AVCPRECONNECTINFO 范围[ **AVCCONNECTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avcconnectinfo)追加到它的结构。 此结构是使用本地固定 AVCPRECONNECTINFO 结构的副本**标志**替换为成员**hPlug**成员。 **HPlug**成员必须保持**NULL**如果**KSPIN\_标志\_AVC\_永久**位设置。 如果**KSPIN\_标志\_AVC\_PCRONLY**或**KSPIN\_标志\_AVC\_FIXEDPCR** 中的设置位**标志**，则**UnitPlugNumber**并**数据流**成员将用于获取**hPlug**处理从*61883。sys*。 任何其他位 （或任何位） 的组合意味着**hPlug**可以获取任何可用的即插即用编号 (通过使用**数据流**成员以确定即插即用方向)。

    **IntersectHandler**例程必须传递到生成的 AVCCONNECTINFO 结构*Avc.sys* （步骤 4 中所述）。 传递 AVCCONNECTINFO 确保*Avc.sys*更高版本进行任何必要的即插即用连接的单位本身 （例如，单元输入或输出插入与子单元目标或源插入之间的连接） 中。

4.  最后，当数据格式 （后格式协商和数据交叉部分） 设置 pin，pin 必须检查 AVCCONNECTINFO 结构的格式。 如果找到此结构，然后 pin 不会移动数据到或从 IEEE 1394 总线或计算机。 相反，它使用[ **AVC\_函数\_设置\_CONNECTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-set-connectinfo) AVCCONNECTINFO 内容发送到较低的驱动程序。 可能的这两个较低的筛选器驱动程序 (例如， *Avcstrm.sys*) 和*Avc.sys*驱动程序执行连接操作，但在此情况下，只有 AVCCONNECTINFO 内容应为缓存的 （没有连接执行的操作）。 较低的驱动程序不会缓存它提供 AVCCONNECTINFO。 这样一来，使得只有一个 pin **hPlug**单位之间的连接。 如果没有较低的筛选器驱动程序，子单元驱动程序应决定是否要将 AVCCONNECTINFO 传递到较低的驱动程序。 *Avc.sys*不需要看到即插即用的 AVCCONNECTINFO 结构控制寄存器 (PCR)-仅连接。

    如果子单元不使用较低的筛选器驱动程序管理 stream 的格式，子单元驱动程序设置了 IEEE 1394 串行总线即插即用连接。 有关详细信息，请参阅[AV/C 流式处理概述](av-c-streaming-overview.md)。

    子单元驱动程序应缓存**hPlug**从格式设置的对等连接，如果成员：

    -   **HPlug**成员与创建的子单元驱动程序不匹配。
    -   **DeviceID**成员不匹配的子单元驱动程序收到 AVCPRECONNECTINFO 中。
    -   **数据流**成员与数据流的子单元的 pin 不匹配。

5.  当要获取 pin 连接资源时，提交[ **AVC\_函数\_ACQUIRE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-acquire)请求。 较低的驱动程序 （或子单元驱动程序本身） 使用任何缓存的 AVCCONNECTINFO 发出**hPlug**连接。 子单元和单元插头之间的内部连接是通过来建立*Avc.sys*后接收**AVC\_函数\_ACQUIRE**请求，请使用缓存的 AVCCONNECTINFO。 *Avc.sys*没有在它没有内部即插即用控件或将连接标记作为永久不缓存信息，也不尝试内部插入连接。

6.  当固定连接资源释放时，提交[ **AVC\_函数\_发行**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-release)请求。 较低的驱动程序和*Avc.sys*保留任何缓存的 AVCCONNECTINFO 以便交替*获取*并*发行*可以执行操作。

7.  提交[ **AVC\_函数\_CLR\_CONNECTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-clr-connectinfo)结构以删除缓存的 AVCCONNECTINFO 数据。

请注意， **AVC\_函数\_设置\_CONNECTINFO**结构必须与 AVCCONNECTINFO 结构数据交集 (本地 AVCCONNECTINFO) 过程中创建一次调用和再一次使用时设置格式 (外 AVCCONNECTINFO) 传递的 AVCCONNECTINFO 结构。 子单元连接不同的设备，筛选器驱动程序之间的连接 (例如， *Avcstrm.sys)* 缓存外信息 (外**hPlug**)，和*Avc.sys*缓存的本地信息。 对于同一设备中的子单元连接之间的连接，筛选器驱动程序不会缓存任何信息，并*Avc.sys*缓存仅外的子单元的信息。 筛选器驱动程序必须通过所有**AVC\_函数\_设置\_CONNECTINFO**请求直至*Avc.sys*，以便从决策制定有关都受防护子单元即插即用连接。

AV/C 连接锁位将设置时在建立连接。 输出插针 （插入源） 公开多个 pin 实例允许覆盖连接 （来自同一输出到一个额外的输入）。 但是，如果允许覆盖连接，执行任何操作将阻止*断开连接*命令从正在删除所有现有连接; 这是固有 AV/C 规范中。 子单元时覆盖连接，发送多个**AVC\_函数\_设置\_CONNECTINFO**并**AVC\_函数\_ACQUIRE**请求对 (而无需干预**AVC\_函数\_发行**请求)。 此外，IEEE 1394 总线引入了第二台计算机或同一台计算机上运行的第二个不兼容应用程序时，会导致此相同的行为。

AV/C 外部即插即用连接不直接受*Avc.sys*，但*Avc.sys*仍可以通过提供建立子单元插入和外部插入之间的内部连接合成AVCCONNECTINFO 结构。 子单元驱动程序可以通过使用创建 AVCCONNECTINFO 结构[ **AVC\_函数\_获取\_UNIQUE\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-unique-id)函数代码填充**DeviceID**成员提供单元地址 0xff 和外部的插入数 （即插即用数字通过使用逻辑 OR 运算符联接与 0x80） **SubunitAddress**并**SubunitPlugNumber**成员和提供正确的数据的流动方向**数据流**成员。 **HPlug**并**UnitPlugNumber**成员应设置为**NULL**。 可以通过检测到数量的输入和输出的外部插头**AVC\_函数\_获取\_EXT\_即插即用\_计数**函数。

方法相*Avc.sys*进行适当内部即插即用连接和公开可能外部即插即用连接到应用程序是让每个可能的外部插件的筛选器工厂。 生成的筛选器实例公开相应的输入或输出插针，进而提供 AVCCONNECTINFO 结构。

 

 




