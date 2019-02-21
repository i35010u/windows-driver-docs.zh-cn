---
title: 应用程序如何创建 WIA 设备
description: 应用程序如何创建 WIA 设备
ms.assetid: f4268c61-11e5-4796-b7cb-80c8112be4d8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6c0846eca30a6623dd8ea98aaf1811b9a59d73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525448"
---
# <a name="how-the-application-creates-the-wia-device"></a>应用程序如何创建 WIA 设备





当应用程序想要使用 WIA 的设备驱动程序时，它将调用**IWiaDevMgr::CreateDevice**方法 （Microsoft Windows SDK 文档中所述）。 WIA 服务首先调用[ **IStiUSD::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543829)锁定互斥独占访问的 WIA 驱动程序。 接下来，WIA 服务调用[ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)创建初始 WIA 项树状结构。 最后，WIA 服务解锁设备驱动程序通过调用[ **IStiUSD::UnLockDevice**](https://msdn.microsoft.com/library/windows/hardware/ff543843)。

**IWiaMiniDrv::drvInitializeWia**方法应执行以下任务。

1.  缓存接口的*pStiDevice*参数指向正确的设备锁定。 (有关详细信息，请参阅[ **IWiaMiniDrv::drvLockWiaDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544995)。)

2.  创建初始 WIA 项树状结构。

3.  递增当前应用程序连接数。 此计数用来通知该驱动程序是否仍连接应用程序。 它还有助于确定要在中执行的适当操作[ **IWiaMiniDrv::drvUnInitializeWia**](https://msdn.microsoft.com/library/windows/hardware/ff545010)。

WIA 项应被命名为某些逻辑含义。 Microsoft 需要以下项名称适用于 Windows XP 及更高版本。

<a href="" id="root"></a>**Root**  
这是 WIA 项树的根项目使用的术语。

<a href="" id="flatbed"></a>**平板**  
这是支持平板扫描仪，扫描程序或支持具有文档送纸器平板扫描仪的扫描的术语。

<a href="" id="feeder"></a>**送纸器**  
这是支持只进纸器的扫描仪的术语。

WIA 服务调用**IWiaMiniDrv::drvInitializeWia**响应 WIA 应用程序的调用中的方法**IWiaDevMgr::CreateDevice** （Windows SDK 文档中所述）。 这样的后果是 WIA 服务调用**IWiaMiniDrv::drvInitializeWia**为每个新的客户端连接的方法。

**IWiaMiniDrv::drvInitializeWia**方法应初始化任何专用的结构并创建驱动程序项树。 驱动程序项树显示了此 WIA 设备支持的所有 WIA 项的布局。 此方法用于创建初始树状结构仅*不*内容 （WIA 属性）。 WIA 服务分别将通过多个调用来填充 WIA 驱动程序项的 WIA 属性[ **IWiaMiniDrv::drvInitItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff544989)方法。

所有 WIA 设备都有一个根项，它是 WIA 设备的所有项的父级。 若要创建 WIA 设备项目 WIA 驱动程序应调用 WIA 的服务帮助程序函数， [ **wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)。

下面的示例演示如何创建 WIA 设备根项。

```cpp
LONG lItemFlags = WiaItemTypeFolder|WiaItemTypeDevice|WiaItemTypeRoot;
IWiaDrvItem  *pIWiaDrvRootItem  = NULL;
HRESULT hr = 
    wiasCreateDrvItem(
                       lItemFlags, // item flags
                       bstrRootItemName, // item name ("Root")
                       bstrRootFullItemName, // item full name ("0000\Root")
                      (IWiaMiniDrv *)this, // this WIA driver object
                       sizeof(MINIDRIVERITEMCONTEXT), // size of context
                       NULL, // context
                       &pIWiaDrvRootItem // created ROOT item
                      );                 // (IWiaDrvItem interface)

if(S_OK == hr){

  //
  // ROOT item was created successfully
  //

 }
```

若要创建 WIA 子项目，直接位于上一示例中创建的根项目使用类似于下面的代码。

**请注意**  * * * 注意[ **IWiaDrvItem::AddItemToFolder** ](https://msdn.microsoft.com/library/windows/hardware/ff543856)调用方法以将新创建的子项目添加到根项。

 

```cpp
LONG lItemFlags = WiaItemTypeFile|WiaItemTypeDevice|WiaItemTypeImage;
PMINIDRIVERITEMCONTEXT pItemContext    = NULL;
IWiaDrvItem           *pIWiaDrvNewItem = NULL;
HRESULT hr = 
    wiasCreateDrvItem(
                       lItemFlags, // item flags
                       bstrItemName,  // item name ("Flatbed")
                       bstrFullItemName,  // item full name ("0000\Root\Flatbed")
                      (IWiaMiniDrv *)this,  // this WIA driver object
     sizeof(MINIDRIVERITEMCONTEXT), // size of context
                      (PBYTE)&pItemContext, // context
                      &pIWiaDrvNewItem // created child item
                     );                // (IWiaDrvItem interface)  

if(S_OK == hr){

  //
  // A New WIA driver item was created successfully
  //

  hr = pIWiaDrvNewItem->AddItemToFolder(pIWiaDrvRootItem); // add the new item to the ROOT
  if(S_OK == hr){

     //
     // successfully created and added a new WIA driver item to 
     // the WIA driver item tree.
    //

   }
   pNewItem->Release();
   pNewItem = NULL;
 }
```

下面的示例演示的实现**IWiaMiniDrv::drvInitializeWia**方法。

```cpp
HRESULT _stdcall CWIADevice::drvInitializeWia(
  BYTE        *pWiasContext,
  LONG        lFlags,
  BSTR        bstrDeviceID,
  BSTR        bstrRootFullItemName,
  IUnknown    *pStiDevice,
  IUnknown    *pIUnknownOuter,
  IWiaDrvItem **ppIDrvItemRoot,
  IUnknown    **ppIUnknownInner,
  LONG        *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
 // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
      return E_INVALIDARG;
  }

  if (!plDevErrVal) {
      return E_INVALIDARG;
  }

  HRESULT hr = S_OK;

  *plDevErrVal = 0;
  *ppIDrvItemRoot = NULL;
  *ppIUnknownInner = NULL;

  if (m_pStiDevice == NULL) {

      //
      // save STI device interface for locking
      //

      m_pStiDevice = (IStiDevice *)pStiDevice;
  }

  //
  // build WIA item tree
  //

  LONG lItemFlags = WiaItemTypeFolder|WiaItemTypeDevice|WiaItemTypeRoot;

  IWiaDrvItem  *pIWiaDrvRootItem  = NULL;

  //
  // create the ROOT item of the WIA device.  This name should NOT be 
  // localized in different languages. "Root" is used by WIA drivers.
  //

  BSTR bstrRootItemName = SysAllocString(WIA_DEVICE_ROOT_NAME);
  if(!bstrRootItemName) {
      return E_OUTOFMEMORY;
  }

  hr = wiasCreateDrvItem(lItemFlags,  // item flags
               bstrRootItemName,  // item name ("Root")
               bstrRootFullItemName,  // item full name ("0000\Root")
                (IWiaMiniDrv *)this,  // this WIA driver object
      sizeof(MINIDRIVERITEMCONTEXT),  // size of context
                               NULL,  // context
                 &pIWiaDrvRootItem);  // created ROOT item
                                      // (IWiaDrvItem interface)
  if (S_OK == hr) {

    //
    // ROOT item was created successfully, save the newly created Root
    // item in the pointer given by the WIA service (ppIDrvItemRoot).
    //

      *ppIDrvItemRoot = pIWiaDrvRootItem;

    //
    // Create a child item  directly under the Root WIA item
    //

      lItemFlags = WiaItemTypeFile|WiaItemTypeDevice|WiaItemTypeImage;

      PMINIDRIVERITEMCONTEXT pItemContext    = NULL;
      IWiaDrvItem           *pIWiaDrvNewItem = NULL;

      //
      // create a name for the WIA child item.  "Flatbed" is used by 
      // WIA drivers that support a flatbed scanner.
      //

      BSTR bstrItemName = SysAllocString(WIA_DEVICE_FLATBED_NAME);

      if (bstrItemName) {

          WCHAR  wszFullItemName[MAX_PATH + 1] = {0};
          _snwprintf(wszFullItemName,(sizeof(wszFullItemName) / sizeof(WCHAR)) - 1,L"%ls\\%ls",
                   bstrRootFullItemName,bstrItemName);

        BSTR bstrFullItemName = SysAllocString(wszFullItemName);
        if (bstrFullItemName) {
          hr = wiasCreateDrvItem(lItemFlags,  // item flags
                               bstrItemName,  // item name ("Flatbed")
                             trFullItemName,  // item full name ("0000\Root\Flatbed")
                        (IWiaMiniDrv *)this,  // this WIA driver object
               sizeof(MINIDRIVERITEMCONTEXT), // size of context
                       (BYTE**)&pItemContext, // context
                        &pIWiaDrvNewItem);    // created child item
                                              // (IWiaDrvItem interface)

            if (S_OK == hr) {

                //
                // A New WIA driver item was created successfully
                //

                hr = pIWiaDrvNewItem->AddItemToFolder(pIWiaDrvRootItem); // add the new item to the ROOT
  if (S_OK == hr) {

                    //
                    // successfully created and added a new WIA 
                    // driver item to the WIA driver item tree.
                    //

                }

                //
                // The new item is no longer needed, because it has
                // been passed to the WIA service.
                //

                pIWiaDrvNewItem->Release();
                pIWiaDrvNewItem = NULL;
            }
            SysFreeString(bstrFullItemName);
            bstrFullItemName = NULL;
        } else {
            hr = E_OUTOFMEMORY;
        }
        SysFreeString(bstrItemName);
        bstrItemName = NULL;
    } else {
        hr = E_OUTOFMEMORY;
    }
  }

  //
  // increment application connection count
  //

  if(S_OK == hr){
    InterlockedIncrement(&m_lClientsConnected);
  }

  return hr;
}
```

 

 




