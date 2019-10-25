---
title: 初始化子单元驱动程序并建立引脚连接
description: 初始化子单元驱动程序并建立引脚连接
ms.assetid: 08c7a604-3aa5-4ee0-be55-b58bea0e6df1
keywords:
- Avc 函数驱动程序 WDK，初始化子单位驱动程序
- Avc 函数驱动程序 WDK，pin 连接
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
ms.openlocfilehash: f6a72d381977d6c073bf408a5118fa8402fe8f8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845572"
---
# <a name="initializing-a-subunit-driver-and-establishing-pin-connections"></a>初始化子单元驱动程序并建立引脚连接


若要初始化子单位驱动程序并建立 pin 连接，请完成以下过程：

1.  提交[**AVC\_函数\_获取\_PIN\_计数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-pin-count)请求。 在此过程的后续函数中使用生成的 pin 计数来指示 pin （介于0到 PinCount-1 之间的偏移量）。

2.  对于每个 pin，请提交[**AVC\_函数\_获取\_pin\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-pin-descriptor)请求。 若要完成内核流式处理（KS）筛选器的定义，请使用与 AVC\_函数一起传递的[**AVC\_PIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_descriptor)结构的返回的[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)成员\_**GET\_PIN 请求\_** 。 *Avc*在**MediumsCount**、**媒体**、**数据流**和 KSPIN\_描述符的**通信**成员中填充。 允许使用次级驱动程序复制 KSPIN\_描述符结构并覆盖任何成员，但建议将中间列表保持不变（此列表可能包含合成到永久性子组插入连接的 Guid）。

    \_KSPIN 中的指针将指向保留的分页池，直到删除了子实体驱动程序的物理设备对象（PDO）。 必须小心不要销毁内容。

    如果要指向，则允许使用子单位驱动程序替换该指针。 但是，子单位驱动程序不得释放这些内存范围。 如果子单位驱动程序使用 AVStream （而不是 Stream 类），则它应使用**KsEdit**例程来替换此类内存引用。

    请注意， *Avc* *不*会填写 KSPIN\_描述符的**接口**、 **DataRanges**、 **Category**、 **Name**或**ConstrainedDataRanges**成员。 如果低级筛选器驱动程序（ *Avcstrm*）不存在，则子单元驱动程序将填充这些成员以及**IntersectHandler**和可选的**上下文**成员（如步骤3中所述）。

    无论**DataRanges**成员的来源是什么，每个标准范围必须与具有[**AVCPRECONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)结构追加的重复范围成对出现（使用适当的说明符 guid）以支持设备到计算机*和*设备到设备的连接。 *Avc*可以通过[**Avc\_函数\_获取\_CONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-connectinfo)请求来为每个 pin 提供 AVCPRECONNECTINFO 结构。

3.  **IntersectHandler**例程为匹配的**DataRanges**结构对创建**DataFormat**结构。 交集例程在 AVC\_函数的结果中提供， **\_获取\_PIN\_描述符**或由子单位驱动程序提供。 如果子单位驱动程序提供其自己的交集处理程序，请参阅[**AV/C 交集处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)。 有关数据交集的详细信息，请参阅[AVStream 中的 DataRange 交集](data-range-intersections-in-avstream.md)。

    匹配 AVCPRECONNECTINFO 范围的**DataFormat**结构附加了一个[**AVCCONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)结构。 此结构是本地 pin 的 AVCPRECONNECTINFO 结构的副本，**标志**成员替换为**hPlug**成员。 如果已设置**KSPIN\_标志\_AVC\_永久**位，则**hPlug**成员必须保留**为 NULL** 。 如果**KSPIN\_标志\_AVC\_PCRONLY**或**KSPIN\_标志\_AVC\_** FIXEDPCR bits 是在**Flags**中设置的，则**UnitPlugNumber**和**数据流**成员将用于获取*61883*中的**hPlug**句柄。 任何其他位（或不是位）组合意味着可以获得任何可用插件的**hPlug** （通过使用**数据流**成员确定插入方向）。

    **IntersectHandler**例程必须将生成的 AVCCONNECTINFO 结构向下传递到*Avc* （如步骤4中所述）。 通过传递 AVCCONNECTINFO，可确保*Avc*稍后可以在单元本身中进行任何必需的连接（例如，单位输入或输出插头之间的连接与子源目标或源插头）。

4.  最后，当数据格式设置在 pin 上（在格式协商和数据交集之后）时，pin 必须检查 AVCCONNECTINFO 结构的格式。 如果找到此结构，则不会将数据从或从 IEEE 1394 总线移入或移出到计算机。 相反，它使用[**AVC\_函数\_设置\_CONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-set-connectinfo)将 AVCCONNECTINFO 内容发送到较低的驱动程序。 这两个筛选器驱动程序（例如， *Avcstrm*）和*Avc*驱动程序都可能执行连接操作，但此时，只应缓存 AVCCONNECTINFO 内容（未执行任何连接操作）。 低级驱动程序不会缓存它提供的 AVCCONNECTINFO。 这样一来，每个单位之间就只能有一个 pin **hPlug**连接。 如果没有低筛选器驱动程序，则子单位驱动程序应决定是否将 AVCCONNECTINFO 传递到较低的驱动程序。 *Avc*不需要为仅限插入控制寄存器（PCR）的连接查看 AVCCONNECTINFO 结构。

    如果子单位不使用较低筛选器驱动程序来管理流格式，则子单位驱动程序将设置 IEEE 1394 串行总线插入连接。 有关详细信息，请参阅[AV/C 流式处理概述](av-c-streaming-overview.md)。

    如果出现以下情况，子源驱动程序应缓存格式的**hPlug**成员以设置对等连接：

    -   **HPlug**成员与由子单位驱动程序创建的成员不匹配。
    -   **DeviceID**成员与在 AVCPRECONNECTINFO 中接收的子单元驱动程序不匹配。
    -   **数据流**成员与子单位的 pin 的数据流不匹配。

5.  当要获取固定连接资源时，请[ **\_获取请求提交 AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-acquire)。 更低的驱动程序（或子单位驱动程序本身）使用任何缓存的 AVCCONNECTINFO 建立**hPlug**连接。 使用缓存的 AVCCONNECTINFO 接收**Avc\_函数\_获取**请求后，子单位和单元插头之间的内部连接将由*Avc*建立。 *Avc*不会缓存信息，也不会尝试内部插入连接（如果它没有内部插件控制）或连接被标记为永久。

6.  在要释放 pin 连接资源时， [ **\_发布请求提交 AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-release)。 更低的驱动程序和*Avc*保留任何缓存的 AVCCONNECTINFO，以便可以执行交替的*获取*和*释放*操作。

7.  提交[**AVC\_函数\_CLR\_CONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-clr-connectinfo)结构以删除缓存的 AVCCONNECTINFO 数据。

请注意，必须在数据交集（本地 AVCCONNECTINFO）期间创建的 AVCCONNECTINFO 结构中调用**AVC\_函数\_集\_CONNECTINFO**结构设置格式（外部 AVCCONNECTINFO）时传递的结构。 对于不同设备的子单元连接之间的连接，筛选器驱动程序（例如*Avcstrm）* 将缓存外部信息（外**hPlug**），而*Avc*会缓存本地信息。 对于同一设备中子单元连接之间的连接，筛选器驱动程序不缓存任何信息，而*Avc*仅缓存外子单位的信息。 筛选器驱动程序必须**将所有 AVC\_函数\_\_将**请求向下传递到*AVC*，以便阻止对子组插入连接进行决策。

AV/C 连接锁定位是在建立连接时设置的。 输出插针（源插头）公开允许重叠连接的多个 pin 实例（从同一输出到其他输入）。 但是，如果允许重叠连接，则不会阻止*断开*连接命令删除所有现有连接;这在 AV/C 规范中是固有的。 覆盖连接时，子组会发送多个**AVC\_函数\_SET\_CONNECTINFO**和**AVC\_函数\_获取**请求对（不包含干扰**AVC\_函数\_发布**请求）。 此外，如果将第二台计算机引入到 IEEE 1394 总线，或在同一台计算机上运行另一个不兼容的应用程序，则可能会出现这种情况。

*Avc*不直接支持 AV/C 外插连接，但*Avc*仍可通过提供合成 AVCCONNECTINFO 结构来建立子单位插头与外部插头之间的内部连接。 子单位驱动程序可以通过使用 AVC\_函数来创建 AVCCONNECTINFO 结构， [ **\_获取\_唯一的\_ID**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-unique-id)函数代码以填充**DeviceID**成员，同时提供单元地址0xff 和外部插件号（通过使用逻辑 OR 运算符，使用逻辑 "或" 运算符联接的插件号）来为**SubunitAddress**和**SubunitPlugNumber**成员提供正确**的数据流方向**。 **HPlug**和**UnitPlugNumber**成员应设置为**NULL**。 可以通过 AVC\_函数检测输入和输出外部插头的数量， **\_获取\_EXT\_插入\_计数**函数。

一种允许*Avc*对应用程序进行适当的内部插入连接并公开可能的外部连接到应用程序的方法是为每个可能的外部插件提供筛选器工厂。 生成的筛选器实例将公开适当的输入插针和输出插针，进而提供 AVCCONNECTINFO 结构。

 

 




