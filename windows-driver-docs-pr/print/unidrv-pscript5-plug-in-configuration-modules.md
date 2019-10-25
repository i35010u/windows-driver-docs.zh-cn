---
title: Unidrv/PScript5 插件配置模块
description: Unidrv/PScript5 插件配置模块
ms.assetid: 806175ba-18a9-48f3-8f50-06e794d1f304
keywords:
- 版本 3 XPS 驱动程序 WDK XPSDrv、Unidrv 插件
- 版本 3 XPS 驱动程序 WDK XPSDrv、PScript5 插件
- IPrintCoreHelper
- Pscript WDK 打印，XPSDrv 打印驱动程序
- Unidrv，XPSDrv 打印驱动程序
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7723a7674408a1aaece1c8211208c8b030d991c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843621"
---
# <a name="unidrvpscript5-plug-in-configuration-modules"></a>Unidrv/PScript5 插件配置模块


在 Windows Vista 中使用 Unidrv 或 PScript5 配置插件的 XPSDrv 打印驱动程序配置模块支持以下新功能：

-   PrintTicket 和 PrintCapabilities 功能

-   用于操作 Unidrv 和 PScript5 设置的[IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)接口

-   XPSDrv 文档事件

-   与筛选器管道中的打印驱动程序筛选器通信

### <a name="printticket-and-printcapabilities-interface-support"></a>PrintTicket 和 PrintCapabilities 接口支持

Unidrv 和 PScript5 打印驱动程序插件实现[IPrintOemPrintTicketProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)接口，以自定义 PrintTicket 和 PrintCapabilities 数据。 此接口中的方法允许插件为该插件提供的自定义功能自定义 PrintTicket 和 PrintCapabilities 处理。

Unidrv 和 PScript5 打印驱动程序实现[IPrintTicketProvider](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))接口，并生成基于 GPD 或 PPD 文件的 PrintTicket 和 PrintCapabilities 数据的初始版本。 初次处理后，Unidrv 或 PScript5 打印驱动程序将调用插件的**IPrintOemPrintTicketProvider**接口，以便在打印驱动程序将此数据返回到调用应用程序之前，该插件可以修改此数据。

### <a name="iprintcorehelper-interface"></a>IPrintCoreHelper 接口

**IPrintCoreHelper**接口启用打印驱动程序配置插件来执行以下操作：

-   获取并设置 Unidrv 和 PScript5 打印驱动程序使用的 DEVMODE 结构的私有部分中的值。

-   枚举打印驱动程序功能、选项和约束。

-   访问完整的 GPD 或部分 PPD 文件内容。

插件正确设置 Unidrv 或 PScript5 配置和启用完全用户界面（UI）替换功能的唯一方法是使用以下**IPrintCoreHelper**接口。

```cpp
DECLARE_INTERFACE_(IPrintCoreHelper, IUnknown) {
  // IUnknown methods skipped
  STDMETHOD(CreateInstanceOfMSXMLObject)(...)
  STDMETHOD(EnumConstrainedOptions)(...)
  STDMETHOD(EnumFeatures)(...)
  STDMETHOD(EnumOptions)(...)
  STDMETHOD(GetOption)(...)
  STDMETHOD(SetOptions)(...)
  STDMETHOD(WhyConstrained)(...)
};
```

以下两个附加接口（ [IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)和[IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)）派生自**IPrintCoreHelper**接口。 这些接口分别是 Unidrv 和 PScript5 打印驱动程序的特定，并包含每个驱动程序独有的其他方法。

```cpp
DECLARE_INTERFACE_(IPrintCoreHelperUni, IUnknown) {
  // IUnknown methods skipped
  // IPrintCoreHelper methods skipped
  STDMETHOD(CreateDefaultGDLSnapshot)(...)
  STDMETHOD(CreateGDLSnapshot)(...)
};

DECLARE_INTERFACE_(IPrintCoreHelperPS, IUnknown) {
  // IUnknown methods skipped
  // IPrintCoreHelper methods skipped
  STDMETHOD(GetFeatureAttribute)(...)
  STDMETHOD(GetGlobalAttribute)(...)
  STDMETHOD(GetOptionAttribute)(...)
};
```

下面的代码示例演示如何使用**IPrintCoreHelper**接口从 DEVMODE 结构中查询信息。 此示例是 Windows 驱动程序工具包（WDK）中 XPSDrv 打印驱动程序示例代码的一部分。

```cpp
HRESULT
CBookletDMPTConv::GetDrvSettingsFromDM(
    __in    PDEVMODE                         pDevmode,
            ULONG                            cbDevmode,
    __out   GPD::Binding::DrvSettings*       pDrvSettings
    )
{
  HRESULT hr = S_OK;

  for (GPD::Binding::EGPDSettings setting = 
        GPD::Binding::EGPDSettingsMin;
      setting < GPD::Binding::EGPDSettingsMax && SUCCEEDED(hr);
      setting++)
  {
    PCSTR pszOption;
    hr = m_pCoreHelper->GetOption(
      pDevmode,
      cbDevmode, 
      m_featureNames[setting], 
      &pszOption)
    if (SUCCEEDED(hr))
    {
      hr = GPDSettingFromOptionString(
      pszOption, 
      setting, 
      pDrvSettings);
    }
  }

  return hr;
}
```

 

 




