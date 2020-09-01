---
title: 通过驱动程序写入 WIA 属性
description: 通过驱动程序写入 WIA 属性
ms.assetid: 6d2164ac-0fbc-4ecb-b3bf-a46efbe07f51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 675192b36a806c1a034831461c46edf66ff55cbf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190719"
---
# <a name="writing-wia-properties-by-a-driver"></a>通过驱动程序写入 WIA 属性





WIA 微型驱动程序可以通过使用以下 WIA 服务函数来更新其 WIA 属性和有效值的任何当前值：

<a href="" id="wiaswritemultiple"></a>[**wiasWriteMultiple**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)  
写入所有 WIA 属性类型。 这是一个常规功能，它允许 WIA 驱动程序写入 WIA 项（包括自定义属性）中的任何现有属性。 它可用于写入每个调用的多个属性。

<a href="" id="wiaswritepropstr"></a>[**wiasWritePropStr**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropstr)  
写入作为字符串 (类型 VT BSTR) 的 WIA 属性 \_ 。

<a href="" id="wiaswriteproplong"></a>[**wiasWritePropLong**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswriteproplong)  
 (type VT I4) 中写入 WIA 属性，其类型为四字节整数 \_ 。

<a href="" id="wiaswritepropfloat"></a>[**wiasWritePropFloat**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropfloat)  
 (键入 VT R4) ，将包含四个字节实数的 WIA 属性写入 \_ 。

<a href="" id="wiaswritepropguid"></a>[**wiasWritePropGuid**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropguid)  
将作为 Guid 的 WIA 属性写入 (类型 VT \_ CLSID) 。

<a href="" id="wiaswritepropbin"></a>[**wiasWritePropBin**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropbin)  
将作为无符号字节字符串的 WIA 属性写入 (类型 VT \_ VECTOR |VT \_ UI1) 。

<a href="" id="wiasgetchangedvaluelong"></a>[**wiasGetChangedValueLong**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)  
获取由四个字节的整数 (type VT I4) 的 WIA 属性的当前更改信息 \_ 。

<a href="" id="wiasgetchangedvaluefloat"></a>[**wiasGetChangedValueFloat**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)  
 (type VT) ，获取 WIA 属性的当前更改的信息，这些属性是四字节实数 \_ 。

<a href="" id="wiasgetchangedvalueguid"></a>[**wiasGetChangedValueGuid**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)  
获取作为 Guid 的 WIA 属性的当前更改的信息， (type VT \_ CLSID) 。

<a href="" id="wiasgetchangedvaluestr"></a>[**wiasGetChangedValueStr**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)  
获取作为字符串 (类型 VT BSTR) 的 WIA 属性的当前更改信息 \_ 。

<a href="" id="wiascreatepropcontext"></a>[**wiasCreatePropContext**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)  
创建 WIA 属性上下文，用于 [**wiasGetChangedValueLong**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)、 [**wiasGetChangedValueFloat**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)、 [**wiasGetChangedValueGuid**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)和 [**wiasGetChangedValueStr**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr) 服务函数。

<a href="" id="wiasfreepropcontext"></a>[**wiasFreePropContext**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasfreepropcontext)  
释放由 [**wiasCreatePropContext**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)创建的已分配上下文内存。

### <a name="implementing-iwiaminidrvdrvvalidateitemproperties"></a><a href="" id="implementing-iwiaminidrv-drvvalidateitemproperties"></a>实现 IWiaMiniDrv：:d rvValidateItemProperties

当对项的 WIA 属性进行更改时，将调用 [**IWiaMiniDrv：:D rvvalidateitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties) 方法。 WIA 微型驱动程序不仅应检查值是否有效，而且必须更新任何更改的有效值。

如果 WIA 属性无效，并且应用程序没有写入它，则必须将无效值和任何依赖值更改为有效值，否则验证 (将失败，因为应用程序会将属性设置为无效的值) 。

下面的示例演示 **IWiaMiniDrv：:D rvvalidateitemproperties** 方法的实现：

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

 

