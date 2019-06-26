---
title: 接口处理程序插件
description: 接口处理程序插件
ms.assetid: cd81f622-d11c-4b40-ac78-9324716e0a2c
keywords:
- 内核流式处理代理 WDK AVStream，接口处理程序
- 接口处理程序 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11c5e3759b86c4098d042f3e5037d5a277e1496a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360657"
---
# <a name="interface-handler-plug-in"></a>接口处理程序插件


您可以编写一个插件，以提供对 KS 微型驱动程序公开特定于驱动程序的属性集的用户模式下以编程方式访问的界面处理程序。 首先，注册您的对象，如中所述[注册 KS 代理插件](registering-ks-proxy-plug-ins.md)。

接口插件类可以派生自[CUnknown](https://go.microsoft.com/fwlink/p/?linkid=106451):

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

插件的接口是聚合与提供 MS KS 代理在创建时的供应商提供 COM 接口。

具体而言， **CreateInstance**的插件方法接收指向 KS 代理为外部未知的。

然后，您可以查询指向 MS 提供的此外部对象[IKsPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dsound/nn-dsound-ikspropertyset)接口：

```cpp
hResult = piOuterUnknown->QueryInterface(
                __uuidof( piKsPropertySet ),
                 &piKsPropertySet );
```

然后，从**CreateInstance**，调用接口来创建界面处理程序对象的实例的构造函数。

提供指向指针**IKsPropertySet**作为构造函数的调用中的参数。 构造函数然后会保留为 m iKsPropertySet 指向\_piKsPropertySet 在以上声明中的成员。

现在，您可以实现 Get，在类中设置方法调用[ **IKsPropertySet::Get** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikspropertyset-get)并[ **IKsPropertySet::Set** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dsound/nf-dsound-ikspropertyset-set)分别用于处理由驱动程序公开的属性。

或者，您可以查询一个指向未知的外部及其**IKsObject**接口。 然后调用[ **IKsObject::KsGetObjectHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-iksobject-ksgetobjecthandle)来获取文件句柄。 现在，通过调用操作设备属性[ **KsSynchronousIoControlDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kssynchronousiocontroldevice)与此文件句柄。

 

 




