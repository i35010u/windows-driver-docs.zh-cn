---
title: TCP/IP 带索引属性和设备索引
description: TCP/IP 带索引属性和设备索引
keywords:
- TCP/IP 索引属性 WDK 打印机
- 索引属性 WDK 打印机
- 设备索引 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3690352687d134481ccdf07cbe3718bcb9024475
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806765"
---
# <a name="tcpip-indexed-properties-and-device-indexes"></a>TCP/IP 带索引属性和设备索引


利用索引属性，可以将数字索引追加到架构属性名称，从而使多个相关属性共享同一名称，但每个属性都有一个数字索引来识别单个属性。 索引值必须是正整数，但大小没有上限。 架构查询确定应该与特定元素关联的索引值。 此机制允许您访问 MIB 表中的数据。

IndexedProperty 构造定义索引属性。 以下限制适用于此构造。

-   IndexedProperty 构造不能是属性构造的父级。 NonIndexedProperty 构造是指在 IndexedProperty 构造下定义不含索引的属性。

-   IndexedProperty 构造和 NonIndexedProperty 构造都不能是已安装的构造的父级。

查询还可以涉及到另一索引：设备索引。 支持 SNMP 的网络设备可以是各种 subdevices （包括打印机）的主机。 网络打印机中的 MIB 表中的条目按设备索引)  (设备类型进行索引。 为了让查询从 MIB 表中检索数据，该查询必须具有正确的设备索引。 标准 TCP/IP 端口监视器允许端口配置 UI 配置设备索引。 一个双向扩展，其中 **deviceIndex** 设置为 **TRUE** (查看 [值](value.md) 和 [已安装](installed2.md) 的构造) 导致生成 oid，同时将设备索引连接到原始 OID。 如果使用索引属性，则会将其索引连接到设备索引后的 OID。

### <a name="code-example"></a>代码示例

下面的代码示例通过向 **Printer** 属性添加 **显示** 属性来扩展 tcp/ip 双向通信架构。 此外， **显示** 属性具有索引属性 **行**，并将 **deviceIndex** 设置为 **TRUE**。 此处所示的架构将生成一个查询，该查询将检索打印机显示的特定行中的文本。

```cpp
<Property name="Printer">
  <Property name="Display">
    <IndexedProperty name="Row">
      <Value name="Text" type="BIDI_TEXT" 
             oid="1.3.6.1.2.1.43.16.5.1.2" deviceIndex="true"/>
    </IndexedProperty>
  </Property>
</Property>
```

前面的示例将生成以下查询：

```cpp
\Printer.Display.Row1:Text
```

从此示例生成的 OID 开始与 **Value** 属性中的 **oid** 属性完全相同，但后面追加了两个索引。 该示例中追加的索引是从 **deviceIndex** 属性设置为 **TRUE** 且 **行** 为索引属性引发的。 假设端口配置 UI 将设备索引定义为111，并且打印机显示的第1行中的文本有兴趣，则生成的 OID 将为1.3.6.1.2.1.43.16.5.1.2.111.1。 除了 (111) 和属性索引 (1) 结尾的设备索引外，此 OID 与原始属性相同。 如果 **deviceIndex** 已设置为 **FALSE** 或省略，则生成的 OID 将为1.3.6.1.2.1.43.16.5.1.2.1。 若要显示显示的第 *n* 行中的文本，请使用的属性索引 *n*。

 

 




