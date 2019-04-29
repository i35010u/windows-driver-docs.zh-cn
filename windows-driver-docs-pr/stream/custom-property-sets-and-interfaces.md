---
title: 自定义属性集和接口
description: 自定义属性集和接口
ms.assetid: ea1337e4-c8e5-4971-b602-c066b5a6fd07
keywords:
- 接口 WDK 视频捕获
- 自定义属性集 WDK 视频捕获
- 视频捕获 WDK AVStream，属性设置
- 捕获视频 WDK AVStream，属性设置
- 属性集 WDK 视频捕获
- 自定义接口 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24114469e8dcf501be497ed9310e838b1c16c01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374131"
---
# <a name="custom-property-sets-and-interfaces"></a>自定义属性集和接口


供应商可以实现自定义属性集来控制特定于设备的或特定于流的参数。 通常情况下，这些内核的属性集公开为 COM 接口的自定义*KsProxy*插件 DLL。 同样，可以实现自定义属性页来提供用户界面来控制自定义属性集。

**若要创建自定义属性集**

1.  创建使用设置该属性的唯一的 GUID *Guidgen.exe*。 （此工具包含在 Microsoft Windows SDK 中）。

2.  实现你的微型驱动程序中设置的属性。

**若要创建属性组的自定义 COM 接口或属性页面**

1.  创建一个自定义的 KsProxy 插件 DLL 实现 COM 接口或属性页。 插件 DLL 类 ID (CLSID) 必须与属性集 GUID 匹配。 链接到*ksproxy.lib*若要获取的实现 **:: KsSynchronousDeviceControl**。

2.  添加公开的标准 Microsoft DirectShow 机制*CFactoryTemplateg\_模板*从 DLL 以允许自注册你的接口。

3.  将行添加到您的硬件设备安装文件 （INF 文件） 来公开 COM 接口和属性页，该示例中所示*MyINF.inf*下面。

下面的代码演示如何实现 IAMCameraControl:

**Camera.h**

```cpp
/*
Implements IAMCameraControl via KSPROPERTY_VIDCAP_CAMERACONTROL
*/

class CCameraControlInterfaceHandler :
    public CUnknown,
    public IAMCameraControl {

public:
    DECLARE_IUNKNOWN;

    static CUnknown* CALLBACK CreateInstance(
        LPUNKNOWN UnkOuter,
        HRESULT* hr);

    CCameraControlInterfaceHandler(
        LPUNKNOWN UnkOuter,
        TCHAR* Name,
        HRESULT* hr);

    STDMETHODIMP NonDelegatingQueryInterface(
        REFIID riid,
        PVOID* ppv);

    STDMETHODIMP Set( 
            IN long Property,
            IN long lValue,
            IN long Flags);

private:
    HANDLE m_ObjectHandle;
};
```

**Camera.cpp**

```cpp
/*
Implements IAMCameraControl via KSPROPERTY_VIDCAP_CAMERACONTROL
*/

#include "pch.h"
#include "camera.h"

CUnknown*
CALLBACK
CCameraControlInterfaceHandler::CreateInstance(
    LPUNKNOWN   UnkOuter,
    HRESULT*    hr
    )
{
    CUnknown *Unknown;

    Unknown = new CCameraControlInterfaceHandler(UnkOuter, NAME("IAMCameraControl"), hr);
    if (!Unknown) {
        *hr = E_OUTOFMEMORY;
    }
    return Unknown;
} 

CCameraControlInterfaceHandler::CCameraControlInterfaceHandler(
    LPUNKNOWN   UnkOuter,
    TCHAR*      Name,
    HRESULT*    hr
    ) :
    CUnknown(Name, UnkOuter, hr)
{
    if (SUCCEEDED(*hr)) {
        if (UnkOuter) {
            IKsObject*  Object;
            *hr =  UnkOuter->QueryInterface(uuidof(IKsObject), reinterpret_cast<PVOID*>(&Object));
            if (SUCCEEDED(*hr)) {
                m_ObjectHandle = Object->KsGetObjectHandle();
                // m_Object handle is file handle of the driver
                if (!m_ObjectHandle) {
                    *hr = E_UNEXPECTED;
                }
                Object->Release();
            }
        } else {
            *hr = VFW_E_NEED_OWNER;
        }
    }
}

STDMETHODIMP
CCameraControlInterfaceHandler::Set(
     IN long Property,
     IN long lValue,
     IN long lFlags
     )
{
    KSPROPERTY_CAMERACONTROL_S  CameraControl;
    ULONG       BytesReturned;

 CameraControl.Property.Set = PROPSETID_VIDCAP_CAMERACONTROL;
 CameraControl.Property.Id = Property;
    CameraControl.Property.Flags = KSPROPERTY_TYPE_SET;
    CameraControl.Value = lValue;
 CameraControl.Flags = lFlags;
    CameraControl.Capabilities = 0;

 return ::KsSynchronousDeviceControl(
                m_ObjectHandle,
                IOCTL_KS_PROPERTY,
                &CameraControl,
                sizeof(CameraControl),
                &CameraControl,
                sizeof(CameraControl),
                &BytesReturned);
}

STDMETHODIMP
CCameraControlInterfaceHandler::NonDelegatingQueryInterface(
    REFIID  riid,
    PVOID*  ppv
    )
{
    if (riid == uuidof(IAMCameraControl)) {
        return GetInterface(static_cast<IAMCameraControl*>(this), ppv);
    }
    return CUnknown::NonDelegatingQueryInterface(riid, ppv);
}
```

**MyINF.inf**

```INF
;IAMCameraControl
HKCR,CLSID\{C6E13370-30AC-11d0-A18C-00A0C9118956},,,%PlugIn_IAMCameraControl%
HKCR,CLSID\{C6E13370-30AC-11d0-A18C-00A0C9118956}\InprocServer32,,,kswdmcap.ax
HKCR,CLSID\{C6E13370-30AC-11d0-A18C-00A0C9118956}\InprocServer32,ThreadingModel,,Both
; This IID is aggregated for the filter given the CLSID of the property set
HKLM,System\CurrentControlSet\Control\MediaInterfaces\{C6E13370-30AC-11d0-A18C-00A0C9118956},,,%PlugIn_IAMCameraControl%
HKLM,System\CurrentControlSet\Control\MediaInterfaces\{C6E13370-30AC-11d0-A18C-00A0C9118956},IID,1,70,33,E1,C6,AC,30,d0,11,A1,8C,00,A0,C9,11,89,56

; CameraControl Property Page
HKCR,CLSID\{71F96465-78F3-11d0-A18C-00A0C9118956},,,%PropPage_CameraControl%
HKCR,CLSID\{71F96465-78F3-11d0-A18C-00A0C9118956}\InprocServer32,,,kswdmcap.ax
HKCR,CLSID\{71F96465-78F3-11d0-A18C-00A0C9118956}\InprocServer32,ThreadingModel,,Both
; Associate the property set with the above property page
HKLM,System\CurrentControlSet\Control\MediaSets\{C6E13370-30AC-11d0-A18C-00A0C9118956}\PropertyPages\{71F96465-78F3-11d0-A18C-00A0C9118956},,,%PropPage_CameraControl%
```








