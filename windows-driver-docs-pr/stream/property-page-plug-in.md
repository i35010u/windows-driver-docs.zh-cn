---
title: 属性页插件
description: 属性页插件
ms.assetid: cf5f5861-1670-413c-9c42-c1b6eb6d719a
keywords:
- 内核流式处理代理 WDK AVStream，属性页
- 属性页 WDK AVStream
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: d56e7740f312fb610d7f234302cbd417222b22e9
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073421"
---
# <a name="property-page-plug-in"></a>属性页插件

可以通过将属性页编写为 KS 代理的插件来向设备属性提供用户界面。 本主题说明如何编写此类插件。 首先，按[注册 KS 代理插件](registering-ks-proxy-plug-ins.md)中所述注册对象。

接下来，为筛选器声明工厂模板。 工厂模板是包含类工厂信息的 c + + 类。

在 DLL 中，声明[CFactoryTemplate](https://docs.microsoft.com/previous-versions//ms781337(v=vs.85))对象的全局数组，每个对象对应于 DLL 中的一个筛选器或 COM 组件。 如果只有一个属性页，请在数组中仅创建一个对象。

对于每个对象，为类标识符（CLSID）生成一个 GUID，并在声明中提供一个条目。

该数组必须命名为 g \_ Templates：

```cpp
CFactoryTemplate g_Templates[] =
{
    {
        L"My Property Page",
        &CLSID_MyPropPage),
        CMyPropPage::CreateInstance,
        NULL,
        NULL
    },
};
```

属性页应从类[CBasePropertyPage](https://docs.microsoft.com/previous-versions//ms780508(v=vs.85))派生，并应重写**CBasePropertyPage**的若干方法：

```cpp
class CMyPropPage: public CBasePropertyPage
{
public:
    // creation routine returns ptr to new prop pg as a CUnknown
    static CUnknown* CreateInstance( LPUNKNOWN piOuterUnknown, HRESULT* phResult );

    // overridden methods:
    HRESULT OnConnect( IUnknown *punk);
    HRESULT OnDisconnect();
    HRESULT OnApplyChanges();
    HRESULT OnActivate();
    HRESULT OnDeactivate();
    INT_PTR OnReceiveMessage( HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam );
private:
    CMyPropPage ( LPUNKNOWN piOuterUnknown );
};
```

若要初始化属性页，承载属性表将调用[IPropertyPage：： SetPageSite](https://docs.microsoft.com/windows/win32/api/ocidl/nf-ocidl-ipropertypage-setpagesite)。 此调用会导致调用插件的**OnConnect**方法。 在进行此调用时，属性页已连接到筛选器，但尚未显示属性页。

在对**OnConnect**的调用中提供的参数是指向 KS 代理的接口，然后可以查询该代理以获取指向**IKsPropertySet**的指针。 然后，可以调用[**IKsPropertySet：： Get**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikspropertyset-get)和[**IKsPropertySet：： Set**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dsound/nf-dsound-ikspropertyset-set)以操作驱动程序的公开属性。

还必须提供**CreateInstance**方法。 系统调用属性页的方法来创建属性页的实例。 此方法应调用类的构造函数来对其进行实例化。

构造函数接收指向外部未知接口的指针，在本例中为 KS 代理。

当属性页应释放关联的对象时，将调用属性页的**OnDisconnect**方法。 此回调应通过调用其**Release**方法将指向该接口的指针的引用计数减少到 KS 代理。
