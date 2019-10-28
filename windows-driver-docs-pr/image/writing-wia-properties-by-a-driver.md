---
title: 通过驱动程序写入 WIA 属性
description: 通过驱动程序写入 WIA 属性
ms.assetid: 6d2164ac-0fbc-4ecb-b3bf-a46efbe07f51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c2bbaf4b6b389134499cf2cbf12772b1ad1e56e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840658"
---
# <a name="writing-wia-properties-by-a-driver"></a>通过驱动程序写入 WIA 属性





WIA 微型驱动程序可以通过使用以下 WIA 服务函数来更新其 WIA 属性和有效值的任何当前值：

<a href="" id="wiaswritemultiple"></a>[**wiasWriteMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)  
写入所有 WIA 属性类型。 这是一个常规功能，它允许 WIA 驱动程序写入 WIA 项（包括自定义属性）中的任何现有属性。 它可用于写入每个调用的多个属性。

<a href="" id="wiaswritepropstr"></a>[**wiasWritePropStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropstr)  
写入作为字符串的 WIA 属性（类型为 VT\_BSTR）。

<a href="" id="wiaswriteproplong"></a>[**wiasWritePropLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswriteproplong)  
写入由四个字节构成的 WIA 属性（VT\_I4）。

<a href="" id="wiaswritepropfloat"></a>[**wiasWritePropFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropfloat)  
编写四字节实数的 WIA 属性（VT\_R4）。

<a href="" id="wiaswritepropguid"></a>[**wiasWritePropGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropguid)  
写入作为 Guid 的 WIA 属性（type VT\_CLSID）。

<a href="" id="wiaswritepropbin"></a>[**wiasWritePropBin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropbin)  
写入作为无符号字节的字符串的 WIA 属性（类型 VT\_VECTOR |VT\_UI1）。

<a href="" id="wiasgetchangedvaluelong"></a>[**wiasGetChangedValueLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)  
获取由四个字节构成的 WIA 属性的当前更改信息（VT\_I4）。

<a href="" id="wiasgetchangedvaluefloat"></a>[**wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)  
获取属于四字节实数的 WIA 属性的当前更改信息（VT\_R4）。

<a href="" id="wiasgetchangedvalueguid"></a>[**wiasGetChangedValueGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)  
获取作为 Guid （type VT\_CLSID）的 WIA 属性的当前更改信息。

<a href="" id="wiasgetchangedvaluestr"></a>[**wiasGetChangedValueStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)  
获取作为字符串的 WIA 属性（VT\_BSTR）的当前更改信息。

<a href="" id="wiascreatepropcontext"></a>[**wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)  
创建 WIA 属性上下文，用于[**wiasGetChangedValueLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)、 [**wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)、 [**wiasGetChangedValueGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)和[**wiasGetChangedValueStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)服务函数。

<a href="" id="wiasfreepropcontext"></a>[**wiasFreePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasfreepropcontext)  
释放由[**wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)创建的已分配上下文内存。

### <a href="" id="implementing-iwiaminidrv-drvvalidateitemproperties"></a>实现 IWiaMiniDrv：:d rvValidateItemProperties

当对项的 WIA 属性进行更改时，将调用[**IWiaMiniDrv：:D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)方法。 WIA 微型驱动程序不仅应检查值是否有效，而且必须更新任何更改的有效值。

如果 WIA 属性无效，并且应用程序没有写入它，则必须将无效值和任何依赖值更改为有效值，否则将无法进行验证（因为应用程序将属性设置为无效的值）。

下面的示例演示**IWiaMiniDrv：:D rvvalidateitemproperties**方法的实现：

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

 

 




