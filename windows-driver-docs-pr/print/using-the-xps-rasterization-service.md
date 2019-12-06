---
title: 使用 XPS 光栅化服务
description: 使用 XPS 光栅化服务
ms.assetid: a6a3746a-3638-464b-bca0-60003f37af76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc60046c38303f8bdb0a3cd7ad0320b4555bd51
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881880"
---
# <a name="using-the-xps-rasterization-service"></a>使用 XPS 光栅化服务

XPS 光栅化服务实现了将 XPS 文档中的固定页面转换为位图的 XPS 光栅化对象。 此服务简化了将 XPS 文档呈现为一系列位图图像的 XPSDrv 筛选器的设计。 筛选器可以告知 XPS 光栅器对象在固定页面中创建与轴对齐的矩形区域的位图图像。

例如，打印机的 XPSDrv 筛选器可能需要将固定页作为一系列水平或垂直带区发送到打印机。 在这种情况下，该筛选器会告诉 XPS 光栅器对象将每个带区光栅化为单独的位图。 或者，如果打印机有足够的内存，筛选器可能会告诉光栅器创建整个页面的位图图像。

XPS 光栅化服务是在系统文件 Xpsrasterservice.dll 中实现的。 但是，XPSDrv 筛选器不直接访问此 DLL 中的入口点。 相反，筛选器通过筛选器从打印筛选器管道管理器接收的[**打印管道属性包**](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag)访问 XPS 光栅化服务的接口。

若要使 XPSDrv 筛选器可以使用，必须在[筛选器管道配置文件](filter-pipeline-configuration-file.md)中指定 XPS 光栅化服务，该配置文件描述打印筛选器管道中的筛选器。 具体而言，配置文件必须包含一个设置为服务 DLL 名称的**FilterServiceProvider**元素，其**dll**特性设置为，如下面的 XML 示例中所示：

```xml
  <FilterServiceProvider dll = "XpsRasterService.dll" />
```

**FilterServiceProvider**元素是**筛选器**元素的子元素，它列出管道中的筛选器。 在管道初始化期间，打印筛选器管道管理器加载 XPS 光栅化服务，并通过属性包使该服务可访问该服务。 有关加载 XPS 光栅化服务的筛选器管道配置文件的示例，请参阅 WDK 中的 XpsRasFilter 示例。 此示例位于\\在 WDK 安装中打印\\Xpsrasfilter 文件夹中。

## <a name="obtaining-an-xps-rasterization-factory"></a>获取 XPS 光栅化工厂

在光栅化 XPS 文档之前，XPSDrv 筛选器必须从打印管道属性包中检索对光栅化工厂对象的引用。 此后，筛选器将从工厂为需要呈现的每个固定页面获取一个新的 XPS 光栅器对象。

为了初始化 XPSDrv 筛选器，打印筛选器管道管理器会调用筛选器的[**IPrintPipelineFilter：： InitializeFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iprintpipelinefilter-initializefilter)方法，并将属性包的[IPrintPipelinePropertyBag](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinepropertybag)接口作为输入参数传递到方法。

若要获取指向 XPS 光栅化工厂对象的指针，XPSDrv 筛选器将调用[**IPrintPipelinePropertyBag：： GetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iprintpipelinepropertybag-getproperty)方法。 属性名称 "MS\_IXpsRasterizationFactory" 标识光栅化工厂对象。 对于此属性，从**GetProperty**获取的值是对光栅化工厂对象的**IUnknown**接口的引用。 获取此接口后，筛选器必须调用[IUnknown：： QueryInterface](https://go.microsoft.com/fwlink/p/?linkid=119700)方法，以获取对该对象的[IXpsRasterizationFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory)接口的引用。 随后，筛选器可以调用[**IXpsRasterizationFactory：： CreateRasterizer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer)方法来创建 XPS 光栅器对象。

当不再需要 factory 对象时，该筛选器应通过对对象的**IXpsRasterizationFactory**接口调用[release](https://go.microsoft.com/fwlink/p/?linkid=98433)方法来释放对象。

下面的代码示例演示如何从**IPrintPipelinePropertyBag**接口实例获取**IXpsRasterizationFactory**接口实例：

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

## <a name="creating-an-xps-object-model-of-a-fixed-page"></a>创建固定页面的 XPS 对象模型

创建 XPS 光栅化工厂后，XPSDrv 筛选器可以使用工厂来创建 XPS 光栅器对象。 XPS 光栅化对象具有[IXpsRasterizer](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nn-xpsrassvc-ixpsrasterizer)接口。 每个 XPS 光栅化程序对象专用于 XPS 文档的特定固定页面。 若要创建 XPS 光栅化对象，工厂需要固定页面的 XPS 对象模型（OM）。 XPS OM （固定页面）包含在具有**IXpsOMPage**接口的对象中。 XPS 光栅化对象使用此接口访问固定页面的内容。 有关**IXpsOMPage**接口的详细信息，请参阅 Windows SDK 文档。

XPSDrv 筛选器按照以下步骤创建 XPS 光栅器对象：

- 筛选器从输入流中读取具有[IFixedPage](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-ifixedpage)接口的固定页面对象。

- 该筛选器创建一个具有**IXpsOMPage**接口的 XPS OM 对象，以保存固定页面的内容。 XPS 光栅化稍后将使用此接口来访问固定页面的内容。

- 若要创建 XPS 光栅器对象，筛选器会将 XPS OM 对象的**IXpsOMPage**接口传递到 xps 光栅化工厂的**IXpsRasterizationFactory：： CreateRasterizer**方法。

如果不再需要 XPS 光栅器对象，筛选器应通过对对象的**IXpsRasterizer**接口调用**release**方法来释放对象。 有关使用 XPS 光栅化服务的 XPSDrv 筛选器的示例实现，请参阅 WDK 中的 XpsRasFilter 示例驱动程序。

若要与 XPS 光栅化服务一起使用，固定页面内的画布和视觉对象画笔最多可以嵌套到64级别。 有关画布和视觉对象画笔的详细信息，请下载[XML 纸张规范](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)。

## <a name="bitmap-resolution-and-pixel-format"></a>位图分辨率和像素格式

固定页面的 XPS 光栅化对象必须知道呈现页面的分辨率。 XPSDrv 筛选器指定此分辨率（以每英寸点数（DPI）为单位），它是对创建 XPS 光栅器对象的**IXpsRasterizationFactory：： CreateRasterizer**的调用中的输入参数。 例如，如果显示设备的分辨率为 600 DPI，固定页面说明了标准的 letter 大小页面，则整个页面的位图图像具有以下尺寸：

width = （8.5 英寸） x （600 DPI） = 5100 点

高度 = （11英寸） x （600 DPI） = 6600 点

若要创建固定页面的矩形区域的位图图像，XPSDrv 筛选器会调用 XPS 光栅器对象的[**IXpsRasterizer：： RasterizeRect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizer-rasterizerect)方法。 此方法始终产生像素大小为32位的位图。 像素格式由 GUID 值**guid 指定\_WICPixelFormat32bppPBGRA**，它是在头文件 Wincodec 中定义的。 格式包含8位红色、绿色和蓝色分量，并使用标准（sRGB）颜色空间。 此外，该格式还包含一个8位 alpha 分量。 每个像素值中的颜色分量由 alpha 分量预乘。 有关此格式的详细信息，请参阅[本机像素格式概述](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)。

某些 XPSDrv 筛选器可能会对 XPS 光栅器对象生成的位图执行额外的处理。 例如，彩色打印机的筛选器可能会将位图转换为 CMYK 像素格式，然后才能在打印机的页面描述语言中将其发送到打印机。

有关 XPS 光栅化服务用于与 XPSDrv 筛选器进行通信的接口的详细信息，请参阅[Xps 光栅化服务引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)。

## <a name="xpsras-and-high-precision-pixel-formats"></a>XPSRas 和高精度像素格式

- 在 Windows 8 中，XPS 光栅化服务公开了新的接口[IXpsRasterizationFactory1](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory1)，它是[IXpsRasterizationFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory)的新版本。 **IXpsRasterizationFactory1**公开一个与 Windows 7 版本（[**IXpsRasterizationFactory：： CreateRasterizer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer)）相同的新方法[**IXpsRasterizationFactory1：： CreateRasterizer1**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))，只不过它需要一个新参数用于输出像素格式。

- 此功能公开一个新枚举[**XPSRAS\_像素\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/ne-xpsrassvc-__midl___midl_itf_xpsrassvc_0000_0003_0001)，它允许调用方选择 IXpsRasterizer：： RasterizeRect 方法返回的[IWICBitmap](https://docs.microsoft.com/windows/desktop/api/wincodec/nn-wincodec-iwicbitmap)接口所使用的像素格式。

## <a name="xpsras-and-the-gpu"></a>XPSRas 和 GPU

如果计算机运行的是带有 WDDM 1.2 显示器驱动程序的 Windows 8，并且已满足[XPSRAS Gpu 使用情况决策树](xpsras-usage-decision-tree.md)中显示的所有条件，则始终使用 GPU 硬件加速。 这意味着，作为开发人员，您不必执行任何步骤来从 GPU 提供的性能增强中获益。 但是，若要进一步优化系统的图形性能，应考虑执行以下操作：

- 调用具有一致矩形尺寸的[**RasterizeRect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizer-rasterizerect)方法。 如果无法做到这一点，最好在第一次调用时为**RasterizeRect**提供最大的所需矩形大小，并在后续调用时要求更小的矩形大小。

- 仅在绝对需要时使用抗锯齿。 当提供给[**IXpsRasterizationFactory：： CreateRasterizer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer)方法的 DPI 值明显较高时，化名为的文本和矢量看起来与反别名对应。 例如，大于200DPI 的 DPI 值被视为高。 应进行测试，以确保在使用带有别名的文本和矢量以及高 DPI 时，给定设备上的输出质量已经足够。

- 如果在对 IXpsOMPage 进行光栅化之前可以对文档进行操作，则在多个页面上重复的元素的子集化字体和使用资源字典将提高 XPSRas 性能。
