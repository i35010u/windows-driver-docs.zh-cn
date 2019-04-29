---
title: 属性页插件
description: 属性页插件
ms.assetid: cf5f5861-1670-413c-9c42-c1b6eb6d719a
keywords:
- 内核流式处理代理 WDK AVStream，属性页
- 属性页 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca2464ee8b40dfb68b434d02b0f09d2f1ef60666
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362209"
---
# <a name="property-page-plug-in"></a>属性页插件


可以通过编写为 KS 代理插件的属性页提供设备属性的用户界面。 本主题说明如何编写此类的插件。 首先，注册您的对象，如中所述[注册 KS 代理插件](registering-ks-proxy-plug-ins.md)。

接下来，声明你的筛选器的工厂模板。 工厂模板是C++类，该类包含的类工厂的信息。

在您的 DLL，声明一个全局数组[CFactoryTemplate](https://go.microsoft.com/fwlink/p/?linkid=106450)对象、 一个用于每个筛选器或 DLL 中的 COM 组件。 如果只有一个属性页，创建只有一个对象数组中。

每个对象，生成的类标识符 (CLSID) 的 GUID 并提供在声明中的条目。

数组必须命名为 g\_模板：

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

属性页应派生自类[CBasePropertyPage](https://go.microsoft.com/fwlink/p/?linkid=106449)和应重写的方法的几个**CBasePropertyPage**:

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

若要初始化的属性页，宿主的属性表调用[IPropertyPage::SetPageSite](https://go.microsoft.com/fwlink/p/?linkid=106442)。 此调用会导致调用即插即用接**OnConnect**方法。 在此调用时，属性页已连接到该筛选器，但尚未显示属性页。

对的调用中提供的参数**OnConnect** KS 代理，然后指向指针的查询必须处于**IKsPropertySet**。 然后，可以调用[ **IKsPropertySet::Get** ](https://msdn.microsoft.com/library/windows/hardware/ff560719)并[ **IKsPropertySet::Set** ](https://msdn.microsoft.com/library/windows/hardware/ff560721)来操作的驱动程序公开的属性。

你还必须提供**CreateInstance**方法。 系统调用属性页的方法来创建属性页的实例。 此方法应调用其进行实例化类的构造函数。

构造函数接收指向外部未知接口，在这种情况下是 KS 代理的指针。

属性页**OnDisconnect**时的属性页应释放关联的对象调用方法。 此回调应递减到 KS 代理的接口指针的引用计数，通过调用其**版本**方法。

 

 




