---
title: 通过驱动程序写入 WIA 属性
description: 通过驱动程序写入 WIA 属性
ms.assetid: 6d2164ac-0fbc-4ecb-b3bf-a46efbe07f51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85cb0be22dd422d0ec30df533208b6dde7179579
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373513"
---
# <a name="writing-wia-properties-by-a-driver"></a>通过驱动程序写入 WIA 属性





WIA 微型驱动程序可以通过使用以下 WIA 服务函数更新任何其 WIA 属性的当前值和有效的值：

<a href="" id="wiaswritemultiple"></a>[**wiasWriteMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple)  
编写所有 WIA 属性类型。 这是使 WIA 驱动程序上 WIA 项，包括自定义属性写入现有的任何属性的常规函数。 它可以用于写入每次调用多个属性。

<a href="" id="wiaswritepropstr"></a>[**wiasWritePropStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropstr)  
写入都是字符串的 WIA 属性 (键入 VT\_BSTR)。

<a href="" id="wiaswriteproplong"></a>[**wiasWritePropLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswriteproplong)  
写入的 4 字节整数 WIA 属性 (键入 VT\_I4)。

<a href="" id="wiaswritepropfloat"></a>[**wiasWritePropFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropfloat)  
写入的 4 字节实数 WIA 属性 (键入 VT\_R4)。

<a href="" id="wiaswritepropguid"></a>[**wiasWritePropGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropguid)  
写入 WIA 属性的 Guid (键入 VT\_CLSID)。

<a href="" id="wiaswritepropbin"></a>[**wiasWritePropBin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropbin)  
写入都是无符号字节的字符串的 WIA 属性 (键入 VT\_向量 |VT\_UI1)。

<a href="" id="wiasgetchangedvaluelong"></a>[**wiasGetChangedValueLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)  
获取有关的 4 字节整数 WIA 属性当前已更改的信息 (键入 VT\_I4)。

<a href="" id="wiasgetchangedvaluefloat"></a>[**wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)  
获取有关的四个字节实数 WIA 属性当前已更改的信息 (键入 VT\_R4)。

<a href="" id="wiasgetchangedvalueguid"></a>[**wiasGetChangedValueGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)  
获取有关 Guid 的 WIA 属性当前已更改的信息 (键入 VT\_CLSID)。

<a href="" id="wiasgetchangedvaluestr"></a>[**wiasGetChangedValueStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)  
获取有关字符串的 WIA 属性当前已更改的信息 (键入 VT\_BSTR)。

<a href="" id="wiascreatepropcontext"></a>[**wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext)  
创建中使用的 WIA 属性上下文[ **wiasGetChangedValueLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)， [ **wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)， [ **wiasGetChangedValueGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)，并[ **wiasGetChangedValueStr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)服务函数。

<a href="" id="wiasfreepropcontext"></a>[**wiasFreePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasfreepropcontext)  
释放由创建的已分配的上下文内存[ **wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext)。

### <a href="" id="implementing-iwiaminidrv-drvvalidateitemproperties"></a>实现 IWiaMiniDrv::drvValidateItemProperties

[ **IWiaMiniDrv::drvValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)项的 WIA 属性发生更改时调用方法。 WIA 微型驱动程序应仅检查值有效，但必须更新任何有效的值所做的更改。

如果 WIA 属性是无效的并且该应用程序不向其写入，无效值和任何相关的值必须更改为有效的值，否则会验证失败 （因为该应用程序将属性设置为无效值）。

下面的示例演示的实现**IWiaMiniDrv::drvValidateItemProperties**方法：

```cpp
HRESULT _stdcall CWIADevice::drvValidateItemProperties(
  BYTE           *pWiasContext,
  LONG           lFlags,
  ULONG          nPropSpec,
  const PROPSPEC *pPropSpec,
  LONG           *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
  //  then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
      return E_INVALIDARG;
  }

  if (!plDevErrVal) {
      return E_INVALIDARG;
  }

  if (!pPropSpec) {
      return E_INVALIDARG;
  }

  HRESULT hr      = S_OK;
  LONG lItemType  = 0;
  WIA_PROPERTY_CONTEXT Context;

  *plDevErrVal = 0;

  //
  // create a WIA property context, to gain access to
  // the WIA application's intended settings.
  //

  hr = wiasCreatePropContext(nPropSpec,
                             (PROPSPEC*)pPropSpec,
                             0,
                             NULL,
                             &Context);
  if(S_OK == hr) {

    //
    // get the current item type to help determine what property set to validate
    //

      hr = wiasGetItemType(pWiasContext, &lItemType);
      if (S_OK == hr) {
          if (lItemType & WiaItemTypeRoot) {

            //
            //  validate root item properties here
            //

        } else {

            //
            // validate item properties here
            //

              WIAS_CHANGED_VALUE_INFO cviDataType;
              memset(&cviDataType,0,sizeof(cviDataType));

            //
            // check to see if the application was updating
            // the WIA_IPA_DATATYPE property
   //

              hr = wiasGetChangedValueLong(pWiasContext,pContext,FALSE,WIA_IPA_DATATYPE,&cviDataType);
              if(S_OK == hr) {
                  if (cviDataType.bChanged) {

                    //
                    // This value was changed, and needs to be checked
                    //
                    // cviDataType.Current.lVal is the current application setting.
                    //

                  } else {

                    //
                    // Nothing has been changed, so leave this property alone.
                    // Let the WIA service function wiasValidateItemProperties
                    // do the rest of the work for you.
                    //

 }
              }
          }

        //
        // free the property context
        //

          wiasFreePropContext(&Context);
      }

    //
    // call WIA service helper when you have finished updating dependent values
    //

    if(S_OK == hr) {

        //
        // call WIA service helper to validate other properties
        //

          hr = wiasValidateItemProperties(pWiasContext, nPropSpec, pPropSpec);
      }
  }
  return hr;
}
```

 

 




