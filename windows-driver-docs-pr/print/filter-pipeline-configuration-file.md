---
title: 筛选器管道配置文件
description: 筛选器管道配置文件
keywords:
- XPSDrv 打印机驱动程序 WDK，呈现模块
- 渲染模块 WDK XPSDrv，筛选器管道配置文件
- 筛选器管道配置文件 WDK XPSDrv
- 私有关键字 WDK XPSDrv
- 筛选器管道属性包 WDK XPSDrv
- 属性包 WDK 筛选器管道
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e840f3303af20a0d564a616d66e618ce21ea5a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797089"
---
# <a name="filter-pipeline-configuration-file"></a>筛选器管道配置文件


*筛选器管道配置文件* 是一个 XML 文件，用于定义以下内容：

-   管道中筛选器的顺序。 此顺序由筛选器管道配置文件中的 XML 元素的顺序定义。

-   筛选接口。 这些接口由筛选器管道配置文件中的 XML 特性定义。

-   每个筛选器的输入和输出格式。 这些格式由筛选器管道配置文件中的 XML 元素定义。

下面的代码示例演示了一个典型的筛选器管道配置文件：

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

### <a name="private-keywords"></a>私有关键字

当 [XPSDrv 配置模块](xpsdrv-configuration-module.md)在 [**DrvDocumentEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent)函数调用期间处理 [XPS 驱动程序文档事件](xps-driver-document-events.md)时，它可以将 *私有关键字* 放在 PrintTicket 条目中。 然后，在筛选器读取 PrintTicket 时，打印筛选器管道中的处理筛选器将读取这些 PrintTicket 条目。

### <a name="filter-pipeline-property-bag"></a>筛选器管道属性包

配置模块还可以使用 *筛选器管道属性包* 来存储数据，或将信息传递给筛选器管道。 若要使用属性包公开配置服务，配置模块必须导出 **DrvPopulateFilterServices** 方法。 此外，筛选器管道配置文件必须包括每个服务的 **&lt; FilterServiceProvider &gt;** 元素。 提供程序模块必须实现并导出 **DllCanUnloadNow** 函数。 通常情况下，这些提供程序将在属性包中发布 COM 接口。 当使用这些接口时，提供程序必须保持加载。

如果服务提供程序 dll 不可用，则另一个元素 **&lt; OptionalFilterServiceProvider &gt;** 允许管道管理器继续执行打印作业。 如果没有可选的服务提供程序，则各个筛选器都必须定义其行为。 否则，如果使用 **&lt; FilterServiceProvider &gt;** 并且无法加载 dll，则作业将失败。 Windows 7 及更高版本支持 **&lt; OptionalFilterServiceProvider &gt;** 元素。

下面的代码示例显示了 **DrvPopulateFilterServices** 函数：

```cpp
HRESULT
DrvPopulateFilterServices(
    __in IPrintPipelinePropertyBag  *pPropertyBag
    );
```

有关前述函数的详细信息，请参阅 [**DrvPopulateFilterServices**](/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-drvpopulatefilterservices)。

下面的代码示例显示了筛选器管道配置文件中的 **&lt; FilterServiceProvider &gt;** 元素的 XML 语法：

```xml
<Filters>
    <Filter ... />
    <FilterServiceProvider dll = "providerA.dll"/>
    <FilterServiceProvider dll = "providerB.dll"/>
</Filters>
```

### <a name="interleaving-mode-for-the-output-device"></a>输出设备的隔行扫描模式

*交错* 是指 XPS 文档的各个资源部分与 FixedPage 文档部分一起流动的方式。 当筛选器管道为管道中包含 XPS 文档接口的第一个筛选器创建 XPS 文档对象模型时，将不再遵循 XPS 假脱机文件的交错顺序。 但是，使用 XPS 文档界面的管道中的最后一个筛选器可以在筛选器配置文件中指定一个交错顺序，以便管道在序列化 XPS 内容时使用。 选择与输出设备或输出文件最兼容的交错顺序可以提高后续文档处理的性能。

下面的示例筛选器摘自前面的示例筛选器配置文件，该文件已修改以显示如何使用隔行扫描选项。 尽管此示例演示了用于说明的隔行扫描选项，但实际筛选器配置文件在筛选器定义中只有一个 **&lt; 交错 &gt;** 元素：

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

筛选器管道支持以下交错顺序：

-   **ResourcesFirst** 交错顺序在依赖于资源的 FixedPage 之前流式传输每个相关资源。 这种交错顺序适用于打印机驱动程序和直接消耗打印机，因为它提供了打印机在呈现开始之前需要呈现文本和页面内容的字体和图像资源。

-   **MarkupFirst** 交错顺序流式传输文档文本和标记，以及有关如何在处理实际资源之前使用资源的信息。 此交错顺序最适用于存档文件目标和联机查看文档的应用程序。

### <a name="archive-optimized-xps-output"></a>Archive-Optimized XPS 输出

此功能使打印驱动程序可以将存档优化的 XPS 输出显式请求为假脱机文件。 在 Windows 8 中，Microsoft XPS 文档编写器 v4 (MXDW) 通过仅可用于 Microsoft XPS 文档转换器 (MXDC) 中的 MXDW 的代码路径生成此存档就绪的 XPS 输出。 因此，打印驱动程序可以从 MXDC 生成此存档优化的 XPS。

下面的代码示例演示了在 &lt; &gt; 筛选器管道配置文件中使用 Archive 元素实现此功能的 XML 语法：

```xml
<Filters>
    ...
    <Archive enabled="true"/>
</Filters>
```
