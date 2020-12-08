---
title: 示例扩展单元插件 DLL
description: 示例扩展单元 DLL
keywords:
- 插件 DLL WDK USB 视频类
- 扩展单元-WDK USB 视频类、示例、插件 DLL
- 示例代码 WDK USB 视频类，扩展单元插件 DLL
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: ef02fa04d0fff5f64560d975393e33b6b54ff4f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805931"
---
# <a name="sample-extension-unit-plug-in-dll"></a>示例扩展单元 DLL

本主题包含用于在 KS 属性集的顶层公开 COM API 的扩展单元插件 DLL 的示例代码。

此示例定义了一个名为 **CExtension** 的类，该类派生自 **CNodeControl**。 稍后还提供了 **CNodeControl** 类的实现。 **CNodeControl** 派生自 Microsoft 提供的 **IKsNodeControl** 接口，该接口是在 *Vidcap* 中定义的。

*Vidcap.ax* 使用 **IKsNodeControl** 来通知扩展节点 ID 的插件，并为其提供 **IKsControl** 的实例。 具体而言，该插件通过对 CExtension 的调用来接收此信息 **：:p \_ ：** **:p CExtension 和 \_ KsControl**。 可以在本主题的 **CNodeControl** 中找到这些方法的可能实现。

*Vidcap* 通过2月 2005 [directx Sdk](/previous-versions/dn629515(v=msdn.10))出现在夏季 2004 directx sdk 中。 安装这些包时，必须安装其他内容才能获取 *Vidcap*。

在 Windows Vista 和更高版本中， *Vidcap* 作为 Microsoft Windows SDK 的一部分包含。

在类头文件中包含以下代码，任意命名为 *Xuproxy*：

```cpp
#include <ks.h>
#include <ksproxy.h>
#include <C:\Program Files\Microsoft DirectX 9.0 SDK (February 2005)\Extras\DirectShow\Include\vidcap.h>
#include <C:\Program Files\Microsoft DirectX 9.0 SDK (February 2005)\Extras\DirectShow\Include\ksmedia.h>

DEFINE_GUID(CLSID_ExtensionUnit, 0xzzzzzzzz, 0xzzzz, 0xzzzz, 0xzz, 0xzz, 0xzz, 0xzz, 0xzz, 0xzz, 0xzz, 0xzz);

class CNodeControl :
    public IKsNodeControl
{
public:
    STDMETHOD(put_NodeId) (DWORD dwNodeId);
    STDMETHOD(put_KsControl) (PVOID pKsControl);

    DWORD m_dwNodeId;
    CComPtr<IKsControl> m_pKsControl;
};

class CExtension :
   public IExtensionUnit,
   public CComObjectRootEx<CComObjectThreadModel>,
   public CComCoClass<CExtension, &CLSID_ExtensionUnit>,
   public CNodeControl
{
   public:

   CExtension();
   STDMETHOD(FinalConstruct)();

   BEGIN_COM_MAP(CExtension)
      COM_INTERFACE_ENTRY(IKsNodeControl)
      COM_INTERFACE_ENTRY(IExtensionUnit)
   END_COM_MAP()

   DECLARE_PROTECT_FINAL_CONSTRUCT()
   DECLARE_NO_REGISTRY()
   DECLARE_ONLY_AGGREGATABLE(CExtension)

   // IExtensionUnit
   public:
   STDMETHOD (get_Info)(
      ULONG ulSize,
      BYTE pInfo[]);
   STDMETHOD (get_InfoSize)(
      ULONG *pulSize);
   STDMETHOD (get_PropertySize)(
      ULONG PropertyId,
      ULONG *pulSize);
   STDMETHOD (get_Property)(
      ULONG PropertyId,
      ULONG ulSize,
      BYTE pValue[]);
   STDMETHOD (put_Property)(
      ULONG PropertyId,
      ULONG ulSize,
      BYTE pValue[]);
   STDMETHOD (get_PropertyRange)(
      ULONG PropertyId,
      ULONG ulSize,
      BYTE pMin[],
      BYTE pMax[],
      BYTE pSteppingDelta[],
      BYTE pDefault[]);
};

#define STATIC_PROPSETID_VIDCAP_EXTENSION_UNIT \
   0xXXXXXXXX,0xXXXX,0xXXXX,0xXX,0xXX,0xXX,0xXX,0xXX,0xXX,0xXX,0xXX
DEFINE_GUIDSTRUCT("XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX", \
   PROPSETID_VIDCAP_EXTENSION_UNIT);
#define PROPSETID_VIDCAP_EXTENSION_UNIT \
   DEFINE_GUIDNAMED(PROPSETID_VIDCAP_EXTENSION_UNIT)
```

在 **CNodeControl** 中实现 **IKsNodeControl** 中的两个虚拟方法。 然后，这些方法由 **CExtension** 类的实例继承。

以下代码位于任意名为 *Xuproxy* 的源文件中：

```cpp
STDMETHODIMP
CNodeControl::put_NodeId(
   DWORD dwNodeId)
{
   m_dwNodeId = dwNodeId;
 return S_OK;
}

STDMETHODIMP
CNodeControl::put_KsControl(
   PVOID pKsControl)
{
   HRESULT hr = S_OK;
   IKsControl *pIKsControl;

 if (!pKsControl) return E_POINTER;
    pIKsControl = (IKsControl *) pKsControl;

    if (m_pKsControl) m_pKsControl.Release();
 hr = pIKsControl->QueryInterface(__uuidof(IKsControl),
       (void **) &m_pKsControl);

    return hr;
}
```

还在同一 *Xuproxy* 文件中包含 **CExtension** 的方法实现：

```cpp
CExtension::CExtension()
{
    m_pKsControl = NULL;
}

STDMETHODIMP
CExtension::FinalConstruct()
{
    if (m_pOuterUnknown == NULL ) return E_FAIL;
    return S_OK;
}

STDMETHODIMP
CExtension::get_InfoSize(
    ULONG *pulSize)
{
    HRESULT hr = S_OK;
    ULONG ulBytesReturned;
    KSP_NODE ExtensionProp;

    if (!pulSize) return E_POINTER;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = KSPROPERTY_EXTENSION_UNIT_INFO;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET |
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

 hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
        sizeof(ExtensionProp),
        NULL,
        0,
        &ulBytesReturned);

    if (hr == HRESULT_FROM_WIN32(ERROR_MORE_DATA))
    {
        *pulSize = ulBytesReturned;
        hr = S_OK;
    }

 return hr;
}


STDMETHODIMP
CExtension::get_Info(
    ULONG ulSize,
    BYTE pInfo[])
{
    HRESULT hr = S_OK;
    KSP_NODE ExtensionProp;
    ULONG ulBytesReturned;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = KSPROPERTY_EXTENSION_UNIT_INFO;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET |
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
 sizeof(ExtensionProp),
        (PVOID) pInfo,
        ulSize,
        &ulBytesReturned);

 return hr;
}


STDMETHODIMP
CExtension::get_PropertySize(
    ULONG PropertyId,
    ULONG *pulSize)
{
    HRESULT hr = S_OK;
    ULONG ulBytesReturned;
    KSP_NODE ExtensionProp;

 if (!pulSize) return E_POINTER;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = PropertyId;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET |
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
 sizeof(ExtensionProp),
        NULL,
        0,
        &ulBytesReturned);

 if (hr == HRESULT_FROM_WIN32(ERROR_MORE_DATA))
    {
        *pulSize = ulBytesReturned;
        hr = S_OK;
    }

 return hr;
}

STDMETHODIMP
CExtension::get_Property(
    ULONG PropertyId,
    ULONG ulSize,
    BYTE pValue[])
{
    HRESULT hr = S_OK;
    KSP_NODE ExtensionProp;
    ULONG ulBytesReturned;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = PropertyId;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET |
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
 sizeof(ExtensionProp),
        (PVOID) pValue,
        ulSize,
        &ulBytesReturned);

    return hr;
}

STDMETHODIMP
CExtension::put_Property(
    ULONG PropertyId,
    ULONG ulSize,
    BYTE pValue[])
{
    HRESULT hr = S_OK;
    KSP_NODE ExtensionProp;
    ULONG ulBytesReturned;

    ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = PropertyId;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_SET |
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
 sizeof(ExtensionProp),
        (PVOID) pValue,
        ulSize,
        &ulBytesReturned);

    return hr;
}

STDMETHODIMP
CExtension::get_PropertyRange(
    ULONG PropertyId,
    ULONG ulSize,
    BYTE pMin[  ],
    BYTE pMax[  ],
    BYTE pSteppingDelta[  ],
    BYTE pDefault[  ])
{
    // IHV may add code here, current stub just returns S_OK
    HRESULT hr = S_OK;
    return hr;
}

CExtension::CExtension()
{
    m_pKsControl = NULL;
}

STDMETHODIMP
CExtension::FinalConstruct()
{
    if (m_pOuterUnknown == NULL) return E_FAIL;
    return S_OK;
}
```
