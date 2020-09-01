---
title: 初始化子单元驱动程序并建立引脚连接
description: 初始化子单元驱动程序并建立引脚连接
ms.assetid: 08c7a604-3aa5-4ee0-be55-b58bea0e6df1
keywords:
- Avc.sys 函数驱动程序 WDK，初始化子单位驱动程序
- Avc.sys 函数驱动程序 WDK，pin 连接
- 固定连接 WDK AV/C
- 连接 WDK AV/C
- 正在初始化 AV/C 子单位驱动程序
- pin 计数 WDK AV/C
- 格式化 WDK AV/C
- 数据格式 WDK AVStream
- AVCCONNECTINFO
- 外部插头连接 WDK AV/C
- KSPIN_DESCRIPTOR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 382de871bafaadf3495cd92e2698eeb268ec3a54
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189765"
---
# <a name="initializing-a-subunit-driver-and-establishing-pin-connections"></a>初始化子单元驱动程序并建立引脚连接


若要初始化子单位驱动程序并建立 pin 连接，请完成以下过程：

1.  提交 [**AVC \_ 函数 \_ 获取 \_ PIN \_ 计数**](./avc-function-get-pin-count.md) 请求。 在此过程的后续函数中使用生成的 pin 计数，以指示 (偏移量范围为0到 PinCount-1) 的固定偏移量。

2.  对于每个 pin，请提交 [**AVC \_ 函数 \_ 获取 \_ pin \_ 描述符**](./avc-function-get-pin-descriptor.md) 请求。 若要完成内核流式处理 (KS) 筛选器的定义，请使用随**AVC \_ 函数 \_ 获取 \_ pin \_ 描述符**请求一起传递的[**AVC \_ PIN \_ 描述符**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_descriptor)结构返回的[**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)成员。 *Avc.sys* 填充 KSPIN 描述符的 **MediumsCount**、 **媒体**、 **数据流**和 **通信** 成员 \_ 。 允许使用子单位驱动程序复制 KSPIN \_ 描述符结构并覆盖任何成员，但建议将中间列表保持不变 (该列表可能包含合成) 的永久次级子连接的 guid。

    KSPIN 描述符结构中的指针 \_ 指向的页面缓冲池，直到删除了子实体驱动程序的物理设备对象 (PDO) 。 必须小心不要销毁内容。

    如果要指向，则允许使用子单位驱动程序替换该指针。 但是，子单位驱动程序不得释放这些内存范围。 如果子单位驱动程序使用 AVStream (而不是 Stream 类) ，则它应使用 **KsEdit** 例程来替换此类内存引用。

    请注意*Avc.sys* ，Avc.sys*不会填写 KSPIN* \_ 描述符的**接口**、 **DataRanges**、 **Category**、 **Name**或**ConstrainedDataRanges**成员。 子单元驱动程序将填充这些成员，以及 **IntersectHandler** 和可选的 **上下文** 成员 (在步骤3中所述) 如果较低筛选器驱动程序 *Avcstrm.sys*不存在。

    无论 **DataRanges** 成员的来源是什么，每个标准范围必须与具有 [**AVCPRECONNECTINFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo) 结构追加 (的重复范围成对使用) 以支持设备到计算机 *和* 设备到设备的连接。 *Avc.sys* 可以通过 [**AVC \_ 函数 \_ GET \_ CONNECTINFO**](./avc-function-get-connectinfo.md) 请求为每个 pin 提供 AVCPRECONNECTINFO 结构。

3.  **IntersectHandler**例程为匹配的**DataRanges**结构对创建**DataFormat**结构。 交集例程是在 **AVC \_ 函数 \_ 获取 \_ PIN \_ 描述符** 的结果中提供的，也可以由子单位驱动程序提供。 如果子单位驱动程序提供其自己的交集处理程序，请参阅 [**AV/C 交集处理程序**](/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)。 有关数据交集的详细信息，请参阅 [AVStream 中的 DataRange 交集](data-range-intersections-in-avstream.md)。

    匹配 AVCPRECONNECTINFO 范围的 **DataFormat** 结构附加了一个 [**AVCCONNECTINFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo) 结构。 此结构是本地 pin 的 AVCPRECONNECTINFO 结构的副本， **标志** 成员替换为 **hPlug** 成员。 如果已设置**KSPIN \_ 标志 \_ AVC \_ 永久**位，则**hPlug**成员必须保留**为 NULL** 。 如果在**Flags**中设置了**KSPIN \_ 标志 \_ AVC \_ PCRONLY**或**KSPIN \_ 标志 \_ AVC \_ FIXEDPCR** ，则将使用**UnitPlugNumber**和**数据流**成员从*61883.sys*获取**hPlug**句柄。 任何其他位数 (或没有任何位的组合) 意味着可以通过使用**数据流**成员确定) 的即插方向，为任何可用的插件 (获取**hPlug** 。

    **IntersectHandler**例程必须将生成的 AVCCONNECTINFO 结构向下传递到步骤 4) 中所述*Avc.sys* (。 通过传递 AVCCONNECTINFO，可以确保 *Avc.sys* 稍后可以在单元本身中进行任何必需的连接 (例如，通过次级目标或源插头) 的单元输入或输出插头之间的连接。

4.  最后，当在格式协商和数据交集) 之后，在 pin (上设置数据格式时，pin 必须检查 AVCCONNECTINFO 结构的格式。 如果找到此结构，则不会将数据从或从 IEEE 1394 总线移入或移出到计算机。 相反，它使用 [**AVC \_ 函数 \_ SET \_ CONNECTINFO**](./avc-function-set-connectinfo.md) 将 AVCCONNECTINFO 内容发送到较低的驱动程序。  (例如， *Avcstrm.sys*) 和 *Avc.sys* 驱动程序执行连接操作，则这可能会导致较低的筛选器驱动程序，但此时只应缓存 AVCCONNECTINFO 内容， (未执行任何连接操作) 。 低级驱动程序不会缓存它提供的 AVCCONNECTINFO。 这样一来，每个单位之间就只能有一个 pin **hPlug** 连接。 如果没有低筛选器驱动程序，则子单位驱动程序应决定是否将 AVCCONNECTINFO 传递到较低的驱动程序。 *Avc.sys* 无需查看插件控制寄存器的 AVCCONNECTINFO 结构 (PCR) 仅连接。

    如果子单位不使用较低筛选器驱动程序来管理流格式，则子单位驱动程序将设置 IEEE 1394 串行总线插入连接。 有关详细信息，请参阅 [AV/C 流式处理概述](av-c-streaming-overview.md)。

    如果出现以下情况，子源驱动程序应缓存格式的 **hPlug** 成员以设置对等连接：

    -   **HPlug**成员与由子单位驱动程序创建的成员不匹配。
    -   **DeviceID**成员与在 AVCPRECONNECTINFO 中接收的子单元驱动程序不匹配。
    -   **数据流**成员与子单位的 pin 的数据流不匹配。

5.  当要获取 pin 连接资源时，请提交 [**AVC \_ FUNCTION \_ 获取**](./avc-function-acquire.md) 请求。 较低版本的驱动程序 (或子单位驱动程序本身) 使用任何缓存的 AVCCONNECTINFO 建立 **hPlug** 连接。 使用缓存的 AVCCONNECTINFO *Avc.sys* 接收到 **AVC \_ 函数 \_ 获取** 请求后，次级和 unit 插头之间的内部连接。 *Avc.sys* 不会缓存信息，也不会尝试内部插入连接（如果它没有内部插件控制）或连接被标记为永久。

6.  在要释放 pin 连接资源时，请提交 [**AVC \_ FUNCTION \_ RELEASE**](./avc-function-release.md) 请求。 更低的驱动程序和 *Avc.sys* 保留任何缓存的 AVCCONNECTINFO，以便可以执行交替 *获取* 和 *释放* 操作。

7.  提交 [**AVC \_ 函数 \_ CLR \_ CONNECTINFO**](./avc-function-clr-connectinfo.md) 结构以删除缓存的 AVCCONNECTINFO 数据。

请注意，必须将 **AVC \_ 函数 \_ 集 \_ CONNECTINFO** 结构与 (本地 AVCCONNECTINFO) 的数据交集创建的 AVCCONNECTINFO 结构一一次调用，并再次与 (外部 AVCCONNECTINFO) 设置格式时传递的 AVCCONNECTINFO 结构一起调用。 对于不同设备的子单元连接之间的连接，筛选器驱动程序 (例如 *Avcstrm.sys) * 将外部信息缓存 (外部 **hPlug**) ，并 *Avc.sys* 缓存本地信息。 对于同一设备中子单元连接之间的连接，筛选器驱动程序不会缓存任何信息， *Avc.sys* 仅缓存外部子单位的信息。 筛选器驱动程序必须 **将所有 AVC \_ 函数 \_ 集 \_ CONNECTINFO** 请求向下传递到 *Avc.sys*，以便将其与有关子组插入连接的决策进行防护。

AV/C 连接锁定位是在建立连接时设置的。 输出插针 (源插头) 公开多个 pin 实例，允许 (从同一输出到其他输入) 的重叠连接。 但是，如果允许重叠连接，则不会阻止 *断开* 连接命令删除所有现有连接;这在 AV/C 规范中是固有的。 重叠连接时，子组会发送多个 **AVC \_ 函数 \_ SET \_ CONNECTINFO** 和 **AVC \_ 函数 \_ 获取** 请求对 (，而不会将 **AVC \_ 函数 \_ RELEASE** 请求) 。 此外，如果将第二台计算机引入到 IEEE 1394 总线，或在同一台计算机上运行另一个不兼容的应用程序，则可能会出现这种情况。

*Avc.sys*不直接支持 AV/C 外插连接，但*Avc.sys*仍可通过提供合成 AVCCONNECTINFO 结构，在子单位插头与外部插头之间建立内部连接。 子单位驱动程序可以通过使用[**AVC \_ 函数 \_ GET \_ UNIQUE \_ ID**](./avc-function-get-unique-id.md)函数代码来创建 AVCCONNECTINFO 结构，以便通过使用逻辑 OR) 运算符和**SubunitAddress**和**SubunitPlugNumber**成员，并在**数据流**成员中提供正确的数据流方向，来填充**DeviceID**成员、提供单元地址0xff 和外部插头号 (插件号。 **HPlug**和**UnitPlugNumber**成员应设置为**NULL**。 可以通过 **AVC \_ 函数 \_ GET \_ EXT \_ \_ ** number 函数来检测输入和输出外部插头的数目。

一种允许 *Avc.sys* 建立正确的内部连接，并向应用程序公开可能的外部连接的方法是为每个可能的外部插件提供筛选器工厂。 生成的筛选器实例将公开适当的输入插针和输出插针，进而提供 AVCCONNECTINFO 结构。

 

