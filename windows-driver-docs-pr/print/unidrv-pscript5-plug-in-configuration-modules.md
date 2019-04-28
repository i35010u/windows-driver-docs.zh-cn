---
title: Unidrv/PScript5 插件配置模块
description: Unidrv/PScript5 插件配置模块
ms.assetid: 806175ba-18a9-48f3-8f50-06e794d1f304
keywords:
- 版本 3 XPS 驱动程序 WDK XPSDrv Unidrv 插件
- 版本 3 XPS 驱动程序 WDK XPSDrv PScript5 插件
- IPrintCoreHelper
- Pscript WDK 打印，XPSDrv 打印驱动程序
- Unidrv、 XPSDrv 打印驱动程序
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd0e8b9a940b463fc0a33c30b741232618209ae0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346555"
---
# <a name="unidrvpscript5-plug-in-configuration-modules"></a>Unidrv/PScript5 插件配置模块


在 Windows Vista 中使用 Unidrv 或 PScript5 配置插件的 XPSDrv 打印机驱动程序配置模块支持以下新功能：

-   PrintTicket 和 PrintCapabilities 功能

-   [IPrintCoreHelper](https://msdn.microsoft.com/library/windows/hardware/ff552960)接口用于操作 Unidrv 和 PScript5 设置

-   XPSDrv 文档事件

-   与通信打印驱动程序筛选器管道中的筛选器

### <a name="printticket-and-printcapabilities-interface-support"></a>PrintTicket 和 PrintCapabilities 接口支持

Unidrv 和 PScript5 打印驱动程序插件实现[IPrintOemPrintTicketProvider](https://msdn.microsoft.com/library/windows/hardware/ff553174)接口可自定义的 PrintTicket 和 PrintCapabilities 数据。 此接口中的方法允许插件以自定义 PrintTicket 和 PrintCapabilities 处理此插件提供的自定义功能。

Unidrv 和 PScript5 打印驱动程序实现[IPrintTicketProvider](https://msdn.microsoft.com/library/windows/hardware/ff554375)接口，并生成基于 GPD 或 PPD 文件的 PrintTicket 和 PrintCapabilities 数据的初始版本。 之后的初始处理 Unidrv 或 PScript5 打印驱动程序然后调用即插即用接**IPrintOemPrintTicketProvider**接口，以便插件可以修改此数据，然后打印驱动程序将其返回给调用应用程序。

### <a name="iprintcorehelper-interface"></a>IPrintCoreHelper 接口

**IPrintCoreHelper**接口，插件的打印驱动程序配置：

-   获取和设置 DEVMODE 结构的专用部分中的值，该 Unidrv 和 PScript5 打印驱动程序使用。

-   枚举打印驱动程序功能、 选项和约束。

-   访问完整 GPD 或部分 PPD 文件内容。

若要正确设置 Unidrv 或 PScript5 配置并启用完整的用户界面 (UI) 的替代功能为插件的唯一方法是通过使用以下**IPrintCoreHelper**接口。

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

以下两个其他接口， [IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)并[IPrintCoreHelperPS](https://msdn.microsoft.com/library/windows/hardware/ff552906)，派生自**IPrintCoreHelper**接口。 这些接口是特定于 Unidrv 和 PScript5 分别打印驱动程序，并包括是唯一的每个驱动程序的其他方法。

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

下面的代码示例演示了如何使用**IPrintCoreHelper**查询信息从 DEVMODE 结构的接口。 此示例中是 XPSDrv 打印机驱动程序示例代码中 Windows Driver Kit (WDK) 的一部分。

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

 

 




