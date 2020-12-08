---
title: 自定义属性集和接口
description: 自定义属性集和接口
keywords:
- 接口 WDK 视频捕获
- 自定义属性设置 WDK 视频捕获
- 视频捕获 WDK AVStream，属性集
- 捕获视频 WDK AVStream，属性集
- 属性集 WDK 视频捕获
- 自定义接口 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d96cc03dd76a6948f9ec5e1c5e20d6d156f8c5b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817967"
---
# <a name="custom-property-sets-and-interfaces"></a>自定义属性集和接口


供应商可以实现自定义属性集来控制特定于设备或流的参数。 通常，这些内核属性集通过自定义 *KsProxy* 插件 DLL 作为 COM 接口公开。 同样，可以实现自定义属性页，以便提供用户界面来控制自定义属性集。

**创建自定义属性集**

1.  使用 *Guidgen.exe* 为属性集创建唯一的 GUID。  (此工具包含在 Microsoft Windows SDK 中。 ) 

2.  实现微型驱动程序中设置的属性。

**为属性集创建自定义 COM 接口或属性页**

1.  创建一个实现 COM 接口或属性页的自定义 KsProxy 插件 DLL。 插件 DLL (CLSID) 的类 ID 必须与属性集 GUID 匹配。 链接到 *ksproxy* 以获取 **：： KsSynchronousDeviceControl** 的实现。

2.  添加从 DLL 公开 *CFactoryTemplateg \_ 模板* 的标准 Microsoft DirectShow 机制，以允许接口的自我注册。

3.  向硬件的设备安装文件添加行 (INF 文件) 以公开 COM 接口和属性页，如下面的示例 *MyINF* 中所示。

下面的代码演示 IAMCameraControl 的实现：

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

**MyINF .inf**

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








