---
title: 示例扩展单元插件 DLL
description: 示例扩展单元插件 DLL
ms.assetid: bd9ea70d-7bd0-494d-8d67-7a36a41d005b
keywords:
- 插件 DLL WDK USB 视频类
- 扩展单位 WDK USB 视频类，示例中，插件 DLL
- 示例代码 WDK USB 视频类扩展单元插件 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bf245d4dac1ec8b886eca4ace2042950818b8e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360111"
---
# <a name="sample-extension-unit-plug-in-dll"></a>示例扩展单元插件 DLL


本主题包含示例代码的公开 COM API 之上 KS 属性集的扩展单元插件 DLL。

此示例定义一个名为类**CExtension**，它派生**CNodeControl**。 实现**CNodeControl**类还提供了更高版本。 **CNodeControl**派生的 Microsoft 提供**IKsNodeControl**接口中定义*Vidcap.h*。

*Vidcap.ax*使用**IKsNodeControl**若要告知插件的扩展节点 ID，并为其提供的一个实例**IKsControl**。 具体而言，该插件收到此信息通过调用**CExtension::put\_NodeId**并**CExtension::put\_KsControl**。 可以稍后在本主题中找到这些方法的可能的实现，父类**CNodeControl**。

*Vidcap.h*将出现在 2004 年夏季 DirectX SDK 通过 2005 年 2 月[DirectX SDK](https://go.microsoft.com/fwlink/p/?linkid=51990)。 安装这些程序包时，必须安装其他功能来获取*Vidcap.h*。

在 Windows Vista 和更高版本*Vidcap.h*是作为 Microsoft Windows SDK 的一部分。

下面的代码包含在类标头文件中，任意名为*Xuproxy.h*:

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

实现中的两个虚方法**IKsNodeControl**中**CNodeControl**。 这些方法然后由的实例继承**CExtension**类。

下面的代码是任意名为源代码文件中的*Xuproxy.cpp*:

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

此外包括以下内容的实现**CExtension**的方法中相同*Xuproxy.cpp*文件：

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

 

 




