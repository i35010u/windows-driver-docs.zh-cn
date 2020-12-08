---
title: WIA 错误处理示例
description: WIA 错误处理示例
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6c6c3d1321e396820f0724f0e032dae4abe82289
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831715"
---
# <a name="wia-error-handling-example"></a>WIA 错误处理示例

有关发送设备状态消息的驱动程序的示例，请参阅 [Windows 映像获取 (WIA) 驱动程序示例](/samples/microsoft/windows-driver-samples/windows-image-acquisition-wia-driver-samples)中的 *扩展 WIA 2.0 怪物驱动程序* 示例。 此示例演示如何实现简单的错误处理程序。

## <a name="example-error-handling-extension"></a>示例：错误处理扩展插件

下面的代码段演示如何实现简单的错误处理扩展插件。 此错误处理扩展仅处理 WIA \_ 错误 \_ 覆盖 \_ 打开设备状态错误并显示模式对话框。 请注意，为了简化此示例，已省略某些代码。

```cpp
STDMETHODIMP

CErrHandler::ReportStatus(

IN LONG lFlags,

IN HWND hwndParent,

IN IWiaItem2 *pWiaItem2,

IN HRESULT hrStatus,

IN LONG lPercentComplete)

{

    HRESULT hr = WIA_STATUS_NOT_HANDLED;

    if (WIA_ERROR_COVER_OPEN == hrStatus)

    {

        int i;

        i = MessageBox(hwndParent,

        ERROR_COVER_OPEN_STR,

        TEXT("Driver UI Extension"),

        MB_RETRYCANCEL|MB_TASKMODAL|MB_ICONERROR);

        if (IDOK == i)

        {

            hr = S_OK;

        }

        else

        {

            hr = WIA_ERROR_COVER_OPEN;

        }

    }

    return hr;

}

STDMETHODIMP

CErrHandler::GetStatusDescription(

IN LONG lFlags,

IN IWiaItem2 *pWiaItem2,

IN HRESULT hrStatus,

OUT BSTR *pbstrDescription)

{

    HRESULT hr = pbstrDescription ? WIA_STATUS_NOT_HANDLED :

    E_INVALIDARG;

    if (WIA_ERROR_COVER_OPEN == hrStatus)

    {

        BSTR bstrDescription = NULL;

        bstrDescription = SysAllocString(ERROR_COVER_OPEN_STR);

        if (bstrDescription)

        {

            *pbstrDescription = bstrDescription;

            hr = S_OK;

        }

        else

        {

            hr = E_OUTOFMEMORY;

        }

    }

    return hr;

}
```
