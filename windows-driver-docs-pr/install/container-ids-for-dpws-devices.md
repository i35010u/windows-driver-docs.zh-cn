---
title: DPWS 设备的容器 ID
description: DPWS 设备的容器 ID
ms.assetid: b613a25e-bedf-481c-8c86-9486af01b2ba
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d91b04536745d444374cefb865fe21a7fa3f3f30
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902397"
---
# <a name="container-ids-for-dpws-devices"></a>DPWS 设备的容器 ID

从 Windows 7 开始，支持 PnP 扩展 ( (DPWS) 的 pnp) 和设备配置文件的设备可以通过在设备元数据文档中包括 **ContainerId** XML 元素来指定容器 ID。 有关 DPWS 和 DPWS 设备元数据文档的详细信息，请参阅 [DPWS 规范。](https://go.microsoft.com/fwlink/p/?linkid=142400)

>[!NOTE]
>从 Windows 10 开始，系统将忽略设备提供的容器 ID，而是自行生成。 它通过使用设备的终结点引用地址 (EPR) 中的 GUID 或设备的 EPR)  (的 SHA-1 哈希来实现此功能。

**ContainerId** XML 元素声明如下：

```cpp
<df:ContainerId xmlns:df="">
  xs:string
</df:ContainerId>
```

**ContainerId** XML 元素类型是一个字符串，其值是全局唯一标识符 (*GUID*) 格式设置。 此字符串的格式为 *{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}*。

下面是一个 **ContainerId** XML 元素的示例。

```cpp
<df:ContainerId xmlns:df="">
  {101392d0-5e91-11dd-ad8b-0800200c9a66}
</df:ContainerId>
```

&lt; &gt; 需要在 &lt; &gt; 设备元数据交换简单对象访问协议 (SOAP) 消息的 ThisDevice 部分中输入 ContainerId XML 元素。 下面的示例显示了 &lt; &gt; 元数据交换消息中的 ContainerId 元素的正确位置。

>[!NOTE]
>这不是完整的 DPWS 元数据交换文档。 有关 DPWS 的详细信息，请参阅 [DPWS 规范。](https://go.microsoft.com/fwlink/p/?linkid=142400)

```cpp
<soap:Envelope
    xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wsdisco="http://schemas.xmlsoap.org/ws/2005/04/discovery"
    xmlns:wsx="http://schemas.xmlsoap.org/ws/2004/09/mex"
    xmlns:wsd="http://schemas.xmlsoap.org/ws/2006/02/devprof"
    xmlns:df="http://schemas.microsoft.com/windows/2008/09/devicefoundation">

    <soap:Header>
        <!-- Place SOAP header information here.-->
    </soap:Header>

    <soap:Body>
        <wsx:Metadata>

           <wsx:MetadataSection
                Dialect="http://schemas.xmlsoap.org/ws/2005/05/devprof/ThisModel">
                <wsd:ThisDevice>
                    <!-- Place ThisDevice metadata here.-->
                    <df:ContainerId>
                        <!--- Place the ContainerID GUID here.--->
                        {101392d0-5e91-11dd-ad8b-0800200c9a66}
                    </df:ContainerId>
                </wsd:ThisDevice>
            </wsx:MetadataSection>

        </wsx:Metadata>
    </soap:Body>
</soap:Envelope>
```

如果 DPWS 设备元数据文档不包含 **ContainerId** XML 元素，则即插即用 (PnP) 管理器将设备终结点引用地址的值用作容器 ID。
