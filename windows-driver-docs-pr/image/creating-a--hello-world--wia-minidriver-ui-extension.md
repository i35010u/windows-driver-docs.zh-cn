---
title: 创建"Hello World"WIA 微型驱动程序 UI 扩展
description: 创建"Hello World"WIA 微型驱动程序 UI 扩展
ms.assetid: 8de1f8ca-f618-44d7-b6dd-c02cdee8a556
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d164e80fab69b0333ba190cf033c3f32437405
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547069"
---
# <a name="creating-a-hello-world-wia-minidriver-ui-extension"></a>创建"Hello World"WIA 微型驱动程序 UI 扩展





WIA 微型驱动程序的 UI 扩展是一个简单的 DLL 将导出了一些功能并实现在至少一个四个以下 COM 接口标识符 (IID):

<a href="" id="iid-iwiauiextension"></a>IID\_IWiaUIExtension  
接口标识符 (IID) **IWiaUIExtension**接口。 这是用来替换我的电脑和控件面板中的微型驱动程序设备图标并将为 Microsoft 公共微型驱动程序用户界面对话框的标准 WIA 接口。

<a href="" id="iid-ishellextinit"></a>IID\_IShellExtInit  
IID **IShellExtInit**接口。 这是标准的 Windows Shell 接口用来初始化属性表、 快捷方式菜单和拖放处理程序 （在非默认拖放操作期间将项添加到快捷菜单的扩展） 的 Shell 扩展。

<a href="" id="iid-icontextmenu"></a>IID\_IContextMenu  
IID **ContextMenu**接口。 这是标准的 Windows Shell 接口用于创建或合并与外壳对象 （WIA 微型驱动程序图标在我的电脑和控制面板中） 关联的快捷菜单。

<a href="" id="iid-ishellpropsheet"></a>IID\_IShellPropSheet  
IID **IShellPropSheet**接口。 这是用来添加或替换为 Shell 对象 （我的电脑和控制面板中的图标进行 WIA 的微型驱动程序） 显示在属性表中的页的标准 Windows Shell 接口。

"Hello World"WIA 微型驱动程序的 UI 扩展包含以下文件：

<a href="" id="hellowld-inf"></a>*hellowld.inf*  
这是安装文件 (修改以使用原始安装此 UI 扩展插件*hellowld*示例)。

<a href="" id="hellowldui-def"></a>*hellowldui.def*  
这是包含两个 COM 导出定义文件**DllGetClassObject**并**DllCanUnloadNow** （同时描述了 Windows SDK 文档中）。

<a href="" id="hellowldui-cpp"></a>*hellowldui.cpp*  
这是 WIA UI 扩展插件实现。

### <a name="installing-wia-ui-extensions"></a>安装 WIA UI 扩展

若要安装 WIA UI 扩展 DLL，添加**UI 类 ID =**{&lt;UI 扩展 DLL 的 CLSID&gt;} 下 INF 文件**DeviceData**部分。 此 CLSID 允许客户端调用**CoCreateInstance** （Microsoft Windows SDK 文档中介绍），并获取 WIA UI 扩展插件的受支持的接口。

下面的示例 INF 段派生自中的 WIA 微型驱动程序示例[创建 Hello World WIA 微型驱动程序](creating-a---hello-world---wia-minidriver.md)。 默认情况下使用的 CLSID 应该是公共对话框、 图标和属性页的 Microsoft 提供的 CLSID。

建议所有 WIA UI 扩展 Dll 应自都注册 COM 对象，以促进更容易安装。 此示例不包含自行注册的 COM 对象。

```INF
[WIADevice.DeviceData]
Server=local
UI DLL=sti.dll
UI Class ID={4DB1AD10-3391-11D2-9A33-00C04FA36145}
```

下面的示例是一个完整的 INF 文件，用于设置**UI 类 ID**对 CLSID 的子项*hellowldui*示例 UI 扩展。

```INF
; HELLOWLD.INF  -- Hello World WIA Minidriver setup file (with a WIA UI extension DLL)
; Copyright (c) 2002 Hello World Company
; Manufacturer:  Hello World Company

[Version]
Signature="$WINDOWS NT$"
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%Mfg%
DriverVer=06/26/2001,1.0
CatalogFile=wia.cat

[DestinationDirs]
DefaultDestDir=11

[Manufacturer]
%Mfg%=Models

[Models]
%WIADevice.DeviceDesc% = WIADevice.Scanner, HELLOWORLD_PNP_ID

[WIADevice.Scanner]
Include=sti.inf
Needs=STI.SerialSection
SubClass=StillImage
DeviceType=1
DeviceSubType=0x0
Capabilities=0x30
DeviceData=WIADevice.DeviceData
AddReg=WIADevice.AddReg
CopyFiles=WIADevice.CopyFiles
ICMProfiles="sRGB Color Space Profile.icm"

[WIADevice.Scanner.Services]
Include=sti.inf
Needs=STI.SerialSection.Services

[WIADevice.DeviceData]
Server=local
UI DLL=sti.dll
UI Class ID={7C1E2309-A535-45b1-94B3-9A020EE600C7}

[WIADevice.AddReg]
HKR,,HardwareConfig,1,1
HKR,,USDClass,,"{7C1E2309-A535-45b1-94B3-9A020EE600C6}"
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6},,,"Hello World WIA Minidriver"
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6}\InProcServer32,,,%11%\hellowld.dll
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6}\InProcServer32,ThreadingModel,,Both

HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C7},,,"Hello World WIA Minidriver UI Extension"
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C7}\InProcServer32,,,%11%\hellowldui.dll
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C7}\InProcServer32,ThreadingModel,,Both
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C7}\shellex\WiaDialogExtensionHandlers\{7C1E2309-A535-45b1-94B3-9A020EE600C7}

[WIADevice.CopyFiles]
hellowld.dll
hellowldui.dll

[SourceDisksFiles.x86]
hellowld.dll=1
hellowldui.dll=1

[SourceDisksNames.x86]
1=%Location%,,,

[SourceDisksFiles.IA64]
hellowld.dll=1
hellowldui.dll=1
[SourceDisksNames.IA64]
1=%Location%,,,

[Strings]
Mfg="Hello World Company"
WIADevice.DeviceDesc="Hello World WIA Minidriver"
Location="Hello World WIA Minidriver Installation Source"
```

*Hellowldui.def*文件应包含以下：

```make
LIBRARY HELLOWLDUI

EXPORTS
        DllGetClassObject   PRIVATE
        DllCanUnloadNow     PRIVATE
```

*Hellowldui.cpp*文件应包含以下：

```cpp
#ifndef WIN32_LEAN_AND_MEAN
#define WIN32_LEAN_AND_MEAN
#endif

#include <windows.h>
#include <initguid.h>
#include <wiadevd.h>
#include <shobjidl.h>
#include <shlobj.h>

// {7C1E2309-A535-45b1-94B3-9A020EE600C7}
DEFINE_GUID(CLSID_HelloWorldWIAUIExtension, 0x7c1e2309, 0xa535, 0x45b1, 0x94, 0xb3, 0x9a, 0x2, 0xe, 0xe6, 0x0, 0xc7);

class CWIAUIExtension : public IWiaUIExtension,   // WIA UI Extension interface
                        public IShellExtInit,     // SHELL Extension interface
                        public IContextMenu,      // SHELL context menu Extension interface
                        public IShellPropSheetExt // SHELL property sheet interface
{
public:

    /////////////////////////////////////////////////////////////////////////
    // Construction/Destruction Section                                    //
    /////////////////////////////////////////////////////////////////////////

    CWIAUIExtension() : m_cRef(1) {
    }

    ~CWIAUIExtension() {
    }

private:
    LONG m_cRef; // object reference count.
public:

    /////////////////////////////////////////////////////////////////////////
    // Standard COM Section                                                //
    /////////////////////////////////////////////////////////////////////////

    STDMETHODIMP QueryInterface(REFIID  riid,LPVOID  *ppvObj)
    {
        if (!ppvObj) {
            return E_INVALIDARG;
        }

        *ppvObj = NULL;

        if (IsEqualIID( riid, IID_IUnknown )) {
            *ppvObj = reinterpret_cast<IUnknown*>(this);
        } else if (IsEqualIID( riid, IID_IWiaUIExtension )) {
            *ppvObj = static_cast<IWiaUIExtension*>(this);
        } else {
            return E_NOINTERFACE;
        }

        reinterpret_cast<IUnknown*>(*ppvObj)->AddRef();
        return S_OK;
    }

    STDMETHODIMP_(ULONG) AddRef()
    {
        return InterlockedIncrement(&m_cRef);
    }

    STDMETHODIMP_(ULONG) Release()
    {
        if(InterlockedDecrement(&m_cRef) == 0) {
        delete this;
            return 0;
        }
        return m_cRef;
    }

    /////////////////////////////////////////////////////////////////////////
    // IWiaUIExtension Interface Section                                   //
    /////////////////////////////////////////////////////////////////////////
    STDMETHODIMP DeviceDialog( PDEVICEDIALOGDATA pDeviceDialogData ) {return E_NOTIMPL;}
    STDMETHODIMP GetDeviceIcon( BSTR bstrDeviceId, HICON *phIcon, ULONG nSize ){
 HRESULT hr = E_NOTIMPL;
        HICON hIcon = reinterpret_cast<HICON>(LoadImage(NULL,
                                                        MAKEINTRESOURCE(IDI_APPLICATION),
                                                        IMAGE_ICON,
                                             nSize,
                                                        nSize,
                                                        LR_SHARED));
        if (hIcon) {
            *phIcon = CopyIcon(hIcon);
            hIcon = NULL;
            hr = S_OK;
        }
        return hr;
    }
    STDMETHODIMP GetDeviceBitmapLogo( BSTR bstrDeviceId, HBITMAP *phBitmap, ULONG nMaxWidth, ULONG nMaxHeight ){return E_NOTIMPL;}

    /////////////////////////////////////////////////////////////////////////
    // IShellExtInit Interface Section                                   //
    /////////////////////////////////////////////////////////////////////////
    STDMETHODIMP Initialize (LPCITEMIDLIST pidlFolder,LPDATAOBJECT lpdobj,HKEY hkeyProgID){return E_NOTIMPL;}

    /////////////////////////////////////////////////////////////////////////
    // IContextMenu Interface Section                                   //
    /////////////////////////////////////////////////////////////////////////
    STDMETHODIMP QueryContextMenu (HMENU hmenu,UINT indexMenu,UINT idCmdFirst,UINT idCmdLast,UINT uFlags) {return E_NOTIMPL;}
    STDMETHODIMP InvokeCommand    (LPCMINVOKECOMMANDINFO lpici){return E_NOTIMPL;}
    STDMETHODIMP GetCommandString (UINT_PTR idCmd, UINT uType,UINT* pwReserved,LPSTR pszName,UINT cchMax) {return E_NOTIMPL;}

    /////////////////////////////////////////////////////////////////////////
    // IShellPropSheetExt Interface Section                                   //
    /////////////////////////////////////////////////////////////////////////
    STDMETHODIMP AddPages (LPFNADDPROPSHEETPAGE lpfnAddPage,LPARAM lParam){return E_NOTIMPL;}
    STDMETHODIMP ReplacePage (UINT uPageID,LPFNADDPROPSHEETPAGE lpfnReplacePage,LPARAM lParam) {return E_NOTIMPL;}
};

/////////////////////////////////////////////////////////////////////////
// IClassFactory Interface Section (for all COM objects)               //
/////////////////////////////////////////////////////////////////////////

class CWIAUIClassFactory : public IClassFactory {
public:
    CWIAUIClassFactory() : m_cRef(1) {}
    ~CWIAUIClassFactory(){}
    STDMETHODIMP QueryInterface(REFIID riid, LPVOID *ppv)
    {
      if (!ppv) {
            return E_INVALIDARG;
        }

        *ppv = NULL;
        HRESULT hr = E_NOINTERFACE;
        if (IsEqualIID(riid, IID_IUnknown) || IsEqualIID(riid, IID_IClassFactory)) {
            *ppv = static_cast<IClassFactory*>(this);
            reinterpret_cast<IUnknown*>(*ppv)->AddRef();
            hr = S_OK;
        }
        return hr;
    }
    STDMETHODIMP_(ULONG) AddRef()
    {
        return InterlockedIncrement(&m_cRef);
    }
    STDMETHODIMP_(ULONG) Release()
    {
  if(InterlockedDecrement(&m_cRef) == 0) {
            delete this;
            return 0;
        }
        return m_cRef;
    }
    STDMETHODIMP CreateInstance(IUnknown __RPC_FAR *pUnkOuter,REFIID riid,void __RPC_FAR *__RPC_FAR *ppvObject)
    {
        if ((pUnkOuter)&&(!IsEqualIID(riid,IID_IUnknown))) {
            return CLASS_E_NOAGGREGATION;
        }

        HRESULT hr = E_NOINTERFACE;
        CWIAUIExtension *pUIExt = new CWIAUIExtension();
        if (pUIExt) {
            hr = pUIExt->QueryInterface(riid,ppvObject);
            pUIExt->Release();
        } else {
            hr = E_OUTOFMEMORY;
        }

        return hr;
    }
    STDMETHODIMP LockServer(BOOL fLock){return S_OK;}
private:
    LONG m_cRef;
};

/////////////////////////////////////////////////////////////////////////
// DLL Entry Point Section (for all COM objects, in a DLL)             //
/////////////////////////////////////////////////////////////////////////

extern "C" __declspec(dllexport) BOOL APIENTRY DllEntryPoint(HINSTANCE hinst,DWORD dwReason,LPVOID lpReserved)
{
    switch (dwReason) {
    case DLL_PROCESS_ATTACH:
        break;
    }
    return TRUE;
}

extern "C" STDMETHODIMP DllCanUnloadNow(void){return S_OK;}
extern "C" STDAPI DllGetClassObject(REFCLSID rclsid,REFIID riid,LPVOID *ppv)
{
    if (!ppv) {
        return E_INVALIDARG;
    }
    HRESULT hr = CLASS_E_CLASSNOTAVAILABLE;
    if (IsEqualCLSID(rclsid, CLSID_HelloWorldWIAUIExtension)) {
        CWIAUIClassFactory *pcf = new CWIAUIClassFactory;
        if (pcf) {
            hr = pcf->QueryInterface(riid,ppv);
            pcf->Release();
        } else {
            hr = E_OUTOFMEMORY;
        }
    }
    return hr;
}
```

### <a name="adding-a-custom-device-icon"></a>添加自定义设备图标

前面的示例是如何替换为你的设备的默认图标的示例。 替换默认图标可以指导用户在使用正确的设备，如果安装多个设备的理想方法。 如果图标类似于连接的设备，它将会更直观的用户。

 

 




