---
title: 接口处理程序插件
description: 接口处理程序插件
ms.assetid: cd81f622-d11c-4b40-ac78-9324716e0a2c
keywords:
- 内核流式处理代理 WDK AVStream，接口处理程序
- 接口处理程序 WDK AVStream
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6b88c785085be750a4cd882b06662265c8c7339e
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992482"
---
# <a name="interface-handler-plug-in"></a>接口处理程序插件

您可以编写接口处理程序插件来向由 KS 微型驱动程序公开的特定于驱动程序的属性集提供以编程方式进行的用户模式访问。 首先，按[注册 KS 代理插件](registering-ks-proxy-plug-ins.md)中所述注册对象。

接口插件类可以从[CUnknown](https://docs.microsoft.com/previous-versions//ms783086(v=vs.85))派生：

```cpp
class CMyPluginInterface : public CUnknown
{
public:
    // creation method
    static CUnknown* CALLBACK CreateInstance( LPUNKNOWN piOuterUnknown, HRESULT* phResult );
private:
 CMyPluginInterface( IKsPropertySet* piKsPropertySet );
    IKsPropertySet* m_piKsPropertySet;
};
```

接口插件是供应商提供的 COM 接口，可在创建时与 MS 提供的 KS 代理进行聚合。

具体而言，该插件的**CreateInstance**方法接收指向 KS 代理的指针作为外部未知。

然后，可以查询此外部对象以获得指向 MS 提供的[IKsPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/dsound/nn-dsound-ikspropertyset)接口的指针：

```cpp
hResult = piOuterUnknown->QueryInterface(
                __uuidof( piKsPropertySet ),
                 &piKsPropertySet );
```

然后，从**CreateInstance**调用接口的构造函数，以创建接口处理程序对象的实例。

提供指向**IKsPropertySet**的指针，作为构造函数调用中的参数。 然后，构造函数将指针作为 \_ 前面声明中的 m piKsPropertySet 成员保留到 iKsPropertySet。

现在，你可以在类中实现 Get 和 Set 方法，分别调用[**IKsPropertySet：： Get**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikspropertyset-get)和[**IKsPropertySet：： Set**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dsound/nf-dsound-ikspropertyset-set)来操作驱动程序所公开的属性。

另外，还可以查询指向其**IKsObject**接口的指针的外部未知。 然后调用[**IKsObject：： KsGetObjectHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-iksobject-ksgetobjecthandle)以获取文件句柄。 现在，通过使用此文件句柄调用[**KsSynchronousIoControlDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kssynchronousiocontroldevice)来操作设备属性。
