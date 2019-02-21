---
title: DPWS 设备的容器 Id
description: DPWS 设备的容器 Id
ms.assetid: b613a25e-bedf-481c-8c86-9486af01b2ba
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9694d53ac64ea133009fb4c3f1aa4b88b50fb785
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542172"
---
# <a name="container-ids-for-dpws-devices"></a>DPWS 设备的容器 Id


从 Windows 7，设备开始，支持的即插即用扩展 (PNP-X) 和设备配置文件的 Web 服务 (DPWS) 可以通过包含指定的容器 ID **ContainerId**设备元数据文档中的 XML 元素。 有关 DPWS 和 DPWS 设备元数据文档的详细信息，请参阅[DPWS 规范。](https://go.microsoft.com/fwlink/p/?linkid=142400)

**请注意**  从 Windows 10 开始，系统将忽略由设备提供的容器 ID，而是会生成一个本身。 这是通过使用设备的终结点引用地址 (EPR) 或设备的 EPR （如果不是一个 GUID） 的 sha-1 哈希中的 GUID。

 

**ContainerId** XML 元素声明，如下所示：

```cpp
<df:ContainerId xmlns:df="">
  xs:string
</df:ContainerId>
```

**ContainerId** XML 元素类型是一个字符串，其值为全局唯一标识符 (*GUID*) 格式。 此字符串的格式设置为 *{xxxxxxxx xxxx-xxxx-xxxx-在左右加上}*。

以下是一种**ContainerId** XML 元素。

```cpp
<df:ContainerId xmlns:df="">
  {101392d0-5e91-11dd-ad8b-0800200c9a66}
</df:ContainerId>
```

&lt;ContainerId&gt; XML 元素必须为处于&lt;ThisDevice&gt;设备元数据交换简单对象访问协议 (SOAP) 消息部分。 下面的示例显示了正确的位置&lt;ContainerId&gt;元数据交换消息中的元素。

**请注意**  这不是完整的 DPWS 元数据交换文档。 DPWS 有关的详细信息，请参阅[DPWS 规范。](https://go.microsoft.com/fwlink/p/?linkid=142400)

 

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

如果 DPWS 设备元数据文档不包括**ContainerId** XML 元素，插 (PnP) 管理器使用的设备的终结点引用地址的值作为容器 id。

 

 





