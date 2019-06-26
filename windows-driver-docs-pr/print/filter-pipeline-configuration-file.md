---
title: 筛选器管道配置文件
description: 筛选器管道配置文件
ms.assetid: 586247bd-6d06-4728-a5f0-ee3fe1d09321
keywords:
- XPSDrv 的打印机驱动程序 WDK，呈现模块
- 呈现模块 WDK XPSDrv，筛选器管道配置文件
- 筛选器管道配置文件 WDK XPSDrv
- 专用关键字 WDK XPSDrv
- 筛选器管道属性包 WDK XPSDrv
- 属性包 WDK 筛选器管道
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3998e550f4abf47a937242617042c5bc7d0a0a46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382586"
---
# <a name="filter-pipeline-configuration-file"></a>筛选器管道配置文件


*筛选器管道配置文件*是定义了以下一个 XML 文件：

-   在管道中的筛选器的顺序。 筛选器管道配置文件中的 XML 元素的顺序来定义此顺序。

-   筛选器接口。 这些接口由筛选器管道配置文件中的 XML 特性定义。

-   每个筛选器的输入和输出格式。 这些格式定义的筛选器管道配置文件中的 XML 元素。

下面的代码示例显示了典型的筛选器管道配置文件：

```xml
<Filters>
    <Filter      dll="XDWMark.dll"
 clsid="{D647D658-BEF6-415f-AFAC-070D64074C5D}"
                name="Watermark filter">
        <Input  guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
        <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
    </Filter>
 <Filter dll="XDScale.dll"
 clsid="{B9B52406-92D3-4721-86E6-3CF78F6D5FC5}"
 name="Page Scaling filter">
 <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream"/>
 <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream"/>
 </Filter>
    <Filter      dll="XDColMan.dll"
 clsid="{8E56FC37-0799-447e-A643-16F4FB18244C}"
 name="Colour Management filter">
         <Input guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
        <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
    </Filter>
    <Filter      dll="XDBook.dll"
 clsid="{7DFC96C6-CEA2-46d8-B354-887C47B7986D}"
                name="Booklet filter">
         <Input guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
        <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
    </Filter>
    <Filter      dll="XDNUp.dll"
 clsid="{1b5bee16-511c-440f-8017-2123f481091a}"
                name="NUp filter">
         <Input guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
        <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
    </Filter>
</Filters>
```

### <a name="private-keywords"></a>Private 关键字

[XPSDrv 配置模块](xpsdrv-configuration-module.md)可以放置*专用关键字*中的 PrintTicket 条目时它处理[XPS 驱动程序文档事件](xps-driver-document-events.md)期间[ **DrvDocumentEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent)函数调用。 而筛选器正在读取 PrintTicket，然后读取这些 PrintTicket 条目中的打印筛选器管道的处理筛选器。

### <a name="filter-pipeline-property-bag"></a>筛选器管道属性包

此外可以使用配置模块*筛选器管道属性包*来存储数据，或将信息传递给筛选器管道。 若要配置服务使用公开的属性包，配置模块必须导出**DrvPopulateFilterServices**方法。 此外，筛选器管道配置文件必须包括 **&lt;FilterServiceProvider&gt;** 元素为每个服务。 提供程序模块必须实现和导出**DllCanUnloadNow**函数。 通常情况下，这些提供程序发布的属性包中的 COM 接口。 使用这些接口时，该提供程序必须保持加载。

另一个元素，  **&lt;OptionalFilterServiceProvider&gt;** ，允许管理器以在服务提供程序 dll 不可用时继续打印作业的管道。 单个筛选器必须在没有可选的服务提供程序的情况下定义它们的行为。 否则为如果 **&lt;FilterServiceProvider&gt;** 使用并且不能加载了 dll，作业将失败。 **&lt;OptionalFilterServiceProvider&gt;** 元素支持在 Windows 7 及更高版本。

下面的代码示例演示**DrvPopulateFilterServices**函数：

```cpp
HRESULT
DrvPopulateFilterServices(
    __in IPrintPipelinePropertyBag  *pPropertyBag
    );
```

有关上述函数的详细信息，请参阅[ **DrvPopulateFilterServices**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nf-filterpipeline-drvpopulatefilterservices)。

下面的代码示例显示的 XML 语法 **&lt;FilterServiceProvider&gt;** 筛选器管道配置文件中的元素：

```xml
<Filters>
    <Filter ... />
    <FilterServiceProvider dll = "providerA.dll"/>
    <FilterServiceProvider dll = "providerB.dll"/>
</Filters>
```

### <a name="interleaving-mode-for-the-output-device"></a>为输出设备在交错执行模式

*交错*指 FixedPage 文档部件以及如何流式传输 XPS 文档的单独的资源部分。 筛选器管道在管道中的 XPS 文档接口创建的第一个筛选器的 XPS 文档对象模型，将无法再遵循交错 XPS 假脱机文件的顺序。 但是，使用 XPS 文档界面在管道中的最后一个筛选器可以在序列化 XPS 内容时要使用的管道的筛选器配置文件中指定交错的顺序。 选择最符合输出设备或输出文件的交错顺序可以提高后续文档处理的性能。

以下示例筛选器是已修改，以便显示如何使用交错选项前面的示例筛选器配置文件的摘录。 虽然此示例演示这两个交错选项用于演示目的，真正的筛选器配置文件具有只有一个 **&lt;Interleaving&gt;** 筛选器定义中的元素：

```xml
    <Filter     dll="XDNUp.dll"
      clsid="{1b5bee16-511c-440f-8017-2123f481091a}"
        name="NUp filter">
      <Input guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
       <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
     <Interleaving mode="ResourcesFirst"\>
     <Interleaving mode="MarkupFirst"\>
    </Filter>
```

筛选器管道支持以下交错订单：

-   **ResourcesFirst**隔行扫描顺序流依赖于该资源 FixedPage 之前每个从属资源。 此交错的顺序很好的打印机驱动程序和直接使用打印机，因为它提供了打印机要求通过要呈现的文本和页面内容开始渲染之前的字体和图像资源。

-   **MarkupFirst**隔行扫描顺序流文档文本和标记以及流式处理的实际资源之前将如何使用资源的相关信息。 此交错的顺序是最佳存档文件目标和联机查看文档的应用程序。

### <a name="archive-optimized-xps-output"></a>存档优化 XPS 输出

此功能允许打印驱动程序显式请求作为后台打印文件存档优化 XPS 输出。 在 Windows 8 中，Microsoft XPS Document Writer v4 (MXDW) 生成此存档就绪 XPS 的输出通过仅可供 MXDW Microsoft XPS 文档转换器 (MXDC) 中的代码路径。 因此打印驱动程序可以从 MXDC 生成此存档优化 XPS。

下面的代码示例演示使用的 XML 语法&lt;存档&gt;若要启用此功能在筛选器管道配置文件中的元素：

```xml
<Filters>
    ...
    <Archive enabled="true"/>
</Filters>
```
