---
title: 使用 XPS 光栅化服务
description: 使用 XPS 光栅化服务
ms.assetid: a6a3746a-3638-464b-bca0-60003f37af76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b2d72552e16ad793a19b5fa5ab02336a29369c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520544"
---
# <a name="using-the-xps-rasterization-service"></a>使用 XPS 光栅化服务


XPS 光栅化服务实现将 XPS 文档中的固定的页转换为位图的 XPS 光栅器对象。 此服务简化了将 XPS 文档呈现为一系列的位图图像的 XPSDrv 筛选器的设计。 筛选器可以告知 XPS 光栅器对象在固定页中创建一个与坐标轴对齐、 矩形区域的位图图像。

例如，打印机的 XPSDrv 筛选器可能需要固定的页后，可以为一系列的水平或垂直带区发送到打印机。 在这种情况下，筛选器告知 XPS 光栅器对象光栅化到每个带区作为单独的位图。 或者，如果打印机具有足够的内存，筛选器可能告知光栅器来创建整个页面的位图图像。

系统文件 Xpsrasterservice.dll 中实现 XPS 光栅化服务。 但是，XPSDrv 筛选器并不直接访问此 DLL 中的入口点。 相反，筛选器访问完成 XPS 光栅化服务的接口[**打印管道属性包**](https://msdn.microsoft.com/library/windows/hardware/ff561066)从打印筛选器管道管理器接收该筛选器。

若要可供使用的 XPSDrv 筛选器，XPS 光栅化服务必须以指定[筛选器管道配置文件](filter-pipeline-configuration-file.md)描述打印筛选器管道中的筛选器。 具体而言，该配置文件必须包含**FilterServiceProvider**具有元素**dll**属性设置为服务 DLL 名称，如下面的 XML 示例中所示：

```xml
  <FilterServiceProvider dll = "XpsRasterService.dll" />
```

**FilterServiceProvider**元素是子元素的**筛选器**列出了在管道中的筛选器的元素。 在管道初始化过程中打印筛选器管道管理器加载 XPS 光栅化服务，并使该服务通过属性包到筛选器可访问。 将 XPS 光栅化服务加载的筛选器管道配置文件的示例，请参阅 WDK 中的 XpsRasFilter 示例。 此示例位于 Src\\打印\\Xpsrasfilter WDK 安装中的文件夹。

### <a name="obtaining-an-xps-rasterization-factory"></a>获取一个 XPS 光栅化工厂

在光栅化 XPS 文档之前, XPSDrv 筛选器必须检索对光栅化工厂对象中打印的管道属性包的引用。 此后，筛选器从每个固定页的呈现所需的工厂获取新的 XPS 光栅器对象。

若要初始化的 XPSDrv 筛选器，打印筛选器管道管理器调用筛选器的[ **IPrintPipelineFilter::InitializeFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff554291)方法并传递属性包[IPrintPipelinePropertyBag](https://msdn.microsoft.com/library/windows/hardware/ff554320)作为输入参数的方法的接口。

若要获取指向 XPS 光栅化工厂对象的指针，XPSDrv 筛选呼叫[ **IPrintPipelinePropertyBag::GetProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff554331)方法。 属性名称"MS\_IXpsRasterizationFactory"标识光栅化工厂对象。 对于此属性，获取从该值**GetProperty**是对的光栅化工厂对象的引用**IUnknown**接口。 获取此接口后, 筛选器必须调用[iunknown:: Queryinterface](https://go.microsoft.com/fwlink/p/?linkid=119700)方法来获取对该对象的引用[IXpsRasterizationFactory](https://msdn.microsoft.com/library/windows/hardware/ff556356)接口。 随后，该筛选器可以调用[ **IXpsRasterizationFactory::CreateRasterizer** ](https://msdn.microsoft.com/library/windows/hardware/ff556350)方法来创建 XPS 光栅器对象。

如果不再需要的工厂对象，该筛选器应通过调用释放对象[释放](https://go.microsoft.com/fwlink/p/?linkid=98433)对象的方法**IXpsRasterizationFactory**接口。

下面的代码示例演示如何获取**IXpsRasterizationFactory**从接口实例**IPrintPipelinePropertyBag**接口实例：

```cpp
//
// Retrieve a reference to the XPS rasterization factory
// from the print pipeline property bag.
//
HRESULT CreateRasterizationFactory(
 IPrintPipelinePropertyBag *pPropertyBag,
 IXpsRasterizationFactory **ppXPSRasFactory)
{
    if (ppXPSRasFactory != NULL)
    {
        *ppXPSRasFactory = NULL;
    }

    if (pPropertyBag == NULL || ppXPSRasFactory == NULL)
    {
        return E_POINTER;
    }

    HRESULT hr;
    VARIANT var;
 IXpsRasterizationFactory *pXPSRasFactory;

    //
    // Retrieve the factory object from the property bag.
    //
 VariantInit(&var);
    hr = pPropertyBag->GetProperty(L"MS_IXpsRasterizationFactory",
                                   &var);
    if (SUCCEEDED(hr))
    {
        assert(var.vt == VT_UNKNOWN && var.punkVal != NULL);

        //
        // Get the factory object's IXpsRasterizationFactory interface.
        //
 IUnknown *pUnknown = var.punkVal;

        hr = pUnknown->QueryInterface(__uuidof(IXpsRasterizationFactory),
 reinterpret_cast<void**>(&pXPSRasFactory));
    }

    if (SUCCEEDED(hr))
    {
        //
        // Give the caller our reference to the IXpsRasterizationFactory interface.
        //
        *ppXPSRasFactory = pXPSRasFactory;
    }

 VariantClear(&var);
    return hr;
}
```

### <a name="creating-an-xps-object-model-of-a-fixed-page"></a>创建固定页的 XPS 对象模型

创建 XPS 光栅化工厂后，XPSDrv 筛选器可以使用工厂来创建 XPS 光栅器对象。 XPS 光栅器对象具有[IXpsRasterizer](https://msdn.microsoft.com/library/windows/hardware/ff556363)接口。 每个 XPS 光栅器对象专用于特定的固定页的 XPS 文档。 若要创建 XPS 光栅器对象，一个工厂需要固定页的 XPS 对象模型 (OM)。 中的对象具有包含 XPS OM （的固定页） **IXpsOMPage**接口。 XPS 光栅器对象使用此接口来访问固定页的内容。 有关详细信息**IXpsOMPage**接口，请参阅 Windows SDK 文档。

XPSDrv 筛选器按照以下步骤以创建 XPS 光栅器对象：

-   筛选器读取具有的固定的页对象[IFixedPage](https://msdn.microsoft.com/library/windows/hardware/ff551019)从输入流的接口。

-   筛选器创建具有的 XPS OM 对象**IXpsOMPage**接口来保存固定页的内容。 XPS 光栅器稍后将使用此接口访问的固定页内容。

-   若要创建 XPS 光栅器对象，该筛选器，将传递 XPS OM 对象**IXpsOMPage** XPS 光栅化工厂的接口**IXpsRasterizationFactory::CreateRasterizer**方法。

如果不再需要 XPS 光栅器对象，该筛选器应通过调用释放对象**释放**对象的方法**IXpsRasterizer**接口。 使用 XPS 光栅化服务的 XPSDrv 筛选器的实现示例，请参阅 WDK 中的 XpsRasFilter 示例驱动程序。

使用 XPS 光栅化服务，可以最多为 64 个级别嵌套画布和固定页中的视觉画笔。 有关画布和视觉画笔的详细信息，请下载[XML 纸张规范](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)。

### <a name="bitmap-resolution-and-pixel-format"></a>解决位图和像素格式

固定页的 XPS 光栅器对象必须知道呈现页面的分辨率。 XPSDrv 筛选器作为输入参数对的调用中指定此分辨率，以每英寸点数 (DPI) **IXpsRasterizationFactory::CreateRasterizer**创建 XPS 光栅器对象。 例如，如果显示设备具有 600 DPI，分辨率和固定的页介绍了标准的信纸大小页面，位图图像的整个页面具有以下维度：

宽度 = （8.5 英寸为单位） x(600 DPI) = 5100 点

高度 = （11 英寸） x(600 DPI) = 6600 点

若要创建位图图像的矩形区域的固定页，XPSDrv 筛选器调用了 XPS 光栅器对象的[ **IXpsRasterizer::RasterizeRect** ](https://msdn.microsoft.com/library/windows/hardware/ff556365)方法。 此方法始终会生成位图的像素大小为 32 位。 GUID 值所指定的像素格式**GUID\_WICPixelFormat32bppPBGRA**，该标头文件 Wincodec.h 中定义。 格式包含 8 位红色、 绿色和蓝色组件并使用标准 (sRGB) 颜色空间。 此外，格式包含一个 8 位 alpha 组件。 每个像素值的分量进行自左乘的 alpha 分量。 有关此格式的详细信息，请参阅[本机像素格式概述](https://msdn.microsoft.com/library/windows/desktop/ee719797.aspx)。

某些 XPSDrv 筛选器可能会执行其他处理 XPS 光栅器对象生成的位图。 例如，彩色打印机的筛选器可能将位图转换为 CMYK 像素格式，再在打印机的页面描述语言中包装位图，并将其发送到打印机。

有关 XPS 光栅化服务使用与 XPSDrv 筛选器进行通信的接口的详细信息，请参阅[XPS 光栅化服务引用](https://msdn.microsoft.com/library/windows/hardware/ff564306)。

### <a name="xpsras-and-high-precision-pixel-formats"></a>XPSRas 和高精度的像素格式

-   在 Windows 8 中，XPS 光栅化服务会公开一个新接口， [IXpsRasterizationFactory1](https://msdn.microsoft.com/library/windows/hardware/hh802467)，这是新版本[IXpsRasterizationFactory](https://msdn.microsoft.com/library/windows/hardware/ff556356)。 **IXpsRasterizationFactory1**公开的新方法[ **IXpsRasterizationFactory1::CreateRasterizer1**](https://msdn.microsoft.com/library/windows/hardware/hh802468)，它与 Windows 7 版本相同 ([ **IXpsRasterizationFactory::CreateRasterizer**](https://msdn.microsoft.com/library/windows/hardware/ff556350))，只不过它采用一个新参数为输出像素格式。
-   此功能公开的新枚举[ **XPSRAS\_像素\_格式**](https://msdn.microsoft.com/library/windows/hardware/hh802469)，允许调用方可以选择使用的像素格式[IWICBitmap](https://msdn.microsoft.com/library/windows/desktop/ee719675.aspx)IXpsRasterizer::RasterizeRect 方法返回的接口。

### <a name="xpsras-and-the-gpu"></a>XPSRas 和 GPU

如果必须使用 WDDM 1.2 显示驱动程序，运行 Windows 8 的计算机和中所示的所有条件[XPSRas GPU 使用情况决策树](xpsras-usage-decision-tree.md)均已满足，则始终使用 GPU 硬件加速。 这意味着，作为开发人员，您无需执行任何步骤以从提供的 GPU 的性能增强功能中受益。 但是，若要进一步优化您的系统的图形性能，您应考虑执行以下操作：

-   调用[ **RasterizeRect** ](https://msdn.microsoft.com/library/windows/hardware/ff556365)具有一致的矩形尺寸方法。 如果这是不可能，最好提供**RasterizeRect** ，最大所需的第一个调用上的矩形大小，并在后续调用中请求较小的矩形大小。
-   仅当绝对需要时使用抗锯齿。 带锯齿的文本和矢量与对应抗锯齿时一样的 DPI 值提供给[ **IXpsRasterizationFactory::CreateRasterizer** ](https://msdn.microsoft.com/library/windows/hardware/ff556350)方法是相当高。 例如，大于 200 DPI 的 DPI 值被视为高。 应进行测试以确保给定设备上的输出质量足够时使用带锯齿的文本和以及高 DPI 的向量。
-   如果可以在光栅化之前操作文档 IXpsOMPage，然后子集化字体，并使用多个页面上重复的元素的资源字典将提高 XPSRas 性能。
