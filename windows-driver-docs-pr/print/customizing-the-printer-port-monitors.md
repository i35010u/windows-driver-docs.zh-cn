---
title: 自定义打印机端口监视器
description: 自定义打印机端口监视器
ms.assetid: e5d4166a-2593-43fd-b476-c54642e2d099
keywords:
- 在框中自动配置支持 WDK 打印机，自定义打印机端口监视器
- bidi 扩展文件 WDK 打印机自动配置
- 框中自动配置支持 WDK 打印机，bidi 扩展名为的文件
- 自定义打印机端口监视 WDK
- 端口监视器 WDK 打印，自定义
- WinSNMP 转换为 Bidi 数据键入 WDK 打印机
- 双向通信 WDK 打印
- 双向通信 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36f4eba5f7f96da40ca254e07ca518359fcc53b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372369"
---
# <a name="customizing-the-printer-port-monitors"></a>自定义打印机端口监视器


您可以定义具有超越标准功能的打印设备的新架构[bidi 通信架构](bidirectional-communication-schema.md)通过自定义标准 TCP/IP 或 Devices (WSD) 端口监视器随一起提供的 Web 服务Windows Vista。 必须创建 bidi 扩展文件，对该驱动程序定义特定的新架构的 XML 文件。 安装该驱动程序时，安装此扩展文件。 TCP/IP 或 WSD 端口监视器识别出该扩展文件，该监视器加载文件，然后可以使用其他 bidi 架构。

Bidi 扩展文件中的架构是标准的打印架构的子集。 此类架构必须遵守的 WDK 提供 Tcpbidi.xsd 或 WsdBidi.xsd 文件结构。

**请注意**  如果[bidi 通信架构](bidirectional-communication-schema.md)满足你的要求，不需要创建 bidi 扩展文件，因此无需自定义的打印端口监视器。

 

应创建 bidi 扩展文件，并将其与打印机驱动程序关联，如果任意下列条件适用：

1.  打印机驱动程序需要从不能在标准的打印架构中找到的打印机的信息。 若要获取此信息，必须扩展与其他查询支持的架构。 枚举支持的架构的特定端口的任何其他客户端获取其他查询，但通常不能理解它们。

2.  你打算包含在标准 TCP/IP 中不支持从标准的打印架构的查询或 WSD 端口监视，因为查询需要特定于驱动程序的信息。 在这种情况下，您必须扩展打印架构。 通常情况下，应将与输入和输出相关的打印架构的部分扩展打印介质的箱。 您还应提供的箱中的 bidi 架构和打印机的管理信息基础 (MIB) 中定义的名称之间的映射。

3.  你想通过进行自定义的标准方式查询工作，如设置自定义对象标识符 (OID) 或更改的刷新间隔。 例如，标准 TCP/IP 端口监视器将轮询 600 秒 （10 分钟） 以默认间隔不支持 Web 服务事件的设备。 可以通过创建 bidi 扩展的设置中 refreshInterval 特性更改的轮询间隔[值](value.md)构造与设备关联。 (请参阅`Memory`下面的代码示例中的属性。)

如果该驱动程序没有关联的 bidi 扩展文件，标准的打印架构中的双向通信支持不能响应查询需要驱动程序特定的数据 (如与相关的数据输入和输出箱)。

**请注意**   （无论是虚拟或物理） 的 Windows Vista 中的路由隔间允许受信任的进程连接到不同的网络的网络接口，同时保持与另一个隔离的各种接口。 例如，Windows Vista 使用这些隔离舱来强制实施 VPN 策略不允许同时访问 VPN 和用户的本地网络和 Internet 的。 在打印时，后台处理程序将模拟的用户时打开 TCP 打印机端口。 因此，后台处理程序不能打印到本地网络打印机，而用户连接到 VPN。

 

### <a name="structure-of-a-bidi-extension-file"></a>Bidi 扩展文件的结构

Bidi 扩展文件的格式正确 XML 必须符合提供与 Microsoft Windows Driver Kit (WDK) 的 Tcpbidi.xsd 或 WsdBidi.xsd 文件。 在这些.xsd 文件中定义的构造使您能够定义新的架构。

下面是不完整显示其基本结构 TCP/IP bidi 扩展文件的示例。 WSD bidi 扩展文件的结构是类似的。

```cpp
<?xml version="1.0" encoding="US-ASCII"?>
<bidi:Schema xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Schema>
    <Property name="Printer">
      <Property name="Configuration">
        <Property name= "Memory">
          <Value name="Size" type="BIDI_INT" oid="1.3.6.1.2.1.25.2.2" refreshInterval="600" drvPrinterEvent="true" />
          .
          .
          .
        </Property>
      </Property>
    </Property>
  </Schema>
</bidi:Schema>
```

在前面的代码示例，请注意:

-   根元素包含一个架构元素。 架构的层次结构开始与架构元素。

-   架构元素具有作为节点的属性元素和值元素离开。

-   每个值元素定义可按其检索数据的特定技术。

### <a name="conversion-of-winsnmp-to-bidi-data-types"></a>WinSNMP 转换为 Bidi 数据类型

中提供了简单网络管理协议 (SNMP) 类型和 bidi 类型之间的对应关系[ **BIDI\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type)枚举主题。

本部分的其余部分包含下列主题来帮助您创建 bidi 架构扩展。

[TCP/IP 架构扩展](tcp-ip-schema-extensions.md)

[WSD 架构扩展](wsd-schema-extensions-for-driver-specific-queries.md)

 

 




