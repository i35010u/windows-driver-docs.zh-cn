---
title: TCP/IP 编制索引的属性和设备索引
description: TCP/IP 编制索引的属性和设备索引
ms.assetid: b26b0c18-1787-43e0-8461-acfbd9fb38f9
keywords:
- TCP/IP 索引属性 WDK 打印机
- 索引的属性 WDK 打印机
- 设备索引 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: debaae0b9b7525edd897c6cb364263f98ea209e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543560"
---
# <a name="tcpip-indexed-properties-and-device-indexes"></a>TCP/IP 编制索引的属性和设备索引


索引的属性启用要追加到架构属性名称，从而支持多个相关的属性，以共享相同的名称，但每个都有一个数字索引来标识的单个属性的数字索引。 索引值必须是正整数，但其大小上没有上限。 架构查询确定与特定元素相关联的索引值。 此机制允许您访问 MIB 表中的数据。

IndexedProperty 构造定义的索引的属性。 以下限制适用于此构造。

-   IndexedProperty 构造不能为父属性构造。 NonIndexedProperty 构造是指定义不包含下一个 IndexedProperty 构造索引的属性。

-   IndexedProperty 构造和 NonIndexedProperty 构造都不可以是已安装构造的父级。

查询还可能涉及到另一个索引： 设备索引。 支持 SNMP 的网络设备可以是各种子设备，包括打印机的主机。 网络打印机中的 MIB 表中具有根据设备类型 （设备索引） 编制索引的条目。 为了使 MIB 表中检索数据的查询，查询必须具有正确的设备索引。 标准 TCP/IP 端口监视器允许设备索引配置的端口配置 UI。 在其中一个 bidi 扩展**deviceIndex**设置为**TRUE** (请参阅[值](value.md)并[已安装](installed2.md)构造) 会导致生成的 OID具有设备索引连接到原始的 OID。 如果使用，索引属性的索引被连接到设备索引后，该 OID。

### <a name="code-example"></a>代码示例

下面的代码示例通过添加扩展 TCP/IP bidi 通信架构**Display**属性设置为**打印机**属性。 此外，**显示**属性的索引的属性**行**，并且具有**deviceIndex**设置为**TRUE**。 如下所示的架构将生成从打印机的显示中的特定行中检索文本的查询。

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

前面的示例生成以下查询：

```cpp
\Printer.Display.Row1:Text
```

此示例中生成的 OID 启动相同**oid**属性中**值**属性，但具有两个附加到它的索引。 在示例中的追加的索引源于**deviceIndex**属性设置为**TRUE**和**行**被索引的属性。 假定端口配置 UI 定义设备索引为 111，和感兴趣的打印机的显示的第 1 行中的文本，生成的 OID 将 1.3.6.1.2.1.43.16.5.1.2.111.1。 此 OID 等同于原始设备索引 (111) 和结束属性索引 (1) 除外。 如果**deviceIndex**设置为**FALSE**或省略，则生成的 OID 是 1.3.6.1.2.1.43.16.5.1.2.1。 若要显示行中的文本*n*的显示中，使用的属性索引*n*。

 

 




