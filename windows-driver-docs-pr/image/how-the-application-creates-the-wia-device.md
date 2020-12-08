---
title: 应用程序如何创建 WIA 设备
description: 应用程序如何创建 WIA 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08103c98bc2709077b1bae2e1a4eafe4be031a35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793739"
---
# <a name="how-the-application-creates-the-wia-device"></a>应用程序如何创建 WIA 设备





当应用程序打算使用 WIA 设备驱动程序时，它将调用 **IWiaDevMgr：： CreateDevice** 方法， (在 Microsoft Windows SDK 文档) 中所述。 WIA 服务首先调用 [**IStiUSD：： LockDevice**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice) ，以将 WIA 驱动程序锁定为互相排斥的访问。 接下来，WIA 服务调用 [**IWiaMiniDrv：:D rvinitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia) 创建初始 WIA 项树结构。 最后，WIA 服务通过调用 [**IStiUSD：： UnLockDevice**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)解锁设备驱动程序。

**IWiaMiniDrv：:D rvinitializewia** 方法应执行以下任务。

1.  缓存 *pStiDevice* 参数指向的接口以获取适当的设备锁定。  (有关详细信息，请参阅 [**IWiaMiniDrv：:D rvlockwiadevice**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)。 ) 

2.  创建初始 WIA 项树结构。

3.  递增当前应用程序连接数。 此计数用于通知驱动程序应用程序是否仍处于连接状态。 它还有助于确定要在 IWiaMiniDrv 中采取的正确操作 [**：:D rvuninitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)。

WIA 项的名称应带有一些逻辑含义。 Microsoft 需要适用于 Windows XP 和更高版本的以下项名称。

<a href="" id="root"></a>**Root**  
这是 WIA 项树的根项的术语。

<a href="" id="flatbed"></a>**平板**  
这是仅支持平板扫描仪或支持带有文档送纸器的平板扫描仪的扫描仪的术语。

<a href="" id="feeder"></a>**放**  
这是仅支持送纸器的扫描仪的术语。

WIA 服务调用 **IWiaMiniDrv：:D rvinitializewia** 方法来响应 WIA 应用程序对 **IWiaDevMgr：： (CreateDevice** 的调用，Windows SDK 文档) 中所述。 这样做的结果是 WIA 服务为每个新的客户端连接调用 **IWiaMiniDrv：:D rvinitializewia** 方法。

**IWiaMiniDrv：:D rvinitializewia** 方法应初始化任何专用结构，并创建驱动程序项树。 驱动程序项树显示此 WIA 设备支持的所有 WIA 项的布局。 此方法仅用于创建初始树结构， *而不* 是 (WIA 属性) 的内容。 WIA 服务将通过多次调用 [**IWiaMiniDrv：:D rvinititemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties) 方法来分别填充 wia 驱动程序项的 wia 属性。

所有 WIA 设备都有一个根项，它是所有 WIA 设备项的父项。 若要创建 WIA 设备项，WIA 驱动程序应调用 WIA 服务 helper 函数 [**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)。

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

若要创建 WIA 子项，请在上一个示例中创建的根项的紧下方，使用如下所示的代码。

**注意**  * * * * * * * * 请注意， [**IWiaDrvItem：： AddItemToFolder**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder) 方法用于将新创建的子项目添加到根项。

 

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

下面的示例演示 **IWiaMiniDrv：:D rvinitializewia** 方法的实现。

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

 

